# What can YOU [ ARKIV ] ? Ideathon — Scoring Rubric

Every submission — any challenge, or the open Other lane — is scored on the same 100-point rubric:
**20 points for alignment with the track it entered + 80 points of general criteria.**

This is an **ideathon**: we score the thinking, not a deployment. A video or diagram can raise your
*Clarity* score (it makes the idea easier to see) and filmed ideas are prioritised for spotlights and
amplification — but there are no separate points for production polish.

---

## The point split

| # | Criterion | Points |
| - | :-------- | -----: |
| 1 | Track alignment | **20** |
| 2 | Arkiv fit — the counterfactual | 20 |
| 3 | Data & query design | 20 |
| 4 | Impact & usefulness | 15 |
| 5 | Clarity & feasibility | 15 |
| 6 | Uniqueness | 10 |
|   | **Total** | **100** |

Each criterion is scored **0–5**, then weighted: `points × (score / 5)`. A criterion that is entirely
absent scores **0** — not 1.

| Score | Meaning |
| :---- | :------ |
| 0 | Absent — the submission doesn't address it at all |
| 1 | A slogan with no substance |
| 2 | Gestured at, but generic — could be said of any idea or any storage layer |
| 3 | Solid — specific to this idea, meets expectations |
| 4 | Good — thoughtful, above average, clearly reasoned |
| 5 | Excellent — sharp, creative, could be handed to a builder as-is |

---

## The six criteria, with anchors

### 1 · Track alignment — 20 pts

How directly the idea serves the track it entered: its **impact and relevance for that space**
specifically. For the **Other** lane, alignment means how genuinely the idea needs the
Web3-database model at all (queryable, time-scoped, tamper-proof entities) outside the three
named tracks.

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| The track label is incidental — the same pitch could sit in any track | Clearly belongs: it addresses a real problem of this track's space and speaks its language | A flagship example of the track: high impact for that space, exactly the kind of idea the track brief describes |

### 2 · Arkiv fit — the counterfactual — 20 pts

Does the idea genuinely need Arkiv? The strongest submissions name what materially **breaks or
weakens on a conventional, operator-controlled database**: verifiable authorship a platform can't
forge, expiry as a guarantee rather than a cron job, an audit trail users can check themselves.

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| "It's on-chain" is the whole argument; a plain database would do fine | A concrete counterfactual: names at least one property the idea loses without Arkiv | The counterfactual is the product: the pitch collapses without queryable, time-scoped, tamper-proof entities — and says what deliberately stays **off** Arkiv |

### 3 · Data & query design — 20 pts

The data model **is** the pitch. Entities, typed attributes (numerics where range queries matter),
the filter predicates and counts the product relies on — with **Entity Expiration, Lifetime
Extension and creator/owner metadata used as real product features**, not compliance checkboxes.

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| One blob entity; no attributes worth querying; no expiry thinking | 2+ entity types with typed attributes, the 2–3 queries the product lives on, and a reasonable expiry per entity type | Right-typed attributes chosen deliberately, relationships via shared keys, queries mapped to real user questions, differentiated lifetimes reflecting product logic, verifiable creator/owner surfaced in the UX — a builder could start from this schema |

### 4 · Impact & usefulness — 15 pts

Genuinely useful to a real developer or user — not a demo hunting for a problem.

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| Tech in search of a use case | A real user with a real pain, plausibly served | You can name who adopts this on day one and why they stay — the problem matters even before the Arkiv angle |

### 5 · Clarity & feasibility — 15 pts

Is the idea explained clearly, and could it realistically be built? Is the scope sharp and honest?

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| Vague vision statement; no idea what v1 is | Clear problem, clear first slice, honest unknowns | Crisp scope with named risks; the "weekend slice" is genuinely buildable and proves the core of the idea |

### 6 · Uniqueness — 10 pts

A fresh angle — not the obvious first idea every submission reaches for.

| 1 (Weak) | 3 (Solid) | 5 (Excellent) |
| :------- | :-------- | :------------ |
| The template idea for this track, unchanged | A familiar shape with a genuine twist that changes what gets stored or asked | An angle we hadn't seen — it reframes what the track can be, and the data model shows it |

---

## Scoring formula

