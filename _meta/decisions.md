# Decision log

Append-only. Newest at the bottom. Records decisions and the reasoning behind them, so
a later session does not silently re-litigate something that was settled deliberately.

---

## 2026-09-10 — Repository is the knowledge base; Claude is the intelligence layer

**Decision:** No backend, database, vector store, RAG pipeline, sub-agents, CI, or
scripts. Markdown with YAML frontmatter for knowledge, YAML for config, JSON for the
machine-owned ledger.

**Reasoning:** The realistic corpus for the next year is thousands of atomic notes, not
millions. Grep over structured markdown with a controlled topic vocabulary beats naive
embedding search at that scale and stays human-auditable. Embeddings become interesting
when grep stops finding things; that will be observable when it happens.

**Format reasoning:** Markdown body = the thinking, human-readable. YAML frontmatter =
the queryable index. YAML for `_registry.yaml` and `topics.yaml` because they are
hand-edited and take comments. JSON for `ledger.json` because it is machine-owned and
its rigidity is the point — it must not drift.

---

## 2026-09-10 — One insight per file, not one file per video

**Decision:** Atomic insight files under `creators/<slug>/insights/`.

**Reasoning:** Per-video files make "which creators believe X" a full-corpus read, and
make an evolving opinion impossible to represent — a belief that changed across four
videos would live in four unrelated files. Atomic files with typed frontmatter make
cross-creator synthesis a grep and let a claim carry its own supersede chain. The cost
is more files, which markdown handles fine.

---

## 2026-09-10 — Raw transcripts are never committed

**Decision:** Transcripts are fetched into memory, extracted from, and discarded.
Insight files carry video IDs and timestamps.

**Reasoning:** Transcripts are large, re-fetchable by ID, and would dominate the repo.
Timestamps preserve the path back to the source, which is what actually matters.

---

## 2026-09-10 — Three extraction lanes: CLAIM, CRAFT, CASE

**Decision:** Insights declare a lane, and the body schema differs by lane.

**Reasoning — this was forced by real data, not designed up front.** The original
design had one claim-shaped schema. Sizing Kallaway's catalog showed 323 videos of
which ~97% are Shorts under 60 seconds. A Hormozi long-form talk yields *claims*; a
Kallaway Short is usually not a claim at all but a *demonstration of craft* — a hook
structure, a compression technique. Forcing "Claim / reasoning / evidence" onto those
would have produced ~300 near-empty files and lost the actual value, which is the shape
of the thing rather than its assertion. CASE was added for Chris Raroque, whose
material is neither doctrine nor technique but things actually built.

**Consequence:** the four tracked creators cover three distinct knowledge types, which
is a stronger corpus than four creators all asserting principles at each other.

---

## 2026-09-10 — Kallaway's premise corrected before processing

**Decision:** Kallaway's `primary_lane` is CRAFT, not CLAIM. Recorded in
`creators/kallaway/profile.md`.

**Reasoning:** The stated premise was that his channel is about how to create content.
The catalog does not support that — see the profile for the evidence. His value is
demonstrated craft, and treating him as a content-strategy doctrine source would have
produced a knowledge base of insights he never actually stated.

---

## 2026-09-10 — Pilot before backfill

**Decision:** Process 20 representative Kallaway videos, then stop for inspection
before processing the remaining 303 or starting any other creator.

**Reasoning:** The lane schemas are unvalidated against real transcripts. Schemas
always look right until real material hits them. Validating at 20 files costs ~24
credits; discovering the CRAFT schema is wrong at 323 files costs the whole backfill
twice.

**Selection method:** deliberately spread across four eras, all seven long-form
formats, and a view range from 3K to 8.6M — including deliberate *low* performers, so
the craft library can contrast what worked against what didn't from the same creator.
Selecting only the best videos would have made that comparison impossible.

---

## 2026-09-10 — Pilot executed: 20 Kallaway videos, 20 insights

**Result:** the three-lane schema survived contact with real transcripts. Four defects
were found, none fatal, all cheap to fix now and expensive to fix at 323 files.

### Defect 1 — no `speaker` field (severity: high)

Two of twenty videos are interviews. Claims by Daniel Ek and Mark Zuckerberg would have
been attributed to Kallaway, which violates SKILL.md §2 directly. A third case appeared
where Kallaway *reports* a third party's framework (Virgil Abloh's 3% rule) — neither his
claim nor a guest's.

`speaker` and `speaker_role` were added ad hoc during the pilot. **`speaker_role` needs a
controlled vocabulary** (`self` | `guest` | `reporting-third-party`) rather than values
invented per insight, or it will drift the way `topics` would without `topics.yaml`.

### Defect 2 — no `commercial` flag (severity: high)

Four of twenty videos are commercial content. The two highest-view videos in the recent
catalog are both Microsoft Copilot Studio placements. Without a flag, a later synthesis
pass reads paid recommendations as sincere technique advice — and would have recommended
imitating a sponsored format. Added to the ledger during the pilot; belongs in insight
frontmatter too.

### Defect 3 — schema assumes one video per insight (severity: medium)

The strongest CRAFT insight (`mid-roll-rehook--003`) is built from seven instances across
five videos, and the commercial-content insight from four. The `source` block holds one
`video_id`, so both required an ad-hoc list in `timestamps`. Cross-video patterns are not
an edge case — they are where the best craft insights come from, because a pattern is
only visible across instances.

### Defect 4 — `views_at_capture` invites a false inference (severity: medium)

Recording performance was correct, but the pilot showed view counts in this catalog track
*subject matter*, not technique: 3K to 8.6M for the same creator and format. The schema
should require any insight citing performance to state what it attributes it to.

### What worked

