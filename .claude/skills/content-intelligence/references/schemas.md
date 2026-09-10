# Schemas

**Revision 2** (2026-09-10) — supersedes the pilot schema. Changes are recorded in
`_meta/decisions.md`. All controlled values live in `_meta/vocabularies.yaml`; this
file explains how to use them.

There are **two knowledge types**, not one:

| Type | Sources | Directory |
|---|---|---|
| **INSIGHT** | Exactly one video | `creators/<slug>/insights/` |
| **PATTERN** | Two or more instances | `creators/<slug>/patterns/` |

A PATTERN is not an insight with extra citations. It is a different claim — *this
recurs* — and it is only supportable across instances.

---

## 1. The six epistemic categories

Everything in this knowledge base is one of six things. They must never be blurred,
in frontmatter, in bodies, or in answers to the user.

| Category | Label | What it is | Who is accountable |
|---|---|---|---|
| **Source evidence** | `[SOURCE]` | Verbatim quotes, transcript timestamps, figures stated on screen | The recording |
| **Creator/guest claim** | `[CLAIM]` | An assertion by a named person, attributed | The named person |
| **Observed pattern** | `[PATTERN]` | A recurring construction, observed across instances | Us — an observation |
| **Agent inference** | `[INFERENCE]` | Our reasoning from the above | Us |
| **Agent recommendation** | `[RECOMMENDATION]` | What we think should be done | Us |
| **Performance data** | `[PERFORMANCE]` | View counts and metrics, at capture time | The platform, at a moment |

Three distinctions carry most of the weight:

- **`[SOURCE]` vs `[CLAIM]`.** That a creator *said* something is source evidence. That
  the thing they said is *true* is not established by their saying it.
- **`[CLAIM]` vs `[PATTERN]`.** A claim is asserted by a person. A pattern is observed
  by us in how content is built — creators usually do not state their patterns, and
  attributing an observed pattern to a creator as though they taught it is a
  misattribution.
- **`[PERFORMANCE]` vs everything else.** Performance is never evidence for the other
  five. See §5.

### The fence rule is lane-aware

A single "everything above `## Agent notes` is sourced" rule works for CLAIM and CASE,
where the sections above genuinely are the creator's words. **It does not work for
CRAFT and PATTERN**, and assuming it did was a defect caught by validation.

In a CRAFT or PATTERN file, most of the body is *ours*: naming a pattern, explaining
why it works, and stating where it fails are all agent analysis of an observed
construction. The creator supplied the construction, not the analysis. Treating those
sections as "sourced" would credit the creator with reasoning they never did — the same
misattribution the `[CLAIM]`/`[PATTERN]` distinction exists to prevent.

| Lane | Source-only sections | Everything else |
|---|---|---|
| **CLAIM** | `## Claim`, `## Their reasoning`, `## Evidence they offered`, `## Scope / conditions` | `## Agent notes` — agent only |
| **CASE** | `## What they built`, `## Decisions they made`, `## Outcome` | `## What transfers`, `## Agent notes` — agent |
| **CRAFT** | `## As executed here` | **All other sections are agent-authored** |
| **PATTERN** | `## Instances` | **All other sections are agent-authored** |

Rules the validator enforces:

- **Source-only sections may never contain `[INFERENCE]` or `[RECOMMENDATION]`.**
- **Quote-bearing sections must carry inline timestamps** (`## Claim`, `## As executed
  here`, `## Instances`) — they are the path back to the tape. Paraphrase sections
  (`## Their reasoning`) and may-be-empty sections (`## Scope / conditions`) do not.
- **`## Agent notes` is required in every file**, even when other sections are already
  agent-authored, because it is where cross-file reasoning and caveats live.
- In CRAFT and PATTERN files, `[INFERENCE]` and `[RECOMMENDATION]` are expected outside
  the source section and are not errors.

The practical consequence: **a CRAFT insight is mostly the agent's reading of what a
creator did.** The file should read that way, and nothing in it may imply the creator
taught the technique unless `observed_in.stated_by_creator` is `true`.

---

## 2. INSIGHT frontmatter

