---
title: Configurando o NetBeans 6.5 para inglês
date: '2008-12-15T19:39:01Z'
categories:
- Java
aliases:
- /2008/12/15/configurando-o-netbeans-65-para-ingles/
---

O NetBeans 6.5 utiliza por padrão as configurações regionais da sua máquina e se o seu computador estiver configurado para o português, ele utilizará esse idioma.

Como é horrível desenvolver utilizando uma IDE em português, aí vai a dica para configurá-lo para o inglês.

Abra o arquivo NETBEANS\_HOME/etc/netbeans.conf, onde NETBEANS\_HOME é o path de instalação do mesmo.

Localize a linha *netbeans\_default\_options* e adicione ao final dela (antes das aspas) o seguinte:  
-J-Duser.language=en
