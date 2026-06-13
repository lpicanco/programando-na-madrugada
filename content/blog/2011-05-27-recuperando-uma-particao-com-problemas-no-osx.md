---
title: Recuperando uma partição com problemas no OSX
date: '2011-05-27T21:14:32Z'
categories:
- MAC OSX
tags:
- osx
---

Ontem, durante uma falha de energia, meu osx não estava conseguindo mais montar a partição de boot. A mensagem que eu estava recebendo era a seguinte:

`failed to open/create the journal  
journal is not empty  
cannot mount root, errno = 19`

Após uma série de tentativas frustradas de recuperação, consegui recuperá-la desabilitando o journal.  
Após bootar pelo cd do osx, vá para o terminal e entre com os seguintes comandos:

`sudo mount_hfs -j device mount_dir  
sudo diskutil disableJournal mount_dir  
sudo diskutil enableJournal mount_dir`

No meu caso, o device era disk0s2
