# Repodify AI Skill

This repository contains the official AI Skill and custom instructions for [Repodify](https://repodify.app). 

By providing this skill to your AI agent (like Claude, Cursor, Antigravity, or Devin), you teach it exactly how to natively build, curate, edit, and manage podcast RSS feeds autonomously using the Repodify MCP server.

## Installation

You can install this skill natively across various AI agents:

### Antigravity
Install the skill globally so Antigravity always knows how to use Repodify:
```bash
agy skill install https://github.com/jonroig/repodify-ai-skill
```

### Devin
```bash
devin plugins install jonroig/repodify-ai-skill
```

### Cursor & Windsurf
The repository contains a `.cursorrules` and `.windsurfrules` file in the root directory. If you are building an app that integrates with Repodify, simply clone this repository or copy those files into the root of your own project.

### ChatGPT (Custom GPT)
Create a new Custom GPT and paste the contents of `.agents/skills/repodify/SKILL.md` into the **Instructions** box.

### Claude Projects
When creating a Claude Project, paste the contents of `.agents/skills/repodify/SKILL.md` into the **Custom Instructions** field.
