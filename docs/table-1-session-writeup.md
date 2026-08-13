# Session writeup — DDD MUC, 12 Aug 2026

**Workshop:** From North Star to Working App
**Table scope:** One traveller. One trip. One friend. From getting home to the friend seeing it.
**Format:** one chat all evening, AI as participant, every artifact corrected by a human before it moved on.

The few clock times below come from file timestamps, not from the transcript, and are
approximate. Everything else is ordered by the sequence of messages.

---

## 1 · North Star — converge (card prompt 1b)

**Done.** The `devils-advocate` skill was invoked against a shortlist of seven candidates:

- Depth of Interaction (time/size)
- Number of trips contributed to by both trip participants
- Number of opened trip notifications
- Ranking on Google Search for "trip sharing"
- User satisfaction
- Weekly actives (opened the app or viewed content ≥1×/week)
- Number of times past trips are interacted with

The critique sorted them three ways: **gameable by the team** (notification opens,
weekly actives, depth of interaction), **still healthy while the product dies**
(user satisfaction — survivorship bias; Google rank; weekly actives), and **an actual
unit of value** (trips contributed to by both participants).

Recommendation given: *weekly co-authored trips* — trips receiving a meaningful
contribution from ≥2 distinct people in the last 7 days — with two counter-metrics
(notifications sent per active user; week-4 retention of the invited second
contributor). A follow-up asked for the same feedback in condensed form, which was
provided.

**Room decision:** the red sticky on the flipchart reads *"# of Trips contributed to by
both participants"*, so the table took the candidate but not the weekly-rate
reframing.

**Skipped:** prompt 1a (divergent generation of 15 candidates) never ran in this chat.
The candidates arrived pre-shortlisted, so the AI took no part in the divergent phase.

---

## 2 · Domain Story — seed (card prompt 2a)

**Skipped entirely.** The `domain-story-seeder` skill was never invoked. The table wrote
the story on paper first and brought it in as a photograph — a deliberate inversion of
the card's sequence, and consistent with "build on paper first, then invoke a critic."

---

## 3 · Domain Story — transcription

**Done, but never confirmed.** A photo of the flipchart arrived as an attachment that
rendered only as a generic PDF icon; the actual file was located at
`~/Downloads/2026-08-12-Document.pdf` (≈19:55) and read from disk. The same
icon-instead-of-content problem recurred later with the glossary.

Thirteen sentences were transcribed (numbered 0–12), and three readings were flagged as
uncertain:

1. sentence 1 — `Trip` written above a struck-through `Organizer`; read as "Trip Organizer"
2. sentence 8 — a scribbled-out word before `User`
3. sentence 2 — `Friend` heavily overwritten; read as emphasis, not correction

**None of the three was answered.** The table moved straight to the critique, so the
transcription was used unverified from this point on.

---

## 4 · Domain Story — challenge (card prompt 2b)

**Done.** The `domain-story-critic` skill was invoked. Three load-bearing findings:

1. **The story never reached its own destination.** The Friend was invited in sentence 1,
   accepted in sentence 2, and then vanished for eleven sentences. The scope's stated
   endpoint — the friend seeing it — was the one thing not drawn.
2. **Sentences 7–12 were a second story.** A different actor (`User`, a stranger)
   searching and bookmarking public trips, with no causal link to the first half — and
   six of thirteen sentences that did not move the chosen north star at all.
3. **Sentences 0–2 sat outside the declared scope,** and assumed people set up a shared
   album *before* travelling. A cheap test was proposed: ask everyone at the table what
   they actually did after their last shared trip.

Also raised: three `looks at` verbs (UI language, not domain language), `bookmarks` /
`searches` / `creates` as UI or CRUD, six actor labels for what appeared to be two
people, no software-system actor anywhere, a `Highlight Reel` that appeared from
nowhere, and nobody asking the co-participant before publication.

---

## 5 · Domain Story — rewrite and map

**Done.** Fixes were incorporated into a 12-sentence rev 2: the Friend-sees-it sentence
added, `Trip Service` promoted to a software actor to give the invitation and the reel
an origin, `looks at` → `relives` / `retraces`, `creates` → `starts`, `shares` →
`adds … to`, six actor labels collapsed to three, and the map step pulled back to the
traveller's half. Sentences 7–12 were parked as "Story 2 — Public Discovery."

A page was written to `docs/domain-story-map.html` with the sentence table, a
domain-story map, the change log, and the open questions.

**Publishing failed.** The Artifact tool was blocked because the session authenticates
with `ANTHROPIC_AUTH_TOKEN` rather than a claude.ai account, so no shareable link was
produced at any point in the evening. The page stayed a local file.

**Deliberately not done:** no lanes, groups, or colour-coded regions were drawn on the
map — the table asked to cut bounded contexts themselves first.

---

## 6 · Bounded Contexts (card prompt 3)

**Skipped in this chat.** The `domain-story-context-finder` skill was never invoked, no
photo of the table's rings was shared, and **the resulting core context was never
reported back**. This had a downstream cost: the prototype at station 5 had to be built
against the whole story, because the context that was supposed to scope it was unknown.

