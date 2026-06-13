---
title: Obtendo as Properties pela ordem de declaração no C#
date: '2009-08-18T18:07:25Z'
categories:
- .Net
tags:
- .Net
- C#
- metadata
- reflection
---

Em alguns momentos, pode ser necessário obter a lista de properties de um objeto. Um jeito simples de fazer isso é:

```csharp
private IEnumerable<PropertyInfo> GetProperties(Type type)
{
    return type.GetProperties();
}
```

O problema é que, segundo a Microsoft, a ordem em que as properties são retornadas não é garantido:

> The GetProperties method does not return properties in a particular order, such as alphabetical or declaration order. Your code must not depend on the order in which properties are returned, because that order varies.

Uma solução para resolver esse problema é ordenar a lista de properties pela property MetadataToken.

O código então, ficaria assim:

```csharp
private IEnumerable<PropertyInfo> GetProperties(Type type)
{
    return type.GetProperties().OrderBy(p => p.MetadataToken);
}
```

Se a intenção for obter as properties na ordem inversa, o código ficaria assim:

```csharp
private IEnumerable<PropertyInfo> GetPropertiesDescending(Type type)
{
    return type.GetProperties().OrderByDescending(p => p.MetadataToken);
}
```

O ideal é que o seu código não dependa da ordem dos membros para executar, mas em alguns casos, como geração automática de código, isso pode ser útil.
