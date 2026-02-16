---
title: Genomes
description: Cognitive blueprints that define what a creature can do — not what it will do.
order: 3
---

## What Is a Genome?

A genome is a cognitive blueprint. When you spawn a creature, its genome is copied into the container — it defines the **structure** of the creature's mind (what tabs appear, what tools exist, how validation works) but not its **behavior**. Two creatures with the same genome and different purposes will act completely differently.

Genomes are self-contained directories. They include source code, a `genome.json` manifest, and everything the creature needs to boot. No orchestrator-specific dependencies.

## genome.json Reference

Every genome has a `genome.json` at its root:

| Field | Type | Description |
|---|---|---|
| `name` | string | Genome identifier (e.g. `"dreamer"`) |
| `version` | string | Semver version |
| `description` | string | One-line summary |
| `author` | string | Who wrote it |
| `license` | string | License identifier (e.g. `"MIT"`) |
| `tags` | string[] | Categorization tags |
| `validate` | string | Command to validate the creature's code before boot (e.g. `"npx tsx --check src/mind.ts src/index.ts"`) |
| `tabs` | Tab[] | What shows in the dashboard |

### Tabs

Each tab is an object:

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique identifier |
| `label` | string | Display name in the dashboard |
| `file` | string | Path to the file inside the creature's workspace |
| `type` | string | `markdown`, `text`, or `jsonl` |
| `limit` | number? | Optional — max lines to display (useful for logs) |

## Built-in Genomes

### dreamer (default)

Full cognitive architecture. Creatures with this genome can dream, consolidate memories, self-evaluate, manage fatigue, browse the web with a persistent browser session, and maintain evolving rules about their world.

**Tabs:** purpose, diary, observations, rules, dreams, self-eval

Use this when you want a creature that learns and adapts over time.

### minimal

Bare-bones loop — bash and sleep. No memory, no dreams, no self-evaluation. The creature discovers everything on its own from a blank slate.

**Tabs:** purpose

Use this when you want to see what emerges without any cognitive scaffolding, or as a starting point for a custom genome.

## Creating Your Own

1. Fork an existing genome directory
2. Edit `genome.json` — change the name, tabs, validation command
3. Modify the source code to add or remove cognitive features
4. Spawn a creature with `--genome your-genome-name`

Genomes have no dependency on the orchestrator. Everything the creature needs lives inside the genome directory.
