# Extraction — transcript to insights

Read `schemas.md` before writing any file.

## 1. Before spending a credit

1. `creators/_registry.yaml` → who is tracked, which lane they serve.
2. `_meta/ledger.json` → **drop every video ID already in `processed_videos`.**
3. `get_youtube_video_info` (free) on the remainder. Skip:
   - live streams and stream VODs
   - videos whose titles indicate a near-duplicate of something already processed
   - material clearly outside the creator's tracked lane
4. Only then fetch transcripts.

Triage is not a formality. A creator with 300 videos will produce many near-identical
ones, and paying for the third version of the same idea buys nothing.

## 2. Reading a transcript

Read the whole thing before extracting anything. Extracting as you read produces
insights biased toward the opening, because that is where creators front-load.

Ask, in order:
- What is **asserted** here? → CLAIM candidates
- What is **demonstrated** here — in how the video is built, not only what is said?
  → CRAFT candidates
- What was **actually done or built**? → CASE candidates

### 2a. Assess attribution before writing anything

For every CLAIM and CASE candidate, settle **who is asserting it** before drafting.
This is not a formality — it is the check that prevents SKILL.md directive 1 being
violated silently.

| Situation | `attribution.role` |
|---|---|
| The tracked creator, their own view | `self` |
| A guest asserting their own view | `guest` |
| Host proposes a framing, guest accepts/extends it | `host-framed-guest-endorsed` |
| Creator reports an absent third party's framework | `third-party-reported` |
| Cannot be established from the transcript | `unknown` |

A guest merely *answering a question* is `guest`, not `host-framed-guest-endorsed`.
Reserve the latter for the host actually proposing the frame.

An insight with `role: unknown` may not be used in synthesis until resolved.

### 2b. Assess commercial character before writing anything

Every video gets a `commercial.status`, including `none`. Ask:

- Is one product the sustained subject, framed favourably throughout?
- Are failure conditions or alternatives given? (Their **absence** is the strongest
  signal of promotional content.)
- Is there an explicit disclosure either way? Quote it.

> **Never write `disclosed-sponsorship` without a disclosure to quote.** `promotional`
> is an observation about content and is always safe when the observable features are
> there. Asserting sponsorship without evidence is a factual claim about a real
> person's undisclosed financial relationships — do not make it.

`basis` is required for every status except `none`.

## 3. What is and is not an insight

**An insight is:** a claim, pattern, or case that would still be useful six months
from now, stated precisely enough to be argued with.

**An insight is not:**
- a summary of the video
- a restatement of the title
- a fact about the news item the video covers
- a platitude the creator repeated in passing ("consistency matters")

The test: *could someone disagree with this?* If not, it is not an insight.

Repetition across videos is signal, not noise — but it is recorded as a **link**, not
a duplicate file. The second occurrence adds a timestamp to the existing insight's
`source`, or creates a new insight only if the idea genuinely developed.

## 4. Yield expectations

A dense long-form video: 3–8 insights. A 60-second Short: **0–2, usually 1.**

Many Shorts produce **zero CLAIM insights and one CRAFT insight**, and that is the
correct outcome, not a failure. Do not manufacture claims to fill a file. A processed
video with zero insights is recorded in the ledger with `insights: 0` — that is
useful information about the creator's catalog.

## 5. CRAFT extraction, specifically

This is the lane most easily done badly. The failure mode is describing the video
instead of the technique.

Wrong: "He opens by saying Christopher Nolan wanted to detonate a real bomb."
Right: "Opens on the single most implausible fact of the story, stated flatly and
without framing, before the viewer knows the subject."

The pattern must be stated so it could be **reproduced on an unrelated subject.** If
it cannot, it has not been extracted — it has been transcribed.

Always fill `## Where it fails`. A technique with no stated failure conditions is a
technique that has not been understood, and it is how the knowledge base ends up
recommending hook formats that are wrong for a technical audience.

## 6. Linking, and promoting to a PATTERN

Before writing a new insight, grep the creator's existing insights **and patterns** on
the same topics.

- **Same idea, developed or reversed** → new file with `supersedes: <old-id>`. Never
  edit the old one. Both survive; `synthesis/evolution.md` reads the chain.
- **Related idea from another creator** → add ids to `related` on both sides.
- **Same construction seen in a second video** → **promote to a PATTERN.** Do not
  append a timestamp to a single-video insight.

### The promotion rule

A single-video CRAFT insight that recurs is no longer a single-video claim. When you
observe the same construction in a second video:

1. Create `creators/<slug>/patterns/<slug>--p<nnn>.md` per `schemas.md` §3.
2. Record **every** instance in `instances`, with `timestamp`, `note` and
   `performance_tier`.
3. Fill `span` honestly — which eras, which tiers, which commercial statuses. A pattern
   observed only in one era and one tier is weak, and `span` is what shows it.
4. Fill `sample_basis` with what was actually sampled, e.g. "20 of 323 videos,
   purposively sampled".
5. Set `generalization: within-creator`.
6. Retire the original single-video insight if the pattern fully supersedes it
   (`supersedes` on the pattern), or keep it if it says something the pattern does not.
7. Update the contributing videos' `contributes_to_patterns` in the ledger.

**Why the promotion rule exists:** in the pilot the strongest craft finding was visible
only across five videos. Five separate insight files would each have looked like an
unremarkable phrase; the recurrence *was* the finding. Cross-video observation is not
an edge case — it is where craft knowledge lives.

**A pattern needs two instances minimum.** Do not open a pattern file speculatively and
wait for it to fill.

## 7. Finishing a run

1. Update `_meta/ledger.json` — every video fetched, including zero-insight ones.
2. Update only the `synthesis/` files the new insights actually touch.
3. Add any genuinely new topics to `_meta/topics.yaml` in the same commit.
4. Commit with a message naming what was learned.

## 8. Standing rules

- Transcripts stay in memory. They are never written to the repo.
- Timestamps are mandatory. They are the path back to the source that replaces
  storing the source.
- If a transcript is auto-generated (ASR) and a passage is garbled, **do not guess.**
  Record what is legible, note the uncertainty in `## Agent notes`, and move on.
- **Record performance, then refuse to reason from it.** Fill `performance` with
  `interpretation: sampling-context-only` and name the `confounds`. Never write a
  sentence in which a view count supports a claim that a technique works.
- **Never invent a controlled value.** If nothing in `_meta/vocabularies.yaml` fits,
  use `unknown`, explain in the body, and raise it in `_meta/decisions.md`.
- **`confidence` is how clearly it was said. `evidence_strength` is whether it is
  backed.** A forcefully asserted, unsupported claim is `high` + `none`, and the
  knowledge base must be able to say exactly that.