```yaml
---
id: kallaway--distribution-before-product--001
knowledge_type: INSIGHT
creator: kallaway                    # whose knowledge base this lives in
lane: CLAIM                          # CLAIM | CRAFT | CASE
type: principle                      # must be valid for the lane
topics: [distribution, audience-building]   # must exist in _meta/topics.yaml

attribution:                         # REQUIRED for CLAIM and CASE
  claimed_by: kallaway               # WHO asserted it
  role: self                         # from vocabularies.yaml attribution_roles
  published_by: kallaway             # always the tracked creator
  co_constructed_with: null          # only for host-framed-guest-endorsed

confidence: high                     # how CLEARLY it was stated. NOT truth.
evidence_strength: anecdote          # whether it is SUPPORTED. Separate axis.
stance: strong                       # how strongly held (CLAIM only; else null)

commercial:                          # REQUIRED on every insight
  status: none                       # from vocabularies.yaml commercial_statuses
  basis: null                        # required unless status is `none`

source:
  video_id: 33RYYHqU0OQ
  title: "I'm building a personal holding company"
  duration: "13:37"
  timestamps: ["2:13", "2:18"]

performance:                         # optional; omit rather than guess
  views_at_capture: "3.3K"
  captured: 2026-09-10
  interpretation: sampling-context-only
  confounds: ["Older video; view count reflects channel size at the time, not now"]

captured: 2026-09-10
supersedes: null
related: []
---
```

### The two-axis rule

`confidence` and `evidence_strength` measure different things and must never be
collapsed:

- `confidence: high` + `evidence_strength: none` = **stated forcefully, backed by
  nothing.** This is extremely common and the knowledge base must be able to say so.
- `confidence: medium` + `evidence_strength: external-data` = hedged but supported.

Synthesis distinguishes "widely asserted" from "actually supported" using these two
fields. Collapsing them destroys that.

### Attribution

`attribution` is mandatory for CLAIM and CASE. It is what stops a guest's opinion
becoming the tracked creator's position — a direct violation of SKILL.md §2.

- `claimed_by` is **who asserted it**, not whose channel it appeared on.
- `published_by` is always the tracked creator.
- For `role: guest`, the tracked creator is the publisher and inherits nothing.
- For `role: third-party-reported`, the claim belongs to the absent third party *as
  reported*, and the report is unverified unless the body cites a primary source.
- For `role: host-framed-guest-endorsed`, fill `co_constructed_with`. Use this only
  when the host proposed the framing and the guest accepted it — a guest merely
  answering a question is `role: guest`.

CRAFT insights describe construction rather than assertion, so they omit `attribution`
and use `observed_in` (§4).

### Commercial

Mandatory on every insight, including `status: none`. An absent field is
indistinguishable from an unassessed one, and the whole point is to know which videos
were promotional before synthesis reads their recommendations as sincere.

**`basis` is required for every status except `none`, and must state what was
observed** — a quoted disclosure, or the observable features that make the content
promotional.

> **Do not assert sponsorship without a disclosure.** `promotional` describes the
> content. `disclosed-sponsorship` describes a disclosure. Writing the latter without
> evidence is a factual claim about a real person's undisclosed financial
> relationships. See `_meta/vocabularies.yaml`.

---

## 3. PATTERN frontmatter

For anything observed across two or more instances.

```yaml
---
id: kallaway--mid-roll-rehook--p001
knowledge_type: PATTERN
creator: kallaway
lane: CRAFT
type: technique
topics: [retention, pacing]

instance_count: 7
instances:
  - video_id: R1bn__sNAaM
    timestamp: "0:07"
    note: "'but here's what's crazy'"
    performance_tier: breakout        # see §5
  - video_id: WDhcMbFFeVU
    timestamp: "0:20"
    note: "'but the real question is how'd they do it'"
    performance_tier: mid
  # ... one entry per instance

span:
  eras: [0-49, 100-149, 150-199]      # catalog index bands the instances span
  performance_tiers: [breakout, mid, low]
  commercial_statuses: [none, promotional]

sample_basis: "20 of 323 videos, purposively sampled across eras and tiers"
generalization: within-creator          # within-creator | cross-creator

confidence: high                        # how clearly the pattern is observable
evidence_strength: demonstrated

captured: 2026-09-10
supersedes: null
related: []
---
```

### Rules

- **Minimum two instances.** One instance is an INSIGHT. Do not open a PATTERN file
  and wait for it to fill.
- **`instances` carries structured entries, not a list of strings.** This was the
  pilot's ad-hoc workaround and it is now the schema.
- **`sample_basis` is mandatory.** A pattern found in a purposive 6% sample is not the
  same claim as one found across a full catalog, and the file must say which it is.
- **`generalization: within-creator`** until a second creator shows the same pattern.
  A habit of one creator is not a principle of content.
- **`span` is the honesty field.** It records the diversity the pattern was observed
  across. A pattern seen only in one era and one performance tier is weak, and `span`
  makes that visible instead of leaving it to the reader to reconstruct.

---

## 4. Bodies

### CLAIM lane

