# Idea generation and critique

## 1. The bar

The goal is **200–300 people on the Lifepal waitlist who genuinely believe in what is
being built.** Not 200–300 signups harvested from a viral moment — those churn, don't
convert, and poison the signal about whether the product resonates.

Every idea is judged against that, not against expected reach.

## 2. Ideas come from intersections

Never generate from "what's trending." Generate from overlap:

```
creator knowledge  ×  the user's own experience  ×  Lifepal context
                   ×  audience problems  ×  current information  ×  goals
```

An idea touching one of these is weak. Three or more is where the original ones live.

**The user's own experience is the scarce input.** Creator knowledge is available to
everyone tracking those creators; the Lifepal build history is not available to
anyone else. An idea that could have been written by someone who never built Lifepal
is, by construction, not differentiated — and it is the single most common failure of
systems like this.

## 3. Where to look first

- `project/` — problems actually being solved right now. A hard problem solved is
  content raw material; a hard problem *not yet* solved is often better, because it is
  honest and it invites the audience in.
- `content/published/` — what has already been covered, what worked, what didn't.
  Do not re-propose something already tried without saying what would be different.
- `synthesis/topics/` — where creators disagree. A live disagreement among strong
  creators is a genuine opening for an original position, *if* the user has grounds
  to hold one.
- `me/audience.md` — the questions real people ask.

## 4. Critique, before offering

Every idea is critiqued adversarially and the critique is stored with it. Answer all
of these in writing:

1. **What would make this fail?**
2. **Who does this actually reach?** Are they the 200–300, or are they an audience
   that will never care about Lifepal?
3. **What does the user know here that nobody else does?** If the answer is nothing,
   cut the idea. Do not soften this.
4. **Is this the user's insight, or a creator's insight restated?** If restated, it is
   not an idea — it is a citation.
5. **Does this build trust with someone who has never heard of Lifepal?**
6. **Would this still be worth publishing if it got no reach?** If no, it was
   engagement bait wearing a disguise.

An idea that survives gets a file in `content/ideas/`. One that does not, does not —
and the reason it failed is worth one line in the response, because it teaches the
shape of the filter.

## 5. Idea file

Path: `content/ideas/<idea-slug>.md`

```markdown
---
id: idea-0001
status: proposed        # proposed | drafting | published | rejected
intersections: [own-experience, lifepal, creator-knowledge]
grounded_in: [kallaway--..., project/current-state.md]
target_audience: ...
created: 2026-09-10
---

## The idea
## Why this, now
## What the user brings that nobody else does
## Format and why that format
Cites craft patterns by ID where relevant.

## Critique
The six questions, answered honestly.

## What would make this fail
```

## 6. Standing prohibitions

- **No virality optimization.** No "this will blow up," no engineered outrage, no
  manufactured contrarianism. A contrarian position is fine when it is genuinely held
  and defensible.
- **No creator voice imitation.** See SKILL.md §9.
- **No generic social-media advice.** "Post consistently," "engage with your niche,"
  "use hooks" — if a recommendation would be identical for someone building a
  completely different product, it is not a recommendation, it is filler.
- **No invented Lifepal detail.** If `project/` doesn't say it, it isn't known. Ask.
- **No fabricated audience insight.** Until `me/audience.md` and
  `content/published/` hold real data, say that audience claims are assumptions.
