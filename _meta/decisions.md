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
