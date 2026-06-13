---
title: 'Erro na instalação de uma Ruby Gem: no such file to load -- mkmf'
date: '2009-05-06T14:36:18Z'
categories:
- Ruby
---

Se ao instalar uma gem você se deparou com esse erro:

```
Building native extensions.  This could take a while...
ERROR:  While executing gem ... (Gem::Installer::ExtensionBuildError)
    ERROR: Failed to build gem native extension.

ruby extconf.rb install mechanize
extconf.rb:1:in `require': no such file to load -- mkmf (LoadError)
```

from extconf.rb:1

O problema é que o mkmf não foi encontrado. Ele se encontra no pacote ruby-dev. Para instalá-lo baixa executar o seguinte comando:

```
sudo apt-get install ruby-dev
```
```
<span style="font-family: -webkit-monospace;">
</span>
```
```
<span style="font-family: -webkit-monospace;">
</span>
```
