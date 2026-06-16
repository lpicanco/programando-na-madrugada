---
title: Usando menos MCP e mais skills pra economizar contexto
slug: usando-menos-mcp-e-mais-skills
date: '2026-06-16T17:50:00Z'
categories:
- Reflexão
tags:
- llm
- claude
- mcp
- skills
- contexto
---

Quando os MCPs (Model Context Protocol) começaram a aparecer, a primeira coisa que fiz foi configurar vários deles. Um pro GitHub, um para postgres, outros para conectar em algumas APIs e por aí vai. Aí reparei numa coisa chata: a janela de contexto já começava lotada, antes mesmo de eu começar qualquer coisa.

Depois de um longo tempo, surgiram as [Skills](https://agentskills.io/), uma forma mais padronizada e econômica de prover novas funcionalidades e contexto adicional aos agentes com a vantagem do progressive disclosure, ou seja, sem despejar todas as tools disponíveis de uma vez no contexto.

**O problema com MCP**

Cada servidor MCP que você conecta injeta o schema de todas as ferramentas dele no contexto, logo na inicialização. Não importa se você vai usar uma ferramenta ou nenhuma, a descrição de todas elas já está lá ocupando espaço. Com três ou quatro servidores, são milhares de tokens gastos antes da primeira mensagem.

E contexto não é de graça. Quanto mais entulho no começo, menos espaço sobra pro que importa, e o modelo ainda fica mais lento e mais caro. Tem também um efeito colateral mais sutil: com dezenas de ferramentas parecidas penduradas, o modelo erra mais na hora de escolher qual chamar.

**O que são Skills**

Uma skill é basicamente um diretório com um `SKILL.md` (que tem um `name` e uma `description` no frontmatter) e os arquivos de apoio que ela precisa. Enquanto a skill não é usada, só a descrição fica no contexto. O conteúdo completo é carregado sob demanda, quando o assunto aparece.

```text
.claude/skills/
└── confluence/
    ├── SKILL.md      # só a descrição fica no contexto até ser usada
    ├── auth.py       # o script roda como processo, o código não entra no contexto
    ├── fetch-page.py
    └── search.py
```

O `SKILL.md` é curto e aponta pro script:

```markdown
---
name: confluence
description: Set of tools to interact with Atlassian Confluence. Use when the user or agent needs to read, search or update Confluence pages.
---

# Confluence

Os scripts leem as credenciais de `CONFLUENCE_BASE_URL` e `CONFLUENCE_TOKEN`.
Sempre rode `python auth.py` primeiro para validar a sessão antes de qualquer
outra operação.

## Buscar uma página
Execute `python fetch-page.py <page-id>`. A saída é o conteúdo em Markdown,
já com as macros do Confluence convertidas.

## Pesquisar páginas
Execute `python search.py "<texto>"` para uma busca CQL. Retorna até 20
resultados como uma lista de `page-id` e título.

## Convenções
- IDs de página são numéricos. Se o usuário passar uma URL, extraia o ID do
  trecho `/pages/<page-id>/`.
- Para atualizar uma página, sempre busque a versão atual antes: o Confluence
  exige o número da versão no update e rejeita gravações desatualizadas.
```

São duas economias juntas. A primeira é a documentação: aquela referência de API e as convenções que antes era necessário informar ao agente manualmente ficam guardadas dentro da skill e só entram no contexto quando fazem falta.

A segunda são os scripts: em vez de o modelo fazer oito chamadas de ferramenta pra montar uma operação, ele roda um script que faz tudo de uma vez. O código do script roda como processo separado e nunca entra no contexto, e o resultado é previsível porque é código de verdade, não o modelo improvisando passo a passo.

**Quando MCP ainda faz sentido**

O MCP ainda é muito útil. Principalmente quando a interação é viva e de mão dupla: consultar um banco de forma exploratória ou pegar o estado atual de uma API que muda o tempo todo. Nesses casos você não sabe de antemão quais chamadas vai precisar, e ter as ferramentas à mão compensa o custo de contexto.

A regra que adotei é essa: se a tarefa é determinística e dá pra descrever como um script com uma boa documentação, vira skill. Se eu preciso de uma conversa ao vivo e com estado contra um sistema externo, aí o MCP ganha preferência.

Hoje meu padrão virou o contrário do que era. Começo perguntando se aquilo cabe numa skill com um script e documentação extra, e só caio pro MCP quando preciso de algo vivo e mais interativo.

Meu contexto agradece.
