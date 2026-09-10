# Lifepal — overview

> **Provenance:** derived from four project documents supplied by Ameer on 2026-09-10
> (`PersonalOS Business Context`, `00-v1-context.md`, `02-requirements.md`,
> `03-build-plan.md`), dated 2026-08-10 / 2026-08-11.
>
> **This is a mirror, not a source.** The canonical version is the Lifepal repo's
> `docs/`. Where this file and that repo disagree, the repo wins.
>
> **Ameer has stated some of this may be outdated** — specific features and
> requirements may have changed; the core has not.

## Naming

The project is now **Lifepal**. It was previously **PersonalOS**, and every supplied
document uses the old name. Both names refer to the same project. `v0` refers to the
first version, archived read-only; `v1` is the current rebuild.

## What it is

A conversational, AI-driven personal operating system: one application where habits,
health, finance, projects, calendar, and notes share a backend, and the primary way of
interacting with it is **talking to it** rather than filling out forms. Structured
views sit alongside the conversation as a verifying second layer.

## The eight domains

| Domain | Covers |
|---|---|
| Home | The conversation surface, plus today's snapshot |
| Today | Everything outstanding right now, across domains, logged in place |
| Habits | History, streaks, periodic AI-assisted review |
| Health | Workouts, bodyweight, weekly meal plan (deviations logged, not every meal) |
| Finance | Transactions captured from bank SMS rather than typed |
| Projects | Personal builds and eventually client work |
| Notes | Capture and search |
| Calendar | Day timeline, month view, 16-week quarter grid |

## The two mechanics that carry the differentiation

**Conversation as the primary write path, with a non-model fallback always
available.** Every domain can be written by talking or by direct entry; both routes go
through the same underlying functions, so nothing depends on the model being available
or parsing correctly.

**Two-tier AI routing to control cost.** Routine interactions go to a cheaper, faster
model; anything requiring judgment escalates to a stronger model loaded with a
domain-specific skill. The split is enforced architecturally rather than by
discipline — specifically because v0 proved discipline alone does not hold cost down.

## The design principle worth remembering

> **The system asserts, you correct. It never asks you to originate data it could
> assert.**

The meal plan is the record and deviations are the writes. The SMS feed is the record
and corrections are the writes. Today asserts what's outstanding. A brain dump returns
a proposed day.

This is a genuinely opinionated stance about how personal software should work, and it
is the most content-relevant idea in the project.

## Why this matters for content

Lifepal is an AI product built solo, with real opinions about AI product design and a
documented history of one hard reversal. That combination — building it, having views
about it, and having been wrong once with receipts — is the raw material.

Related: `project/current-state.md`, and `me/positioning.md`.
