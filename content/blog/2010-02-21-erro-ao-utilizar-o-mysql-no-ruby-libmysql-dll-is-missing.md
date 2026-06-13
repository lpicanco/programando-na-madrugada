---
title: 'Erro ao utilizar o mysql no ruby: LIBMYSQL.dll is missing'
date: '2010-02-21T01:39:26Z'
categories:
- Ruby
- Ruby on Rails
tags:
- libmysql
- mysql
- rails
- Ruby
---

Um erro muito comum que costuma acontecer no ruby/rails, em ambiente windows é: "LIBMYSQL.dll is missing from your computer"

![LIMYSQL.dll is missing](http://www.luizpicanco.com/wp-content/uploads/2010/02/erro.png "erro")

E a mensagem também pode aparecer no console da seguinte forma:

```text
ruby.exe - Unable to locate Component
This application has failed to start because LIBMYSQL.DLL was not
found. Re-installing the application might
fix this problem.
```

Esse erro ocorre porque a dll do mysql, LIBMYSQL.dll, não foi localizada. Para resolver esse problema, faça o seguinte:

1 - Instale a gem do mysql

```text
gem install mysql
```

2 - Copie o arquivo LIBMYSQL.dll do diretório bin do mysql(ex.: c:mysqlbin) para o diretório bin do ruby (ex.: c:rubybin)