- Per criterion: `weighted = points × (score / 5)`.
- Judge total: sum of the six weighted values (/100), **unrounded**.
- Submission score: **unrounded average** of judge totals (human and/or LLM judges, per panel setup).

## Judging process

1. **Eligibility check before scoring.** Entries that violate the rules (plagiarism, no meaningful
   Arkiv involvement, late, prohibited content) are **disqualified before judging** — removed from
   the pool, not scored low.
2. **Calibration round.** Before independent scoring, every judge scores the same 3–5 sample
   submissions and compares notes — so a "3" means the same thing across judges.
3. **Independent scoring.** Each judge scores every valid submission in their track's pool against
   the rubric.
4. **Evidence notes.** A one-line justification is required for any extreme score (0–1 or 5).
5. **Conflict of interest.** A judge with a personal or professional connection to a submitter
   discloses it and recuses from that entry; its score is the average of the remaining judges.
6. **Ranking + allocation.** Prizes are awarded **per track** (up to one winner each at
   $500 / $300 / $200) against the track's ranking; a track with stronger submissions may be
   weighted accordingly.
7. Judges' decisions are final and not subject to appeal.

## Tiebreaker

Ties are broken on **unrounded** totals first. If two submissions are still exactly tied:

1. Higher **Arkiv fit** score wins
2. Then higher **Data & query design** score
3. If still tied, the judging team discusses and reaches consensus

---

## LLM-assisted scoring

This rubric is written so an LLM can apply it consistently (the organizer may use LLM judges as a
first pass or as additional panel members; humans make final calls). To score with an LLM, provide:
(1) this rubric in full, (2) the track's brief from the [Ideation Guide](ideation-guide.md),
(3) the submission's form answers verbatim, and (4) the instruction block below.

**Instruction block:**

```text
You are a judge for the "What can YOU [ ARKIV ] ?" Ideathon. Score the submission against the
six rubric criteria, exactly as anchored. Rules:
- Score each criterion 0–5 (integers). 0 = the submission does not address it at all.
- Judge only what is written in the submission. Do not invent missing details, do not reward
  intentions, and do not penalise plain English.
- Track alignment is judged against the provided track brief (for "Other": against whether the
  idea genuinely needs queryable, time-scoped, tamper-proof entities).
- Production polish (visual quality of video/mocks) earns nothing; content clarity does.
- For every criterion, quote or reference the exact submission text that drove the score.
- If you detect possible plagiarism, a design that doesn't meaningfully involve Arkiv, or
  prohibited content, set "flag" accordingly instead of scoring low — eligibility is decided
  by a human before scoring counts.
Return ONLY the JSON object described in the schema.
```

**Output schema:**

```json
{
  "submission_id": "string",
  "track": "ai-agents | marketplaces | defi | other",
  "flag": null,
  "scores": {
    "track_alignment":      { "score": 0, "evidence": "quote or reference" },
    "arkiv_fit":            { "score": 0, "evidence": "…" },
    "data_query_design":    { "score": 0, "evidence": "…" },
    "impact_usefulness":    { "score": 0, "evidence": "…" },
    "clarity_feasibility":  { "score": 0, "evidence": "…" },
    "uniqueness":           { "score": 0, "evidence": "…" }
  },
  "weighted_total": 0.0,
  "one_line_verdict": "string"
}
```

`weighted_total` = 20·(track_alignment/5) + 20·(arkiv_fit/5) + 20·(data_query_design/5) +
15·(impact_usefulness/5) + 15·(clarity_feasibility/5) + 10·(uniqueness/5).
`flag` is `null` or one of `"plagiarism_suspected" | "no_meaningful_arkiv" | "prohibited_content"`.

## Judge scorecard template (human)

```
Submission: [Idea name]           Track: [AI & Agents / Marketplaces / DeFi / Other]
Judge:      [Name]                Date:  [Date]

  Track alignment:                   _ /5  → _ /20
  Arkiv fit (counterfactual):        _ /5  → _ /20
  Data & query design:               _ /5  → _ /20
  Impact & usefulness:               _ /5  → _ /15
  Clarity & feasibility:             _ /5  → _ /15
  Uniqueness:                        _ /5  → _ /10

TOTAL:                               _ /100

Evidence notes (required for any 0–1 or 5):
[...]

Conflict of interest: [none / disclosed → recused]
```
