---
title: Microsoft Bug King
date: '2006-12-27T18:11:41Z'
categories:
- Ruby on Rails
aliases:
- /2006/12/27/microsoft-bug-king/
comments:
- author: jsalles
  date: '2007-03-01'
  content: também funciona com a frase "bush odeia bin laden". Portanto o bug pode ser mais complexo.
  email: jsalles@nippon.com
- author: Rodrigo Seco
  date: '2007-10-26'
  content: A primeira palavra tem q ter 4 caracteres e a terceita 3. Entre elas tem q existir uma palavra com pelo menos 3 caracteres. Depois da palavra de 3 devem ter somente palavras de 5.
  email: digoseco@gmail.com
- author: Leonardo Oliveira de LIma
  date: '2007-11-20'
  content: se vc digitar a palavra "bush não ama bin laden" o bug tbm acontecerá !
  email: leonardosarue@yahoo.com.br
---

Dessa vez, nem o notepad escapou. Existe um bug no notepad que o faz gravar incorretamente os dados quando se grava um arquivo com o conteúdo: *bush ama bin laden*

Não acredita ? Então, veja você mesmo!

1. Abra o notepad
2. Digite: *bush ama bin laden*
3. Salve o arquivo com um nome qualquer
4. Feche o notepad
5. Abra o arquivo no notepad novamente

Obviamente que o problema não é com a frase *bush ama bin laden* e sim com a seguinte sequência de caracteres:

*palavra de 4 letras* - espaço - *palavra de 3 letras* - espaço - *palavra de 3 letras* - espaço - *palavra de 5 letras*