- **Three lanes were the right call.** CLAIM would have produced near-empty files for
  most Shorts; CRAFT captured what was actually there.
- **Atomic insights paid off immediately.** One 60-second video produced both a CRAFT and
  a CASE insight, consumed by different downstream readers.
- **Zero-insight videos are useful.** Six of twenty produced no standalone insight; four
  still contributed evidence to cross-video patterns.
- **Deliberate low-performer sampling changed the conclusions.** The most transferable
  craft insight came from a 29K-view video and the most important strategic one from a
  3.3K-view video. Selecting on views would have inverted the findings.

### Not decided here

Whether to fix the schema before backfilling, and whether the backfill is worth its cost
given yield concentration — 4 of 20 insights came from a single 13-minute video, while
the two highest-view Shorts produced 2 and 0. Both are for Ameer.

---

## 2026-09-10 — Schema revision 2: the four pilot defects fixed

All four defects from the pilot are closed, and the existing 20 pilot files were
migrated and validated rather than left on the old schema.

### 1. Attribution is now mandatory and closed

`attribution: {claimed_by, role, published_by, co_constructed_with}` on every CLAIM and
CASE. `role` draws from a **closed vocabulary** in the new `_meta/vocabularies.yaml`:
`self` | `guest` | `host-framed-guest-endorsed` | `third-party-reported` | `unknown`.

`host-framed-guest-endorsed` was added because the pilot found a case neither "his" nor
"the guest's": Kallaway proposed the taste-moat framing and Ek accepted and extended it.
Crediting either alone would misreport what happened.

`unknown` is the fallback, and an insight carrying it **may not be used in synthesis**
until resolved. That is what makes the vocabulary closed in practice — there is a legal
move when nothing fits, so there is no reason to invent a value.

### 2. Commercial is mandatory, and describes content rather than payment

`commercial: {status, basis}` on every insight including `status: none`, because an
absent field is indistinguishable from an unassessed one.

**A correction to the pilot's own finding.** The pilot recorded these videos as
"sponsored placements." That was an overstatement and is retracted. None of the three
carries a disclosure, and asserting payment without evidence is a factual claim about a
real person's undisclosed financial relationships.

The vocabulary now separates the observation from the accusation:
`promotional` (observable: one product is the sustained subject, framed favourably, no
failure conditions, no alternatives) versus `disclosed-sponsorship` (a disclosure exists
and is quoted). `basis` is required for every status except `none`.

### 3. PATTERN is a first-class knowledge type

New directory `creators/<slug>/patterns/`, new `knowledge_type` field, and a promotion
rule in `references/extraction.md` §6: a construction seen in a second video becomes a
PATTERN rather than an insight with an appended timestamp.

Patterns require `instances` (structured, with per-instance tier and commercial status),
`span`, `sample_basis`, `generalization`, and a mandatory `## Limits of this
observation` section.

`generalization: within-creator` is the default and stays until a second creator shows
the pattern independently. The two pilot cross-video findings were migrated:
`mid-roll-rehook--p001` (7 instances, 5 videos) and `promotional-framework-format--p002`
(4 instances). Their single-video predecessors are retired via `supersedes`.

### 4. Performance is structurally prevented from carrying causal weight

`performance` now requires `interpretation`, whose vocabulary has effectively one legal
value: `sampling-context-only`. The alternative, `controlled-comparison`, requires
`performance.controls` naming what was held constant — **nothing in the knowledge base
qualifies, and nothing is expected to.**

`confounds` is required where a figure is unusual, so the competing explanation travels
with the number. Patterns reason with `performance_tier` relative to the creator's own
catalog rather than raw counts.

The standing rule, in SKILL.md §6a: performance may describe the sample or show a
pattern spans tiers. It may never be cited as evidence that a technique caused a result.

### Also added: `evidence_strength`, a second axis

`confidence` records how *clearly* something was said; `evidence_strength` records
whether it is *backed* (`none` | `anecdote` | `self-reported-data` | `external-data` |
`demonstrated`). The pilot repeatedly hit forcefully-asserted, unsupported claims and
had no way to record both facts at once. Six of eight CLAIM insights are now
`confidence: high` + `evidence_strength: none`, which is a finding in itself.

### Defect found during validation: the fence rule was wrong for CRAFT

The pilot's rule — everything above `## Agent notes` is sourced — is false for CRAFT and
PATTERN files. Naming a pattern, explaining why it works and stating where it fails are
all *agent analysis of an observed construction*. Treating those as sourced would credit
the creator with reasoning they never did.

The fence is now lane-aware, with source-only sections declared per lane
(`schemas.md` §1). The practical consequence is worth stating plainly: **a CRAFT insight
is mostly the agent's reading of what a creator did**, and no file may imply otherwise
unless `observed_in.stated_by_creator` is `true`.

### Validation

A validator was written in the session scratchpad — **not committed**, per the
repository's no-scripts rule. It checks closed vocabularies against
`_meta/vocabularies.yaml` itself (so it cannot drift from the source of truth), required
fields per lane and knowledge type, the lane-aware fence, inline timestamps in
quote-bearing sections, pattern minimums, ledger reconciliation, and dangling ID
references. It also greps for performance data used causally.

First run: 10 failures. Three were a validator bug (topic regex broke on trailing
comments), six were the CRAFT fence defect above, and one was a real missing field.
After fixes: **20 files pass, 0 errors** — 18 insights, 2 patterns.

Three genuine gaps it caught in the pilot's own work: two interview insights quoted
claims with no inline timestamps (the long transcripts were fetched without timestamp
markers — now flagged in-file as approximate), and one pattern's instance table had no
timestamps at all.

### Not done, deliberately

The remaining 303 Kallaway videos and the other three creators are untouched.
