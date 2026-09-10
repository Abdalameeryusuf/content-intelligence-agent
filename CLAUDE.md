# Operating context

This repository is a knowledge base, not an application. Do not add a backend,
database, vector store, RAG pipeline, build step, or scripts to it. If a task seems
to need one, stop and say so rather than building it.

**Before doing any content-intelligence work, read
`.claude/skills/content-intelligence/SKILL.md`.** It defines how to retrieve,
extract, synthesize, research, and write. This file only points at it.

## Non-negotiables, repeated here because they are cheap to forget

- Never present agent inference as something a creator said.
- Never overwrite knowledge to reflect a new view; supersede it.
- Never commit raw transcripts.
- Never imitate a creator's voice or phrasing.
- Never optimize for virality.
- Say plainly when the knowledge base does not cover something. Do not fill the
  gap from general training knowledge while appearing to answer from the corpus.

## Repo hygiene

- Commit after each meaningful unit of work (one creator's run, one synthesis pass).
- Log architecture and strategy decisions in `_meta/decisions.md`, append-only.
- Keep infrastructure identifiers (project IDs, uids, env structure) out of this repo.
  They serve no content purpose and belong only in the Lifepal repo.
