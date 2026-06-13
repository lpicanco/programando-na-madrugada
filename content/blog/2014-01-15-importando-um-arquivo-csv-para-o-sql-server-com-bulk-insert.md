---
title: Importando um arquivo CSV para o SQL Server com BULK INSERT
date: '2014-01-15T21:08:29Z'
categories:
- SQL
tags:
- sql server
---

Como importar um arquivo CSV para o SQL Server com BULK INSERT

```
BULK
INSERT CLIENTE
FROM 'F:BULKDATACLIENTE.txt'
WITH
(
FIRSTROW = 2,   -- Ignora o header
FIELDTERMINATOR = ',',  
ROWTERMINATOR = 'n'
)
GO
```
