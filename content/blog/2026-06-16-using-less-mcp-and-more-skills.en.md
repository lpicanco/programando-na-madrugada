---
title: Using less MCP and more skills to save context
date: '2026-06-16T17:50:00Z'
categories:
- Reflection
tags:
- llm
- claude
- mcp
- skills
- context
---

When MCPs (Model Context Protocol) started showing up, the first thing I did was set up a bunch of them. One for GitHub, one for postgres, others to connect to a few APIs, and so on. Then I noticed something annoying: the context window was already full before I even started anything.

A long while later, [Skills](https://agentskills.io/) came along, a more standardized and cheaper way to give agents new features and extra context, with the upside of progressive disclosure, meaning you don't dump every available tool into the context at once.

**The problem with MCP**

Every MCP server you connect injects the schema of all its tools into the context, right at startup. It doesn't matter if you're going to use one tool or none, the description of all of them is already there taking up space. With three or four servers, that's thousands of tokens spent before the first message.

And context isn't free. The more clutter at the start, the less room there is for what matters, and the model also gets slower and more expensive. There's also a subtler side effect: with dozens of similar tools hanging around, the model makes more mistakes picking which one to call.

**What Skills are**

A skill is basically a directory with a `SKILL.md` (which has a `name` and a `description` in the frontmatter) and the support files it needs. While the skill isn't used, only the description stays in the context. The full content is loaded on demand, when the topic comes up.

```text
.claude/skills/
└── confluence/
    ├── SKILL.md      # only the description stays in the context until it's used
    ├── auth.py       # the script runs as a process, the code doesn't enter the context
    ├── fetch-page.py
    └── search.py
```

The `SKILL.md` is short and points to the script:

```markdown
---
name: confluence
description: Set of tools to interact with Atlassian Confluence. Use when the user or agent needs to read, search or update Confluence pages.
---

# Confluence

The scripts read the credentials from `CONFLUENCE_BASE_URL` and `CONFLUENCE_TOKEN`.
Always run `python auth.py` first to validate the session before any
other operation.

## Fetch a page
Run `python fetch-page.py <page-id>`. The output is the content in Markdown,
with the Confluence macros already converted.

## Search pages
Run `python search.py "<text>"` for a CQL search. Returns up to 20
results as a list of `page-id` and title.

## Conventions
- Page IDs are numeric. If the user passes a URL, extract the ID from
  the `/pages/<page-id>/` part.
- To update a page, always fetch the current version first: Confluence
  requires the version number on the update and rejects stale writes.
```

It's two savings in one. The first is the documentation: that API reference and those conventions you used to have to feed the agent by hand now live inside the skill, and they only enter the context when they're needed.

The second is the scripts: instead of the model making eight tool calls to put together one operation, it runs a script that does it all at once. The script's code runs as a separate process and never enters the context, and the result is predictable because it's real code, not the model improvising step by step.

**When MCP still makes sense**

MCP is still very useful. Mostly when the interaction is live and goes both ways: poking around a database to explore it, or grabbing the current state of an API that changes all the time. In those cases you don't know ahead of time which calls you'll need, and having the tools on hand is worth the context cost.

The rule I adopted is this: if the task is deterministic and you can describe it as a script with good documentation, it becomes a skill. If I need a live, stateful conversation against an external system, then I reach for MCP.

Today my workflow is the opposite of what it used to be. I start by asking whether it fits in a skill with a script and some extra documentation, and I only fall back to MCP when I need something live and more interactive.

My context thanks me.
