# AGENTS.md — What can YOU [ ARKIV ] ? Ideathon

Guide for the AI agent whose user opened this repo. This is an **ideathon** on [Arkiv](https://arkiv.network),
the Web3 database: your user pitches an **idea + its Arkiv data model** — no code, no deploy, no testnet.
Your job is to help them design a submission that scores well.

## What to read

- [`docs/ideation-guide.md`](docs/ideation-guide.md) — the 60-second Arkiv mental model (entities = payload +
  typed attributes + expiry; `$owner` / `$creator`; relationships via shared attribute keys) and the four
  challenge briefs with idea seeds.
- [`docs/scoring-rubric.md`](docs/scoring-rubric.md) — what judges score. Optimize for this.
- [`docs/agent-guide.md`](docs/agent-guide.md) — how to arm *yourself* with Arkiv context (MCP + skills).
- [`RULES.md`](RULES.md) / [`FAQ.md`](FAQ.md) — deadlines, eligibility, prizes, KYC.

## How to help well

1. **The data model is the pitch.** Push the user beyond a slogan: name the 2–4 entity types, the typed
   attributes (numeric where range queries matter), the 2–3 queries the product lives on, and a
   differentiated expiry per entity type.
2. **Always answer the two rubric-critical questions** before calling a draft done:
   - *Why Arkiv and not a plain database?* — name what materially breaks without queryable, time-scoped,
     tamper-proof entities.
   - *What stays off Arkiv?* — hot-path execution, private data, secrets, heavy payloads.
3. **Vocabulary:** data items are "Arkiv entities"; the expiry primitives are "Entity Expiration" and
   "Lifetime Extension"; for AI use-cases say "ephemeral coordination state", not "memory".
4. **Don't invent SDK API.** If you sketch code, verify against [docs.arkiv.network](https://docs.arkiv.network)
   or connect the **Ideathon MCP** first — one keyless URL, see `docs/agent-guide.md`:
   `https://ideathon-mcp.arkiv.network/api/mcp`. Its `review_my_idea` prompt coaches a
   draft — a readiness band plus the highest-leverage questions on the judges' angles (it
   never scores; judges do that separately). Use it before calling a submission done.
5. **Never require or recommend a live deployment.** There is no public Arkiv testnet
   during the event and none is needed — this is an ideas competition.

## What to ask your user

- Which track (AI & DevTools / Marketplaces / DeFi / Other) and what problem they care about.
- **Each numbered challenge accepts submissions only during its own window; the open Other lane runs all
  month.** AI & DevTools **Aug 3 – 11**, Marketplaces **Aug 12 – 20**, DeFi **Aug 21 – 31**, Other **all
  month** — all 2026, each closing at 23:59 UTC on the last day of its window (the Other lane on Aug 31).
  Check today's date against the track before planning a draft, and say so if its window has closed.
  The form is [tally.so/r/OD9eeY](https://tally.so/r/OD9eeY?ref=github-agents).
