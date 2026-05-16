# SyncNode Claude Code Skill

A [Claude Code skill](https://docs.claude.com/en/docs/agents/skills) for building apps with [SyncNode](https://syncnode.ai) — a unified AI API gateway that fronts Replicate, OpenAI, OpenRouter, FAL, and Alibaba DashScope behind a single billing and auth surface.

## What this skill does

When you're using Claude Code and ask things like:

- *"Add image generation to my app via SyncNode"*
- *"Use SyncNode to wire up chat completions"*
- *"Help me integrate SyncNode's FAL endpoint"*
- *"Build a content moderation flow using SyncNode"*

Claude will load this skill and know:

- The full endpoint surface (`/generate`, `/chat-completion`, `/fal/generate`, `/alibaba/generate`, `/face-swap/run`, `/moderate`)
- Auth pattern (API key + Bearer JWT)
- Polling lifecycle for async jobs
- Cost-per-call so it can warn before burning your balance
- Code samples in cURL, JavaScript, and Python
- Common errors and how to fix them

## Install

### Option 1 — clone into your skills directory

```bash
git clone https://github.com/syncnode-ai/syncnode-skill.git ~/.claude/skills/syncnode
```

Restart Claude Code. The skill auto-loads when its trigger description matches your prompt.

### Option 2 — install per-project

Drop the `SKILL.md` (and `examples/`) into `.claude/skills/syncnode/` inside your project. The skill will be available to anyone using Claude Code in that repo.

## Verify it's working

In Claude Code, type:

```
/skills
```

`syncnode` should appear in the list. Then try:

```
Set me up to use SyncNode for image generation
```

Claude should walk you through getting an API key, adding a Replicate provider credential, and scaffolding a working `/generate` call.

## What's in this repo

```
SKILL.md          # The skill itself — Claude reads this
README.md         # This file
examples/
  curl.sh         # Every endpoint as a cURL command
  syncnode.js     # Minimal Node.js client using native fetch
  syncnode.py     # Minimal Python client using requests
```

## Pricing (for reference)

| Endpoint | Cost per call |
|---|---|
| `/chat-completion` (OpenRouter) | $0.02 |
| `/chatgpt-completion` (OpenAI) | $0.02 |
| `/generate` (Replicate image/video) | $0.02 |
| `/fal/generate` (FAL) | $0.02 |
| `/alibaba/generate` (Alibaba DashScope) | $0.02 |
| `/face-swap/run` | $0.02 |
| `/moderate` (content moderation) | $0.005 |

New SyncNode accounts start with $5.00 free credit.

## Updating the skill

API changes go in two places:

1. The endpoint reference inside `SKILL.md`
2. The example files in `examples/`

The skill description (frontmatter) controls when Claude invokes it — change with care, since wording affects trigger accuracy.

## License

MIT
