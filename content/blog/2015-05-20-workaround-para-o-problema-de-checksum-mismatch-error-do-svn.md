---
title: Workaround para o problema de checksum mismatch error do SVN
date: '2015-05-20T10:34:55Z'
categories:
- SVN
tags:
- dicas
- svn
---

Existem casos onde os metadados de uma working copy do SVN fica corrompida e durante o commit, recebemos a seguinte mensagem:

{{< highlight bash >}}
$ svn commit -m "Some update"
svn: Checksum mismatch for '/home/me/dev/bionshare/FileServer.java';
expected: '77d5a3ce97ccff226dcdaaf07d5721f5',
actual: '67d76735a0467d91c5ff733f98de451d'
{{< / highlight >}}

Existem algumas formas de resolver esse problema, como renomear o arquivo e depois restaurar o nome original. A forma mais rápida que eu encontrei foi essa:

{{< highlight bash >}}
$ svn update --set-depth empty
D FileServer.java
Updated to revision 6544.
$ svn update --set-depth infinity
A FileServer.java
Updated to revision 6544.
{{< / highlight >}}

Esses comandos restauram os dados de cache do arquivo com as informações do repositório.
