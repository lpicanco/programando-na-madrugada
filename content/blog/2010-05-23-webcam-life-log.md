---
title: Webcam Life Log
date: '2010-05-23T21:10:35Z'
categories:
- ActionScript
- AIR
- LifeHack
tags:
- ActionScript
- AIR
- lifecaching
- lifelog
- webcam
---

O Webcam Life Log é um utilitário que tira fotos com a webcam, em um intervalo de tempo definido. Desenvolvi ele utilizando o Adobe AIR.

Para instalar, basta clicar na imagem abaixo.

**Please upgrade your Flash Player**  
This is the content that would be shown if the user does not have Flash Player 6.0.65 or higher installed.

```actionscript
// version 9.0.115 or greater is required for launching AIR apps.
var so = new SWFObject("http://webcamlifelog.googlecode.com/svn/wiki/AIRInstallBadge.swf", "", "215", "180", "9.0.115", "#000000"); 

so.useExpressInstall("http://webcamlifelog.googlecode.com/svn/wiki/expressinstall.swf");
so.addVariable("airversion", "1.5.3");
so.addVariable("appname", "Webcam%20Life%20Log");
so.addVariable("appurl", "http://webcamlifelog.googlecode.com/files/WebCamLifeLog.air");
so.addVariable("appid", "com.luizpicanco.WebCamLifeLog");
so.addVariable("appversion", "0.1");
so.write("flashcontent");
```

Screenshot:  
![](http://webcamlifelog.googlecode.com/svn/wiki/webcamlifelog.png "Webcam Life Log screenshot")

O código-fonte está disponível no google code:  
[http://code.google.com/p/webcamlifelog](http://code.google.com/p/webcamlifelog/)
