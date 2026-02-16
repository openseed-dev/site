---
title: CLI Reference
description: Every command and flag for managing creatures.
order: 5
section: core
---

## Commands

### seed up

Start the orchestrator and dashboard.

```bash
seed up [--port 7770]
```

| Flag | Default | Description |
|---|---|---|
| `--port` | `7770` | Port for the dashboard |

### seed spawn

Create a new creature.

```bash
seed spawn <name> [options]
```

| Flag | Default | Description |
|---|---|---|
| `--purpose "..."` | — | What the creature should do |
| `--genome` | `dreamer` | Cognitive genome (`dreamer` or `minimal`) |
| `--model` | `claude-opus-4-6` | LLM model to use |

### seed start

Start a stopped creature.

```bash
seed start <name> [--manual]
```

Pass `--manual` to start in manual mode — the creature waits for messages instead of thinking autonomously.

### seed stop

Stop a running creature. State is preserved.

```bash
seed stop <name>
```

### seed list

List all creatures and their current status.

```bash
seed list
```

### seed fork

Fork a creature with its full history into a new creature.

```bash
seed fork <source> <name>
```

### seed destroy

Permanently remove a creature and all its data.

```bash
seed destroy <name>
```

## pnpm Equivalents

If running natively (not via Docker), use `pnpm` instead of `seed`:

| seed | pnpm |
|---|---|
| `seed up` | `pnpm up` |
| `seed spawn alpha --purpose "..."` | `pnpm spawn alpha -- --purpose "..."` |
| `seed start alpha` | `pnpm start alpha` |
| `seed stop alpha` | `pnpm stop alpha` |
| `seed list` | `pnpm list-creatures` |
| `seed fork alpha beta` | `pnpm fork alpha beta` |
| `seed destroy alpha` | `pnpm destroy alpha` |

Note the `--` separator before flags when using `pnpm spawn`.