---

## 7 · Break and driver swap

Not observable from the transcript.

---

## 8 · Visual Glossary (card prompt 4a)

**Done, partly confirmed.** The glossary photo again arrived as a PDF icon; the file was
found at `~/Downloads/visual-glossary.pdf` (≈20:47). Seven terms and eight relationships
were transcribed, and four readings were queried.

Two corrections came back from the table:

- `Moment part of 1..*  Highlight Reel` → **`0..1`**. This resolved a cardinality clash
  the critique had raised (`Trip has 0..1 Highlight Reel` vs. every Moment needing at
  least one), and the objection was withdrawn.
- **`Creator` → `Organizer`**, **`Participant` → `Friend`**. The glossary being the
  terminology authority, the domain story was rewritten to match and the page reissued
  as rev 3.

**Left unanswered:** whether `owns` reads `1..1`, whether `0:25` is a real 25-photo
business rule, and the direction of the `participates` arrow.

**Not produced:** the full term catalogue and derived model (entities, value objects,
aggregates, identity) that prompt 4a asks for. Only a short preview was given —
`Trip` as aggregate root, `Moment` as a second aggregate, `Location` and `Photo` as
value objects — pending the naming decision.

**Skipped:** prompt 4b, the `domain-story-glossary-consistency` skill. A hand-rolled
reconciliation was done inline instead, at station 5.

---

## 9 · Story edits

**Done.** `Map` was removed on request — it had no glossary entry and no bearing on the
friend seeing the trip. The story became **11 sentences (rev 4)**, and one of the two
story-vs-glossary gaps closed.

A rendering defect was also fixed: `<pre class="mermaid">` renders only inside the
Artifact runtime, so the diagram was inert when the page was opened as a local file.
`mermaid@11` was downloaded to `docs/mermaid.min.js` (≈20:53) and referenced with a
guarded initializer. **Not visually verified** — no browser was available in the session.

---

## 10 · Running Prototype (card prompt 5a)

**Done.** The `prototype-from-domain-story-and-glossary` skill was invoked with the
frozen 11-sentence story, the interpreted glossary, and no formatting example. Built to
`docs/prototype.html` — one self-contained file, in-memory state, an Organizer/Friend
persona switcher, sentence numbers on every control, and a Trip Service log that records
each action as its story sentence.

Glossary cardinalities became UI rules: Location required (`1..1`), Photos capped at 25
(`0..25`), one Friend per Trip (`1..1`), at most one Highlight Reel (`0..1`), empty Trips
legal (`0..n`). `Photo` and `Location` became fields, not screens. Seed data was placed
on the bounds — a Moment with exactly 25 Photos, one with zero, a Trip with no Moments,
an invitation still unaccepted.

**Not click-tested** — no browser in the session. Logic was verified, pixels were not.
**Not published** — same auth block as before, so no link went to the host.

---

## 11 · Fix round and demo (card prompts 5b, demo)

**Skipped.** No walk-through of the story against the prototype was reported, so no fix
round was run. The three demo sentences were never agreed.

---

## What the table produced

| Artifact | State |
|---|---|
| North star metric | Chosen: trips contributed to by both participants |
| Domain story | Rev 4, 11 sentences — corrected, never formally frozen |
| Story 2 (Public Discovery) | Parked, 6 sentences |
| Domain story map | `docs/domain-story-map.html`, local only |
| Bounded contexts | Cut by the table; not recorded here |
| Visual glossary | 7 terms, 8 relationships; 2 corrections applied |
| Derived model | Preview only |
| Prototype | `docs/prototype.html`, local only |
| Host link | None — artifact publishing was blocked all evening |

## Open questions carried out of the session

1. Does anyone really invite before there is anything to see? Sentences 1–3 may need inverting.
2. When is a Trip finished? Nothing closes it, yet the north star counts Trips.
3. Is `Moment` one thing or two — a dropped photo and a highlighted keepsake behave differently.
4. `Trip Invitation` and `Comment` are story vocabulary with no glossary entry.
5. Three glossary readings unconfirmed: `owns 1..1`, the `0..25` Photo cap, the `participates` direction.
6. `Organizer` fits sentences 1–3 and fights 9–11 — possibly two roles wearing one name, and possibly the bounded-context seam.

## Process notes

- **Two attachments arrived as generic PDF icons rather than content.** Both times the
  real file had to be located in `~/Downloads`. Worth knowing for the next session.
- **Artifact publishing was unavailable for the whole evening** because
  `ANTHROPIC_AUTH_TOKEN` takes precedence over a claude.ai login. Both deliverables exist
  only as local files.
- **The AI never got the last word on any artifact.** Every transcription was offered for
  verification, and the two corrections that came back — the `0..1` cardinality and the
  `Creator`/`Participant` renames — were applied and propagated. Several other
  verification questions went unanswered and are listed above as open.
- **Three of the five station skills were never invoked:** `domain-story-seeder`,
  `domain-story-context-finder`, and `domain-story-glossary-consistency`. The first two
  by choice (paper first, own cut first); the third was substituted with an inline
  reconciliation.
