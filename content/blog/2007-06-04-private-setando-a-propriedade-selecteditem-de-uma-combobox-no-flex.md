---
title: Setando a propriedade selectedItem de uma ComboBox no Flex
date: '2007-06-04T16:26:40Z'
categories:
- ActionScript
- Flex
- RIA
aliases:
- /2007/06/04/private-setando-a-propriedade-selecteditem-de-uma-combobox-no-flex/
---

Fala pessoal, Estava fazendo um código para seleciononar automaticamente uma combo box em função do registro selecionado no data grid do flex.

O método recebe dois parâmetros: A combo box e o ID do registro selecionado.

O método segue abaixo:

```
public static function SelectComboBox(comboBox: ComboBox, 
	id: int): void {

    var dataProvider: ArrayCollection = 
	ArrayCollection(comboBox.dataProvider);

    var selectedIndex: int = 0;

    for (var i:int = 0; i < dataProvider.length; i++) {
        if (dataProvider[i].id == id) {
            selectedIndex = i;
            break;
        }
    }
    comboBox.selectedIndex = i;
} 
```
