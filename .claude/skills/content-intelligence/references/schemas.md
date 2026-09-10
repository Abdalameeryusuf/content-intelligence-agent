# Schemas

## Insight file

Path: `creators/<creator-slug>/insights/<short-slug>--<nnn>.md`

### Frontmatter — all lanes

```yaml
---
id: kallaway--hook-cold-open--001   # <creator>--<slug>--<nnn>, globally unique
creator: kallaway                    # must match _registry.yaml
lane: CRAFT                          # CLAIM | CRAFT | CASE
type: hook                           # see vocabulary below, must match lane
topics: [hooks, retention]           # MUST exist in _meta/topics.yaml
confidence: high                     # how CLEARLY it was stated/demonstrated
stance: strong                       # how strongly held (CLAIM only; else null)
source:
  video_id: R1bn__sNAaM
  title: "Christopher Nolan wanted to drop a real bomb to film Oppenheimer"
  duration: "1:00"
  views_at_capture: "8.6M"
  timestamps: ["0:00", "0:12"]
captured: 2026-09-10
supersedes: null                     # id of an insight this replaces
related: []                          # ids in other creators, for synthesis
---
```

**`confidence` is not truth.** It records how clearly the creator stated or
demonstrated the thing. A confidently asserted, evidence-free claim is
`confidence: high` with weak evidence in the body. Keeping these axes separate is what
lets synthesis distinguish "widely believed" from "actually supported."

**`views_at_capture`** is recorded for CRAFT insights because performance is part of
the evidence for whether a technique worked. It is a snapshot, not a live figure, and
must never be presented as current.

### Type vocabulary, by lane

| Lane | Valid `type` |
|---|---|
| CLAIM | `principle`, `framework`, `concept`, `opinion`, `prediction`, `strategy` |
| CRAFT | `hook`, `format`, `structure`, `technique`, `pacing` |
| CASE | `case-study`, `launch`, `experiment` |

### Body — CLAIM lane

```markdown
## Claim
> "direct quote" — attributed, with timestamp

## Their reasoning
The argument they actually made. Paraphrase, not quote-collage.

## Evidence they offered
What they cited: their own numbers, an anecdote, third-party data, or nothing.
"Nothing" is a valid and important entry.

## Scope / conditions
Where they say it applies and where they say it doesn't. Omit if they gave none —
and note that they gave none.

## Agent notes
Everything below this heading is the agent's analysis, not the creator's.
```

### Body — CRAFT lane

```markdown
## The pattern
What is actually being done, described so it could be reproduced without imitating
the wording. Structural, not verbatim.

## As executed here
The specific instance, with timestamps. One example, concretely.

## Why it works
Mechanism, not admiration. What does it do to the viewer's attention?

## Where it fails
Conditions under which this backfires or does not transfer. Required, not optional —
a pattern with no stated failure mode has not been understood.

## Transfer to Lifepal
Whether and how this could serve a technical-product audience. "Does not transfer"
is a valid and useful answer.

## Agent notes
```

### Body — CASE lane

```markdown
## What they built
## Decisions they made
Named decisions and the stated reasoning, not a chronology.

## Outcome
What actually happened, with numbers where given. Note when numbers are absent.

## What transfers
## Agent notes
```

**The `## Agent notes` fence is structural.** Everything above it is sourced to the
creator. Everything below is the agent's. This is checkable, which is the point.

---

## `_registry.yaml`

```yaml
creators:
  - slug: kallaway
    name: Kallaway
    handle: "@kallaway"
    channel_id: UCnl8_0CEX3mRPMeg4_xEF9w
    primary_lane: CRAFT
    secondary_lanes: [CLAIM, CASE]
    why_tracked: One sentence. What this creator is for.
    catalog_size: 323
    status: pilot        # pilot | active | paused
```

---

## `_meta/ledger.json`

Machine-owned. Never hand-edited.

```json
{
  "version": 1,
  "runs": [
    {
      "date": "2026-09-10",
      "creator": "kallaway",
      "videos_processed": 20,
      "insights_created": 41,
      "credits_spent_estimate": 24,
      "note": "pilot"
    }
  ],
  "processed_videos": {
    "R1bn__sNAaM": {
      "creator": "kallaway",
      "date": "2026-09-10",
      "insights": 2,
      "lanes": ["CRAFT"]
    }
  }
}
```

`processed_videos` is the idempotency key. A video ID present here is never
re-fetched, which is what makes "process only new material" real rather than aspirational.
