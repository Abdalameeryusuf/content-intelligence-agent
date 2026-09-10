# Lifepal — current state

> **Snapshot as of the source documents: 2026-08-11.**
> Read on 2026-09-10. **Roughly a month may have passed with changes not reflected
> here.** Do not present this as live state.
>
> Canonical source: the Lifepal repo's `docs/`. This is a mirror.

## Stage

**Pre-build on v1, not pre-planning.** Three planning conversations complete:

- Design system (`01-design-system.md`) — shadcn/ui base, Kibo UI extension
- Requirements (`02-requirements.md`) — 52 requirements across eight domains plus the
  conversation layer, down from v0's 68
- Component inventory (`05-components.md`) — Phase 1 only, deliberately

**Phase 1 has not started.** Nothing beyond it has started.

## The six phases

Each must be in real daily use before the next begins.

| Phase | Scope | Done when |
|---|---|---|
| 1 | Conversation, Habits, Goals | A goal read back correctly; a habit tick reaches the grid; a spoken correction updates in place |
| 2 | Calendar + proactive notifications | A rough spoken plan becomes a confirmed schedule; a screenshot deadline reaches the calendar; one notification answered through the assistant |
| 3 | Finance | A real bank SMS becomes a confirmed transaction without being typed |
| 4 | Health | A meal plan written, a deviation logged, a workout screenshot parsed without inventing data |
| 5 | Projects + Notes | A project-linked deadline appears on the calendar; a check-in is answered |
| 6 | Parking lot | Deferred — voice notes, wearable sync |

Phase 1 is the largest (18 requirements) and is flagged in the source docs as the one
most at risk. The stated response if it hasn't closed after three weeks of real use is
to **split it, not push harder.**

## The v0 → v1 pivot — the content-relevant part

v0 was built, deployed, and used daily for months. Rather than extending it, Ameer
pulled a full data export and ran a structured interview against his own usage
evidence.

**The export: 197 documents across 26 collections.** What the numbers showed:

| Collection | Count | What it meant |
|---|---|---|
| `financeTransactions` | 48 | Largest collection — and described as tedious at every step |
| `habitChangeLog` | 26 | Against 17 habits — the review mechanism genuinely worked |
| `habitReviews` | 13 | The one Phase 3 feature the data endorsed |
| `mealLogs` | 2 | The photo flow produced two records in its lifetime |
| `goals` | **0** | Every alignment feature was reasoning against nothing |
| `projectCheckIns` | **0** | Phase 4's done-when never fired |
| `workItems`, `revenueProjects`, `clients`, `clientFollowUps`, `revenueOpportunities` | **0** | Three domains built, never touched |

**The diagnosis:** v0 was built as a logging system with a chat feature attached, when
real use showed the opposite was needed — a conversational assistant where logging
costs almost nothing and the conversation is the product.

**The decision:** archive v0 read-only as a permanent reference and fallback, restart
from an empty repository, import nothing. Ever.

Three domains and 19 of 68 requirements were cut on this evidence.

## Open questions Ameer is holding

From the business context document — these are live, not settled:

- Whether Lifepal is a product or stays a personal tool and portfolio piece
- Who it would be for, and what would have to be true for people to pay
- How the single-user architecture would need to change for more than one account

**These are honestly open.** The agent must not resolve them in content ideas, and must
not imply they are decided.

## What is deliberately excluded from this mirror

Infrastructure identifiers, auth mechanics, and environment structure. They serve no
content purpose and belong only in the Lifepal repo.
