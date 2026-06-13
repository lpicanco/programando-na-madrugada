---
title: Baixando o conteúdo de uma URL no PowerShell
date: '2013-11-10T19:46:18Z'
categories:
- PowerShell
tags:
- powershell
---

Hoje precisei programar um job no SQL Server para baixar um arquivo de um site usando o powershell.

O script que eu utilizei foi esse:

```
$fileName = "c:tempfile.zip"
$webclient = New-Object System.Net.WebClient
$webclient.DownloadFile("http://siteparabaixararquivo/arquivo",$fileName)
```

Um script muito simples que as vezes poder ser útil.
