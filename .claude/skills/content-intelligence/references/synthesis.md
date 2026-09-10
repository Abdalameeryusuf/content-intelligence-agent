# Synthesis and research

## 1. When to synthesize

After a processing run, update **only** the topics the new insights touch. Do not
regenerate all synthesis — it is expensive and it destroys stable analysis that was
correct.

## 2. A topic file

Path: `synthesis/topics/<topic-slug>.md`

```markdown
---
topic: audience-building
updated: 2026-09-10
insight_count: 14
creators: [kallaway, ali-abdaal, alex-hormozi]
---

## Where they agree
Each point cites the insight IDs behind it. A point with one ID is not agreement.

## Where they disagree
The actual dispute, with IDs on each side, and what the disagreement turns on.

## What has evidence behind it
Which positions rest on numbers or outcomes, and which are assertion.

## Gaps
What none of them address. Explicitly.

## Agent synthesis
The agent's reading. Below the fence, clearly its own.
```

**Never write a synthesis point without citing IDs.** An uncited synthesis cannot be
verified, cannot be refreshed, and rots invisibly.

## 3. Craft library

Path: `synthesis/craft/<group-slug>.md`

**Groups PATTERN and CRAFT-INSIGHT files by theme.** It does not restate them — it
indexes them and reports what holds across the group.

Since PATTERN files became a first-class type, the craft library's job narrowed: the
per-pattern detail (instances, span, failure conditions) lives in
`creators/<slug>/patterns/`, and the library reports what is true *across* patterns.

Each entry cites the pattern or insight ID and its `generalization`. A library entry
must never state something more strongly than the underlying file does — if every
underlying pattern is `within-creator`, the library entry is too.

**Performance is not endorsement.** Cite `performance_tier` spans to show a pattern is
a habit rather than a response to a hit. Never cite view counts to argue a pattern
works — see `schemas.md` §5. A high-view instance from a creator with a large existing
audience says more about the audience than the pattern.

## 4. Current research

Path: `research/<YYYY-MM-DD>--<topic-slug>.md`

```markdown
---
date: 2026-09-10
topic: waitlist-conversion
queries: ["..."]
source_quality: mixed
supersedes_research: null
---

## What I searched
## Findings
Each with a source URL and a publication date.

## Source assessment
Which of these are primary, which are content marketing, which are unverifiable.

## Contradicts / updates
Links to earlier research files and to creator insights this bears on.
**Contradicting a creator insight does not modify that insight.**

## Agent notes
```

Rules:
- New research on an old topic is a **new dated file**. Never edit an old one.
- Recency is not authority. State which claim rests on what.
- Flag findings older than ~90 days as potentially stale on retrieval.
- Research is triggered by a question that genuinely turns on current fact.

## 5. Disagreements and evolution

`synthesis/disagreements.md` and `synthesis/evolution.md` are **indexes**, not stores.

- A disagreement entry: the proposition, the IDs on each side, what it turns on, and
  whether it is live or resolved.
- An evolution entry: the creator, the supersede-chain of IDs in order, and what
  changed between them.

Both are derived. If the underlying insights change, these are regenerated from them,
never patched in place.

## 6. Honest synthesis

- **Do not manufacture consensus.** Loosely similar statements in different contexts
  are not a shared principle. Say that.
- **Absence is a finding.** Report it.
- **Do not adjudicate by follower count.** Evidence decides, and where there is no
  evidence, say there is none on either side.
- **A creator being wrong is reportable.** Tracking someone is not endorsing them.
- **Check `attribution.role` before crediting anyone.** A guest's claim on a tracked
  creator's channel is the guest's. Synthesis that says "Kallaway believes X" when
  `claimed_by` is a guest is a misattribution defect, not a wording slip.
- **Check `commercial.status` before treating a recommendation as sincere.** A
  recommendation inside `promotional` content is weak evidence of what the creator
  actually thinks, and must be labeled when cited.
- **Check `generalization` before generalizing.** A `within-creator` pattern supports
  "this is how Kallaway works," never "this is how content works."
- **Never let a synthesis claim outrun its sources.** If the underlying files say
  `evidence_strength: none`, the synthesis says so too.
- **An insight with `attribution.role: unknown` is not usable** until resolved.