```markdown
## Claim
> "direct quote" — attributed to the person in `attribution.claimed_by`, with timestamp

## Their reasoning
The argument they actually made.

## Evidence they offered
What they cited. "Nothing" is a valid and important entry, and must match
`evidence_strength`.

## Scope / conditions
Where they say it applies and doesn't. Note explicitly if they gave none.

## Agent notes
[INFERENCE] / [RECOMMENDATION] only, each labeled.
```

### CRAFT lane (single instance)

```markdown
## The pattern
Stated so it could be reproduced on an unrelated subject. If it cannot, it has been
transcribed rather than extracted.

## As executed here
`observed_in` — the specific instance, with timestamps.

## Why it works
Mechanism, not admiration.

## Where it fails
Required. A pattern with no stated failure conditions has not been understood.

## Transfer to Lifepal
"Does not transfer" is a valid answer.

## Agent notes
```

CRAFT frontmatter replaces `attribution` with:

```yaml
observed_in:
  video_id: rjo5XUtVQSE
  stated_by_creator: false    # did they NAME the technique, or only use it?
```

`stated_by_creator: false` is the normal case and it matters: a creator using a
technique has not taught it, and the knowledge base must not imply they did.

### CASE lane

```markdown
## What they built
## Decisions they made
## Outcome
Numbers where given. Note explicitly when absent or unverifiable.
## What transfers
## Agent notes
```

### PATTERN

```markdown
## The pattern
## Instances
A table: video, timestamp, performance tier, commercial status, what varied.
## What holds across instances
Only what is true of ALL of them.
## What varies
Where instances differ — this is where the conditions live.
## Where it fails
## Transfer to Lifepal
## Limits of this observation
Required. Sample size, era coverage, tier coverage, and what would falsify it.
## Agent notes
```

`## Limits of this observation` is mandatory and is the section that stops a pattern
from a 6% sample being read as a law.

---

## 5. Performance data

Performance is recorded because it describes the sample, and withheld from every
inferential role.

**The problem it creates:** in the pilot, one creator's videos ranged from 3K to 8.6M
views using the same formats. Subject matter and technique are confounded and cannot be
separated by observation. A field that simply sits next to a technique invites the
reader — human or model — to treat it as the technique's result.

**The fix, in three parts:**

1. **`interpretation` is a required field with effectively one legal value**
   (`sampling-context-only`). The alternative, `controlled-comparison`, requires
   `performance.controls` naming what was held constant. Nothing currently qualifies.
2. **`confounds` is required** whenever a figure is unusual — name the competing
   explanation in the file, so it travels with the number.
3. **Tiers, not raw numbers, for pattern reasoning.** Patterns cite
   `performance_tier` (`breakout` | `high` | `mid` | `low`) to show a pattern spans
   tiers. Tiers are relative to the creator's own catalog, never absolute.

**The standing rule:**

> Performance data may be cited to describe what was sampled, or to show a pattern
> appears across performance tiers. It may never be cited as evidence that a technique
> caused a result. If a sentence uses a view count to argue a technique works, it is
> wrong regardless of how it is hedged.

A pattern appearing across breakout *and* low tiers is mildly interesting — it suggests
the pattern is a habit rather than a response to a hit. That is the strongest legal
inference, and it is about the creator, not about effectiveness.

---

## 6. `_registry.yaml`

```yaml
creators:
  - slug: kallaway
    name: Kallaway
    handle: "@kallaway"
    channel_id: UCnl8_0CEX3mRPMeg4_xEF9w
    primary_lane: CRAFT
    secondary_lanes: [CLAIM, CASE]
    why_tracked: One sentence.
    catalog_size: 323
    status: pilot        # pilot | active | paused
```

---

## 7. `_meta/ledger.json`

Machine-owned, never hand-edited.

```json
{
  "version": 2,
  "runs": [ { "date": "...", "creator": "...", "videos_processed": 20,
              "insights_created": 18, "patterns_created": 2 } ],
  "processed_videos": {
    "R1bn__sNAaM": {
      "creator": "kallaway", "date": "2026-09-10",
      "insights": 2, "lanes": ["CRAFT"],
      "commercial_status": "none",
      "contributes_to_patterns": ["kallaway--mid-roll-rehook--p001"]
    }
  },
  "patterns": {
    "kallaway--mid-roll-rehook--p001": { "instance_count": 7, "derived_from": ["..."] }
  },
  "unavailable_videos": { }
}
```

`processed_videos` is the idempotency key. `contributes_to_patterns` lets a video that
produced no standalone insight still show its contribution, so zero-insight videos are
visibly useful rather than looking like wasted spend.
