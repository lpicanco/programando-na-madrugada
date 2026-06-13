---
title: Catálogo de Anti-Padrões em TDD
date: '2007-09-20T01:45:04Z'
categories:
- TDD
aliases:
- /2007/09/20/catalogo-de-anti-padroes-em-tdd/
---

Catálogo interessante prouzido pelo [James Carr](http://blog.james-carr.org/) e traduzido pelo [Victor](http://malditacomedia.blogspot.com/2007/08/tdd-anti-patterns.html)

- **The Liar** 
  - Todos os metodos de um teste unitário estão passando perfeitamente, aparentando serem validos, entretanto sob uma inspeção mais próxima é descoberto que o teste unitário não testa o real intuíto para que foi criado.

- **Excessive Setup** 
  - Um teste que necessita muito trabalho para ser configurado antes mesmo de ser executado. Algumas vezes centenas de linhas de código tornam-se necessárias para adaptar o ambiente a um único método de testes, com dezenas de objetos envolvidos. Aqui a maior dificuldade é compreender "o quê" realmente está sendo testado dentro de toda a "sujeira" que um setup pode causar. (tradutor: *Lembrem-se sempre do princípio [KISS](http://en.wikipedia.org/wiki/KISS_principle)*)

- **The Giant** 
  - Um teste unitário que, mesmo sendo verdadeiro na intenção de validar um objeto, pode possuir centenas de linhas contendo inúmeros casos de teste (inúmeros mesmos). Esta pode ser uma indicação do que chamamos de [God Object](http://en.wikipedia.org/wiki/God_object), objeto que possui responsabilidades demais dentro do sistema. Indício claro de alto acoplamento em seu sistema.

- **The Mockery** 
  - Muitas vezes um mock pode ser útil e bastante indicado. Mas desenvolvedores podem perder tempo desnecessariamente esforçando-se em mockear o que não está sendo testado. Percebe-se neste caso que a classe possuí tantos mocks, stubs ou fakes que no final das coisas o sistema não está sendo testado, mas o que é retornado da interação entre os mocks. (tradudor: *use apenas o que for estritamente necessário!*)

- **The Inspector** 
  - Um teste unitáro que viola o encapsulamente em um esforço de atingir 100% de cobertura de testes, mas está situação nem sempre é favoravél, pois qualquer tentativa de refactor pode quebrar testes desnecessariamente, necessitanto adequações nas classes de teste unitário.
- **Generous Leftovers**
  - Uma instância de um teste unitário cria um dado que é persistido em algum lugar, e outro teste utiliza tal dado para seus próprios asserts. Caso algo saia errado, o teste que utiliza o dado cadastrado também falhará. (tradutor: *Testes devem ser independentes!* )

- **The local Hero**
  - Um teste que é dependente de algo específico do ambiente de desenvolvimento em que ele foi escrito. O resultado: o teste passa perfeitamente na células de desenvolvimento, mas falha quando alguém tenta executá-lo fora desse ambiente.

- **The Nitpicker**
  - Um teste unitáro que compara toda a saída quando o que lhe deveria interessar é uma pequena parte apenas, assim o teste deve se manter sempre alinhado com detalhes que o teste não deveria tratar. Esta situação é endemica em testes de aplicações web.

- **The Dodger** 
  - Um teste unitário que possui muitos testes para efeitos pequenos (e presumidamente simples de testar), mas nunca testando o comportamente real desejado. Encontrado em testes relacionados para testes de banco de dados, onde um método é chamado, e então o teste seleciona itens do banco e procede asserts contra os resultados.

- **The Loudmout** 
  - Um teste unitário (ou suite de testes) que enxe o console com mensagens de diagnóstico, logs e qualquer outro tipo de saídas, mesmo quando os testes estão passando. Algumas vezes durante a criação dos testes existe o desejo de manualmente ver a saída dos metodos, mas mesmo eles deixando de serem necessários, são deixados para trás.

- **The Greedy Catcher** 
  - Um teste unitário que trata exceções e sobrepões pilhas de execução (stack trace) algumas vezes com mensagens menos informativas, mas algumas vezes ainda apenas logando (Loudmouth) e deixando o teste passar.

- **The Sequencer** 
  - Um teste unitário dependente de uma lista que sempre é retornada em forma desordenada.

- **Hidden Dependecy**
  - Primo de primeiro grau do "The Local Hero", um teste unitário dependente de um dado que deve ser populado em algum lugar par ao teste rodar. Se o dado não estive presente, o teste falhará deixando pouca informação para o desenvolvedor o que é necessário, ou porque o teste falhou... forçando-o a buscar através de uma floresta de código para descobrir de onde vem o dado que o teste deveria utilizar.

- **The Enumerator**
  - Um teste unitário em que os nomes de métodos são apenas uma enumeração: teste1, teste2, teste3. Como resultado, a intenção dos testes torna-se pouco clara, e a única maneira de ter certeza é ler o código fonte e rezar para que esteja bem escrito.

- **The Stranger**
  - Um método de teste que nem ao menos pertence ao Teste Unitário que ele está inserido. O método está realmente testando um objeto separado e independente, normalmente um objeto utilizado pelo objeto que sofre o teste.

- **The Operating System Evangelist**
  - Um teste unitário que está ajustado apenas para um determinado sistema operacional para que possa funcionar. Um bom exemplo seria um caso de teste que utilize o separador de linhas do Windows para um assert, que falha apenas rodando em Linux.

- **Success Against All Odds**
  - Um teste escrito para passar antes mesmo de falhar. Como um infeliz efeito colateral, o caso de teste acaba sempre passando mesmo que tenha sido feito para falhar.

- **The Free Ride**
  - Ao invés de escrever um novo teste para uma nova funcionalidade ou característica, apenas um novo assert é criado ao final de um teste já existente.

- **The One**
  - Uma combinação de alguns outros padrões, particularmente o TheFreeRide e TheGiant. Um teste unitário que contém apenas um único metodo que teste todo tipo de funcionalidade que um objeto pode conter. Um indicador comum é que o teste possui o mesmo nome da classe, e ainda com múltiplas linhas, setups e asserts

- **The Peeping Tom**
  - Um teste que, compartilhando recursos, pode ver o resultado de outro test, e pode falhar mesmo que o sistema testado esteja em perfeito funcionamento. Verificado na ferramenta Fitnesse, onde a utilização de variáveis estáticas para abrigar coleções não eram corretamente limpas após a execução do teste, podendo surgir erros durante a execução de qualquer teste. Também conhecido com TheUninvitedGuests.

- **The Slow Poke**
  - Um teste unitário que é incrivelmente lento para ser executado. Quando o teste é iniciado, os programadores podem ir ao banheiro, fumar um cigarro ou pior ainda, inicar o teste no final do dia e ir para casa, esperando que o resultado saia no dia seguinte.


