---
title: Levantando um http server simples no OSX, de forma nativa
date: '2011-03-10T23:03:08Z'
categories:
- Python
- LifeHack
- MAC OSX
---

Estava precisando levantar um simples servidor http de páginas estáticas no osx. Após uma busca no google, descobri uma forma muito simples de fazer isso, utilizando pyhton, que ja vem embutido no osx.

É só executar o seguinte comando do diretório a ser servido:  
`Hadron:HTML lpicanco$ python -m SimpleHTTPServer 8082`

Um simples servidor HTTP será iniciado para o diretório local. *8082* é o número da porta.
