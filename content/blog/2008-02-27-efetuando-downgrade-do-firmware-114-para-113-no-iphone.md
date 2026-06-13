---
title: Efetuando downgrade do firmware 1.1.4 para 1.1.3 no iPhone
date: '2008-02-27T11:39:30Z'
categories:
- Hacking
- iPhone
aliases:
- /2008/02/27/efetuando-downgrade-do-firmware-114-para-113-no-iphone/
---

Olá pessoal,

Ontem atualizei sem querer para o firmware 1.1.4 e acabei com um telefone que só faz chamada de emergência. Após muito sufoco, descobri como voltar para o 1.1.3.

Passos:

1 - Efetue um restore no iTunes para o 1.1.3 (Vai dar erro, sem problemas)  
2 - Utilizando o ZiPhone, efetue o JailBreak e a ativação  
3 - Via SSH suba [esse arquivo](http://www.luizpicanco.com/uploads/downgrade-04.04.05-04.03.13.rar)(descompactado) para um diretório qualquer do iPhone e de as permissoes 755 para o bbupdater e ieraser  
3 - Efetue unload no commcenter (ulctl)  
4 - No terminal do iPhone execute:

./ieraser  
./bbupdater -f ICE04.03.13\_G.fls -e ICE04.03.13\_G.eep

5 - Efetue load no commcenter denovo e reinicie seu iphone  
6 - Pelo ZiPhone, efetue o unlock no SIM-Card

Bom pessoal é isso, o ideal é esperarem sair o Jailbreak e a ativação oficial para o 1.1.4, mas para quem atualizou essa dica pode ajudar.  
Lembrando que o meu iPhone é o 1.0.0 OTB

**Update 28/02/2008: O [ZiPhone](http://www.ziphone.org/) já está fazendo o downgrade automaticamente. Recomendo utilizar o ZiPhone para realizar o downgrade.**
