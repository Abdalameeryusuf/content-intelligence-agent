# Content Intelligence Agent — Knowledge Base

This repository is the persistent memory of a personal content-intelligence agent.
There is no application here. No backend, no database, no pipeline, no scripts.
**Claude is the intelligence layer; this repo is what it remembers.**

Everything here is meant to be read by a human as easily as by a model.

## What lives where

| Path | Holds | Written by |
|---|---|---|
| `.claude/skills/content-intelligence/` | How the agent reasons. **No creator knowledge.** | Human + agent |
| `creators/<slug>/insights/` | Single-video insights | Agent |
| `creators/<slug>/patterns/` | **Cross-video patterns** (2+ instances) | Agent |
| `synthesis/` | Cross-creator analysis derived from `creators/` | Agent |
| `research/` | Dated web findings, append-only | Agent |
| `me/` | Goals, positioning, audience | **Human** |
| `project/` | Lifepal context, as dated snapshots | Human + agent |
| `content/` | Published history, idea backlog, strategy | Both |
| `_meta/` | Ledger, topic + controlled vocabularies, decision log | Agent |

## The load-bearing rules

1. **Insights are atomic.** One idea per file, not one file per video. Anything resting
   on two or more videos is a **PATTERN**, a separate knowledge type in `patterns/`.
2. **Nothing is overwritten.** A changed view *supersedes* an old one; both survive.
3. **Creator statements and agent inference are structurally separated**, not just
   stylistically — via lane-aware source-only sections. Note that a CRAFT file is
   *mostly* agent analysis: the creator supplied the construction, not the reading of it.
4. **Transcripts are never committed.** Insight files carry video IDs and timestamps,
   which is enough to return to the source.
5. **`_meta/ledger.json` is machine-owned.** Do not hand-edit it.
6. **No creator knowledge in the Skill.** Delete `creators/` and the Skill is still valid.
7. **Six epistemic categories, never blurred**: `[SOURCE]`, `[CLAIM]`, `[PATTERN]`,
   `[INFERENCE]`, `[RECOMMENDATION]`, `[PERFORMANCE]`.
8. **Performance data never proves a technique worked.** It describes the sample only.
9. **Controlled values come from `_meta/vocabularies.yaml`.** Never invented per file.

## Entry points

- New here? Read `.claude/skills/content-intelligence/SKILL.md`.
- Want to know what's been processed? `_meta/ledger.json`.
- Want to know why the repo is shaped this way? `_meta/decisions.md`.

## Status

Pilot stage. One creator (Kallaway) partially processed to validate the extraction
schema before scaling. See `_meta/decisions.md` for what is deliberately not built yet.
