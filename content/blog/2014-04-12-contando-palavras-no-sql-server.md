---
title: Contando palavras no SQL Server
date: '2014-04-12T22:38:01Z'
categories:
- SQL
tags:
- dicas
- sql
- sql server
---

Hoje precisei executar uma consulta no SQL Server que me retornasse a quantidade de palavras de uma coluna, agrupado pela palavra.

Utilizei a consulta abaixo para fazer o serviço sujo:

```
WITH Num1 (n) AS (SELECT 1 UNION ALL SELECT 1),
Num2 (n) AS (SELECT 1 FROM Num1 AS X, Num1 AS Y),
Num3 (n) AS (SELECT 1 FROM Num2 AS X, Num2 AS Y),
Num4 (n) AS (SELECT 1 FROM Num3 AS X, Num3 AS Y),
Nums (n) AS (SELECT ROW_NUMBER() OVER(ORDER BY n) FROM Num4),
Words (word) AS (
SELECT SUBSTRING(' ' + descr + ' ', n + 1, 
       CHARINDEX(' ', ' ' + descr + ' ', n + 1) - n - 1)
FROM Nums
JOIN (SELECT text FROM TweetMessages) AS F(descr)
  ON SUBSTRING(' ' + descr + ' ', n, 1 ) = ' '
 AND n < LEN(' ' + descr + ' '))
SELECT word, COUNT(*) AS cnt 
FROM Words
GROUP BY word
ORDER BY cnt DESC
```

Não é uma maravilha de performance, mas é bem útil!

O resultado da consulta:  
[![twitterCount](http://104.131.7.34/wp-content/uploads/2014/04/twitterCount.png)](http://104.131.7.34/wp-content/uploads/2014/04/twitterCount.png)
