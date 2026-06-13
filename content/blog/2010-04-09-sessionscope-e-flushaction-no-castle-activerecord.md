---
title: SessionScope e FlushAction no Castle ActiveRecord
date: '2010-04-09T00:21:51Z'
categories:
- .Net
- C#
tags:
- .Net
- activerecord
- C#
- castle
- cshap
- dotnet
- flush
- flushaction
- hibernate
- nhibernate
- orm
- persistence
---

O Castle ActiveRecord é uma implementação do padrão homônimo feita em cima nHibernate. Um ORM bastante conhecido no mundo Java. Apesar de alguns comportamentos serem realizados pelo nHibernate, estarei aqui citando o ActiveRecord como responsável por tais comportamentos.

Um problema muito comum que eu costumo me deparar, é com a utilização de lazy loading no ActiveRecord.

Geralmente na utilização de lazy loading em aplicações web, é utilizado o padrão Session per Request para o SessionScope. Só que por padrão, o ActiveRecord persiste automaticamente (em algumas situações) as entidades, mesmo que seus métodos Save ou Update não tenham sido invocados. Isso costuma gerar uma série de problemas, como por exemplo, entidades com o seu estado interno inválido sendo persistido.

Para resolver esse problema, deve ser especificado o FlushAction como Never:

```csharp
SessionScope session = new SessionScope(FlushAction.Never);
```

Assim, o ActiveRecord não irá mais persistir automaticamente as entidades. Em contrapartida, mesmo invocando os métodos Save ou Update as entidades não serão persistidas. Para que isso ocorra, será necessário utilizar os métodos SaveAndFlush e UpdateAndFlush, respectivamente, ou utilizar o método Flush da instância do SessionScope.
