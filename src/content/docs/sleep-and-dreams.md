---
title: Sleep and Dreams
description: How creatures consolidate experience, reflect, and maintain long-term memory.
order: 7
section: dreamer
---

## Memory Tiers

Creatures (dreamer genome) operate with three layers of memory:

1. **In-context**: the rolling LLM conversation window, ~20 recent messages. This is working memory.
2. **Observations**: prioritized notes in `.self/observations.md`, tagged RED/YLW/GRN by importance. Injected into context on wake-up.
3. **Total recall**: every message ever sent, appended to `.self/conversation.jsonl`. Searchable with `rg` from the creature's bash tool. Never trimmed.

In-context memory is fast but small. Observations are curated. Total recall is complete but requires explicit search.

## Fatigue

Each tool call increments an action counter. This prevents creatures from burning tokens in runaway loops.

- At **60 actions** (FATIGUE_WARNING), the creature receives a system message suggesting sleep.
- At **80 actions** (FATIGUE_LIMIT), consolidation is forced. The creature sleeps whether it wants to or not.

The counter resets after consolidation.

## Voluntary Sleep

Creatures can call the `set_sleep` tool with a duration in seconds. Short naps (under 30s) are just pauses, no consolidation runs. Sleeps of 30+ seconds trigger consolidation, provided the last dream was at least 10 minutes ago.

## Consolidation (Dreaming)

When consolidation triggers, a separate LLM call reviews the creature's recent conversation and produces:

- **Observations**: key facts, patterns, and learnings, priority-tagged. Merged into `.self/observations.md`.
- **Reflection**: a narrative summary of what happened and what matters. This is the "dream."

The dream is saved to `.self/dreams.jsonl`. Old messages beyond the keep window are trimmed from context.

## Deep Sleep

Every 10th dream triggers deep sleep, a more thorough consolidation:

- Prunes stale observations from `.self/observations.md`
- Rewrites priority tags based on current relevance
- Writes a diary entry summarizing the cycle
- Forces a 300-second pause

Deep sleep is where long-term memory gets maintained. Without it, observations accumulate noise.

## Wake-Up

On wake, the creature's context is rebuilt with:

- The last dream's reflection
- Current priority observations
- Pointers to `.self/conversation.jsonl` and `.self/dreams.jsonl` for full history access

This gives the creature continuity across sleep cycles without loading the entire history into context.

## Tuning Constants

| Constant | Default | What it controls |
|---|---|---|
| FATIGUE_WARNING | 60 | Actions before tiredness warning |
| FATIGUE_LIMIT | 80 | Actions before forced consolidation |
| MIN_DREAM_INTERVAL_MS | 10 min | Minimum time between dreams |
| QUICK_NAP_THRESHOLD | 30s | Sleeps shorter than this skip consolidation |
| DEEP_SLEEP_EVERY | 10 | Dreams between deep sleep cycles |
| DEEP_SLEEP_PAUSE | 300s | Forced pause during deep sleep |
| KEEP_RECENT_MESSAGES | 20 | Messages kept after context trim |
| MAX_CONTEXT_CHARS | 100K | Emergency overflow threshold |