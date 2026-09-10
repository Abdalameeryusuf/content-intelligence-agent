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

Path: `synthesis/craft/<pattern-slug>.md`

Groups CRAFT insights into reusable patterns. Each pattern records: the structure,
the instances (with IDs and performance figures at capture), conditions for working,
conditions for failing, and whether it transfers to a technical-product audience.

The performance figures are evidence, not endorsement — a pattern that performed once
is not a validated pattern, and a high-view instance from a creator with a large
existing audience says less about the pattern than about the audience.

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
