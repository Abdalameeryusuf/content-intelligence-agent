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

## 6. Linking

Before writing a new insight, grep the creator's existing insights on the same topics.

- **Same idea, developed or reversed** → new file with `supersedes: <old-id>`. Never
  edit the old one. Both survive; `synthesis/evolution.md` reads the chain.
- **Same idea, restated unchanged** → add the timestamp to the existing file's
  `source.timestamps`. No new file.
- **Related idea from another creator** → add ids to `related` on both sides.

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
