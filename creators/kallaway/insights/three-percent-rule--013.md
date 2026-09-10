---
id: kallaway--three-percent-rule--013
knowledge_type: INSIGHT
creator: kallaway
lane: CLAIM
type: framework
topics: [positioning, creative-process, titles-and-framing]

attribution:
  claimed_by: virgil-abloh
  role: third-party-reported
  published_by: kallaway
  co_constructed_with: null

confidence: high
evidence_strength: anecdote
stance: moderate

commercial:
  status: none
  basis: null

source:
  video_id: GacM6G1owfA
  title: "The simple genius of Virgil Abloh's 3% rule"
  duration: "0:49"
  timestamps: ["0:06", "0:22", "0:34", "0:44"]

performance:
  views_at_capture: "5.8K"
  tier: low
  captured: 2026-09-10
  interpretation: sampling-context-only
  confounds:
    - "No primary Abloh source cited in the video; the framework is unverified as reported."

captured: 2026-09-10
supersedes: null
related: [kallaway--comparison-anchor--008]
---

## Claim

**Framework attributed to Virgil Abloh, reported by Kallaway. Abloh is not a tracked
creator and this is second-hand.**

> "Virgil believed you only had to alter a product by 3% to create something totally
> new." — 0:06

The mechanism Kallaway gives for why it works:

> "People constantly desire both familiarity and novelty. Your subconscious likes
> recognizing things you've seen before, but also releases dopamine when you see
> something new. The 3% rule achieves both — base comfort with a hint of innovation."
> — 0:44

## Their reasoning

The argument is that recognition and novelty are separate appetites, and that a small
alteration to a familiar object satisfies both simultaneously, where a large alteration
satisfies only the second.

The supporting anecdote: asked to reimagine ten Nike silhouettes, Abloh found the
products "so perfectly put together, he only wanted to make slight edits" (0:34) —
presented as the rule being discovered rather than applied.

## Evidence they offered

**One anecdote and an unsourced neurological claim.** The dopamine mechanism is asserted
with no citation. The Nike collaboration is real and well known, but is a single case
and is selected precisely because it worked.

Notably, the "3%" is not measured or measurable — no method is given for what counts as
3% of a product.

## Scope / conditions

None stated. Presented as generally applicable to design and creative work.

## Agent notes

[INFERENCE] The number is rhetorical, not quantitative, and should be treated that way.
Its value is the *direction* it points — that minimal deviation from a familiar form can
outperform reinvention — not the figure.

[INFERENCE] This is directly relevant to a real Lifepal decision, and pulls against a
temptation. Lifepal's differentiating mechanic is genuinely unfamiliar: conversation as
the primary write path, the system asserting and the user correcting. Under the 3% rule,
the way to make that legible is to anchor it to a form people already know and change
one thing — which is also what `kallaway--comparison-anchor--008` argues from a different
direction.

[INFERENCE] The counter-case is worth holding alongside it: the project docs record that
v0 failed *because* it was built as a familiar thing (a logging app) with the novel part
bolted on. Applied to the product itself, the 3% rule would have endorsed exactly the
mistake the export data exposed. Applied to how the product is *explained*, it is sound.

[RECOMMENDATION] Keep the distinction explicit — this framework is about presentation,
not architecture. Filing it under `positioning` rather than `product-launch` reflects
that, and a future synthesis pass should not let it drift.

[INFERENCE] **Attribution note.** `role: third-party-reported` — the framework is
Abloh's, reported by Kallaway, and Abloh is not present. The claim belongs to Abloh *as
reported*, and the report is unverified: the video cites no primary source, which is why
`evidence_strength` is `anecdote` rather than anything stronger.

During the pilot this case produced an invented role value. Schema revision 2 closes the
vocabulary in `_meta/vocabularies.yaml` precisely to stop that.
