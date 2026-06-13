---
title: Removendo registros duplicados na base de dados
date: '2013-11-01T22:18:16Z'
categories:
- SQL
tags:
- exemplos
- script
- sql
---

[![duplicate-content](http://104.131.7.34/wp-content/uploads/2013/11/duplicate-content-300x225.jpg)](http://104.131.7.34/wp-content/uploads/2013/11/duplicate-content.jpg)  
Script SQL simples para remover os registros duplicados de uma tabela:

```sql
DELETE FROM Links
WHERE ID NOT IN
(
	SELECT MAX(ID)
	FROM Links
	GROUP BY url
)
```
> Removendo os registros com urls duplicadas da tabela Links.
