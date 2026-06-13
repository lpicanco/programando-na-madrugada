---
title: Instalando o Redmine no dreamhost
date: '2008-12-04T23:30:45Z'
categories:
- Gest&Atilde;?&Acirc;&pound;o
- Ruby on Rails
tags:
- redmine rails dreamhost passenger
aliases:
- /2008/12/04/instalando-o-redmine-no-dreamhost/
---

O [Redmine](http://www.redmine.org/) é uma excelente ferramenta de gerenciamento de projetos.

Se após seguir os [passos de instalação](wiki.dreamhost.com/Redmine) o layout ficar quebrado, remova o arquivo public/.htaccess

O .htaccess que vem com o redmine, tem alguns problemas de compatibilidade com o Passenger do Dreamhost
