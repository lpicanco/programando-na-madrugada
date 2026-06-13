---
title: Desbloqueando o iPhone após um Restore - Couldn't locate the bytes to patch
date: '2007-10-23T19:55:48Z'
categories:
- Hacking
- iPhone
aliases:
- /2007/10/23/desbloqueando-o-iphone-apos-um-restore-couldnt-locate-the-bytes-to-patch/
comments:
- author: Iphone | Apple | Mac Blog » Desbloqueando o iPhone após um Restore - CouldnÃ¢â?¬â?¢t locate the bytes to patch
  date: '2007-10-23'
  content: '[...] Programando na Madrugada added an interesting post on Desbloqueando o iPhone após um Restore - Couldnââ?¬â?¢t locate the bytes to patchHere’s a small excerpt [...]'
- author: Humbertob
  date: '2007-10-28'
  content: 'Fiz todo o procedimento de downgrade, depois iBrickk, unlock e depois rodei o anySIM... ao final apareceu a mensagem.... "patched"... pedindo para tentar mais tarde.... tentei e nada...


    Depois tentei este tutorial bbupdater.... e também não obtive sucesso....


    O iPhone já encontra-se ativado, funcionando, inclusive youtube... porém não identifica o SIMCard...


    O que posso fazer..?'
  email: morenobatalha@gmail.com
- author: Luiz Antonio Picanço
  date: '2007-10-28'
  content: Qual a versão do firmware que você está utilizando ? Você já tinha tentado desbloquear ele antes ?
  email: lpicanco@gmail.com
- author: Humbertob
  date: '2007-10-31'
  content: fiz o Downgrade para 1.0.2. NÉ£o tinha feito nenhum procedimento antes... Era virgem
  email: morenobatalha@gmail.com
---

Após ter instalado várias aplicações no meu iPhone, a aplicação de e-mail parou de funcionar, com isso, resolvi restaurá-lo pelo iTunes para realizar o processo de desbloqueio novamente.  
Quando fui rodar o anySim, recebi a seguinte mensagem: couldn't locate the bytes to patch  
O problema é que como o baseband já estava hackeado o anySim não consegui hackea-lo novamente. Para resolver o problema tive que recorrer ao bbupdater

Segue abaixo a solução para o problema:  
1 - Você vai precisar dos seguintes arquivos (Download [aqui](http://rs157.rapidshare.com/files/55991876/314_bbfirmware.zip)):

- 314.eep
- 314.fls
- bbupdater

2 - Com o iBrickr, crie um diretório para guardar esses arquivos (Ex.: restore) e copie os 3 arquivos para lá  
3 - Pelo iBrickr, instale a aplicação MobileTerminal  
4 - No iPhone, execute o MobileTerminal  
5 - Digite os seguintes comandos:

`cd /restore`

launchctl unload /System/Library/LaunchDaemons/com.apple.CommCenter.plist

chmod +x bbupdater

bbupdater -f \*.fls -e \*.eep

launchctl load /System/Library/LaunchDaemons/com.apple.CommCenter.plist

Se você receber uma mensagem do launchtcl dizendo "no process", ignore-a.  
6 - Execute o AnySim  
7 - Enjoy!
