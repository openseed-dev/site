---
title: Getting Started
description: Install OpenSeed, spawn your first creature, and watch it think.
order: 1
---

## Prerequisites

You need [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running. That's it.

## Quick Start (Docker Compose)

```bash
git clone https://github.com/openseed-dev/openseed.git
cd openseed
cp .env.example .env
```

Open `.env` and add your API key(s) — at minimum, set `ANTHROPIC_API_KEY` or `OPENAI_API_KEY`.

```bash
docker compose up
```

Open [http://localhost:7770](http://localhost:7770), click **+** to spawn a creature, and watch it think.

## Native Install (Alternative)

If you prefer running outside Docker:

**Requirements:** Node.js 18+, pnpm, Docker (still needed for creature containers)

```bash
git clone https://github.com/openseed-dev/openseed.git
cd openseed
pnpm install
export ANTHROPIC_API_KEY=sk-ant-...
pnpm up
```

Open [http://localhost:7770](http://localhost:7770).

## Spawning from CLI

```bash
pnpm spawn alpha -- --purpose "explore the world and build useful things"
```

This creates a creature named `alpha` with the given purpose. The name is arbitrary — pick whatever you want.

## What Happens Next

When a creature spawns, it:

1. Boots inside its own Docker container
2. Reads its `PURPOSE.md` to understand what it should do
3. Starts thinking — calling tools, making decisions, sleeping when idle

The dashboard at [http://localhost:7770](http://localhost:7770) shows thoughts, tool calls, and sleep cycles in real time. Send messages to a creature with **Cmd+Enter** (or **Ctrl+Enter**).

## Choosing a Model

| Model | Provider | Input / Output per MTok |
|---|---|---|
| claude-opus-4-6 | Anthropic | $5 / $25 |
| claude-sonnet-4-5 | Anthropic | $3 / $15 |
| claude-haiku-4-5 | Anthropic | $1 / $5 |
| gpt-5.2 | OpenAI | $1.75 / $14 |
| gpt-5-mini | OpenAI | $0.25 / $2 |
| o4-mini | OpenAI | $1.10 / $4.40 |

Set the model at spawn time with `--model`:

```bash
pnpm spawn alpha -- --purpose "build things" --model claude-sonnet-4-5
```

Or select a model from the dropdown in the dashboard when spawning via the UI.
