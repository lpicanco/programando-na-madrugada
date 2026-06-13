---
title: Removendo a acentuação e os caracteres especiais de uma String
date: '2010-05-28T10:56:37Z'
categories:
- .Net
- C#
tags:
- .Net
- algoritmo
- C#
---

Estava precisando remover a acentuação e os caracteres especiais do nome de um arquivo. Para isso, desenvolvi um extension method para a classe String.

Exemplo:  
String de entrada:  
**Adobe Acrobat - Pacy-Paraná\_05.12\_áèïôúã+.pdf**

String de retorno:  
**AdobeAcrobatPacyParana\_05.12\_aeioua.pdf**

Desenvolvi o método utilizando uma HashTable e expressão regular. Caso você tenha alguma sugestão de melhoria, poste aí nos comentários.

Extension method:

```csharp
public static String RemoveSpecialCharacters(this String self)
{
	var normalizedString = self;

	// Prepara a tabela de símbolos.
	var symbolTable = new Dictionary<char, char[]>();
	symbolTable.Add('a', new char[] {' ', 'á', 'ä', 'â', 'ã'});
	symbolTable.Add('c', new char[] { 'ç' });
	symbolTable.Add('e', new char[] { 'è', 'é', 'ë', 'ê' });
	symbolTable.Add('i', new char[] { 'ì', 'í', 'ï', 'î' });
	symbolTable.Add('o', new char[] { 'ò', 'ó', 'ö', 'ô', 'õ' });
	symbolTable.Add('u', new char[] { 'ù', 'ú', 'ü', 'û' });

	// Substitui os símbolos.
	foreach (var key in symbolTable.Keys)
	{
		foreach (var symbol in symbolTable[key])
		{
			normalizedString = normalizedString.Replace(symbol, key);
		}
	}
			
	// Remove os outros caracteres especiais.
	normalizedString = Regex.Replace(normalizedString, "[^0-9a-zA-Z._]+?", "");
	return normalizedString;
}
```
