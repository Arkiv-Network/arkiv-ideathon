# What can YOU [ ARKIV ] ? Ideathon — Ideation Guide

---

## What you're pitching

A concept designed on [Arkiv](https://arkiv.network), the Web3 database — **the idea plus its Arkiv data model**. No code, no deploy. Your submission stands on four things:

1. **The problem** — what's broken today, and for whom
2. **The entities** — what you'd write to Arkiv, with which typed attributes
3. **The queries** — what the product asks Arkiv, filtered / paginated / counted
4. **The counterfactual** — why this genuinely needs Arkiv over a plain database, and what deliberately stays off it

The data model is the pitch. That's where the [rubric](scoring-rubric.md) scores hardest.

---

## How Arkiv works (60-second mental model)

### 1. Arkiv entities = payload + typed attributes + an expiry

Every Arkiv entity has:

- **Payload** — the actual data (JSON, text, or bytes). Stored as-is.
- **Attributes** — typed key-value pairs. **This is your index.** Filtering and lookups happen against attributes, not the payload.
- **An expiry** — every entity is time-scoped: you set how long it lives when you create it (the SDK's `expiresIn`, in seconds — a positive integer; lifetimes are measured in 2-second blocks, so prefer even values), and you can extend it later. Cost depends primarily on stored size and requested lifetime — you don't pay for forever.

### 2. Attributes have types — pick the right one

- **String attributes** support equality lookups. (The underlying protocol also supports glob matching, but the TypeScript SDK currently exposes equality only — design around `eq`.) Use for tags, statuses, names, identifiers.
- **Numeric attributes** support range queries (`gt`, `lt`, `gte`, `lte`) and are **integers** — scale decimals to fixed-point (store cents, or basis points). Use for anything you'll filter by range — timestamps, scores, counts, prices.

If you store `priority` as the string `"5"`, you lose range queries. In your pitch, say which attributes are numeric and why.

### 3. Relationships are shared attribute keys

There's no built-in foreign key. To link entities, put the parent's key in a shared attribute on the child (e.g. `{ key: "orderId", value: parentEntityKey }`). Querying children of a parent is then a single equality filter.

### 4. Two metadata fields do the tamper-proof work: `$owner` and `$creator`

- **`$owner`** — the wallet that currently controls the entity. Mutable (transferable). Only the owner can update / delete / extend.
- **`$creator`** — the wallet that originally created the entity. **Immutable** — set at creation, can't be spoofed. This is your verifiable-authorship primitive.

### 5. Expiration is a feature, not housekeeping

**Entity Expiration** means state prunes itself: stale quotes vanish, incident scratchpads dissolve after the incident, eval clutter doesn't pile up. **Lifetime Extension** means renewal is an explicit, verifiable act: a listing that gets re-upped, a membership that renews. The strongest submissions differentiate lifetimes per entity type — that's a rubric criterion on its own.

### 6. It's a shared, public database

Every entity is publicly readable, and every write is attributable. Design accordingly: namespace your entities with a project attribute, and keep genuinely private data off Arkiv (or encrypt the payload — the encryption layer is yours to design).

---

## The challenges

Same rubric everywhere — pick the one that excites you, or bring anything to the open lane. The idea seeds below are sparks, not briefs: **build something else if it fits the spirit.** Each numbered challenge accepts submissions only during its own window — the open lane runs all month.

### Challenge 1 · AI & DevTools — submissions Aug 3 – 11 (closes Aug 11, 23:59 UTC) · host: Santiago Zuluaga

Agents and dev tools constantly need shared state that outlives a single run but shouldn't live forever: what's been claimed, what a review found, how an eval scored. Arkiv gives that **ephemeral coordination state** a queryable, time-scoped home with verifiable authorship — no side database, no indexer. And the track is just as open to **developer tools and infrastructure** that help builders or agents model, ingest, inspect, query, or onboard to Arkiv — **improving Arkiv's DevEx and developer adoption is first-class here**, even if your tool touches the chain itself lightly (deep use of Arkiv's primitives is a bonus, not a gate). For those, the schema you're judged on is the one your tool consumes or emits (see the tooling lens in the [rubric](scoring-rubric.md)).

| Idea seed | The hook |
| :-------- | :------- |
| **Agent Handoff Queue** — agents create, claim, update and close work items as Arkiv entities | Query by repo / status / priority / expiry; stale claims expire; creator metadata verifies who made each transition |
| **PR Review Trace** — a GitHub Action stores an agent's findings, fixes and final status per commit | Query by repo / sha / severity; traces live only through the review window; tx hashes make review state auditable |
| **Prompt Run Index** — an eval harness logs prompt inputs, model metadata, scores and failures | Indexed numeric scores + timestamps make regressions queryable; short expiry keeps eval clutter from piling up |
| **Build Recipe Registry** — a searchable registry of build recipes your agent pulls on demand | Recipes indexed by stack / task / version; maintainers update them and readers verify the publisher |
| **Incident Context Board** — a shared incident scratchpad for logs, hypotheses, owners, mitigations | Time-scoped entities fit the incident window; query by service / severity; signed updates keep the timeline verifiable |
| **Entity Schema Explorer** — a devtool that introspects any Arkiv project's entities and shows the schema, relationships and lifetimes builders actually created | A tool-shaped idea: judged on the contract it consumes — scoped queries by project + creator, shared-key link resolution, expiry-aware views no generic DB browser could offer |

**A strong submission:** the problem, the entity + attribute schema, the queries your agent relies on, and why Arkiv beats a plain database. A mock, diagram or pseudocode makes it sing.

### Challenge 2 · Marketplaces — submissions Aug 12 – 20 (closes Aug 20, 23:59 UTC) · host: Marcos Miranda

Marketplaces are mostly state management: what's listed, what's been quoted, what's still available, who said what. Arkiv models each of those as a queryable entity with an expiry and a verifiable creator — inventory filters cleanly and expires itself instead of going stale.

| Idea seed | The hook |
| :-------- | :------- |
| **RFQ Quote Board** — buyers post requests, sellers post quotes; UI filters active quotes | Quotes expire automatically; numeric attributes power price/deadline queries; signer metadata verifies quote origin |
| **Dispute Evidence Packet** — buyers and sellers attach time-bounded evidence entities | Query evidence by orderId and side; kept only through the dispute window; every attachment has a verifiable creator |
| **Availability Slots** — bookings for desks, devices or services with expiring slots | Slots are CRUD entities indexed by location / start / price; expired slots prune themselves instead of rotting as inventory |
| **Bounty Microboard** — open bounties, submissions, reviews and status | Query by skill / reward / deadline / status; owner fields distinguish sponsor, submitter and reviewer |
| **Seller Signal Feed** — short-lived inventory / SLA / capacity signals buyers query before transacting | Time-scoped signals prevent stale claims; attributes make availability filterable; tx-linked updates are verifiable |

**A strong submission:** one marketplace flow end-to-end — the entity schema for a listing/quote, the filters buyers run, how state updates and expires, and where verifiable authorship shows up in the UI.

### Challenge 3 · DeFi — submissions Aug 21 – 31 (closes Aug 31, 23:59 UTC) · host: Shantelle Awomoyi

DeFi generates mountains of state that isn't the swap itself: bids, risk snapshots, oracle candidates, incentive epochs, treasury intents. Arkiv is a good home for that — queryable and tamper-proof, time-scoped to the window it matters in, and explicitly **not** on the execution hot path.

| Idea seed | The hook |
| :-------- | :------- |
| **Auction Evidence Board** — solvers publish bid metadata, fills and dispute evidence per auction window | Query by auctionId / solver / asset / timestamp; evidence expires after the challenge window; creator metadata verifies source |
| **Liquidation Watch Snapshot** — periodic risk-state snapshots for lending positions | Query by market / collateral / healthFactor; snapshots are time-scoped and verifiable, without being execution-critical |
| **Oracle Round Notes** — reporters publish candidate values, sources and challenge status per round | Query by asset / round / status; entries live through the dispute window; signer metadata verifies reporter identity |
| **Incentive Epoch Explorer** — pools publish incentive parameters per epoch | Numeric epoch/pool attributes make incentives filterable; expired epochs prune; updates carry tx hashes |
| **Treasury Intent Feed** — a DAO publishes swap/payment intents and competing quotes before execution | Query active intents by token / size / deadline / status; quotes expire; creators are verifiable before a signer acts |

**A strong submission:** a DeFi concept with an explicit off-hot-path scope — what evidence/state lives as entities, the queries that read it, and how expiry + verifiability become product features.

### The Other lane — open all month (closes Aug 31, 23:59 UTC)

Not every good idea is AI, a marketplace or DeFi. The open lane takes everything else that maps cleanly to Arkiv — registries and RWA, provenance trails, governance state, social graphs, game or world state. The bar is the same: it has to genuinely need queryable, time-scoped, tamper-proof entities, not just any storage.

| Idea seed | The hook |
| :-------- | :------- |
| **On-chain Registry** — domains, licenses, memberships, certificates as queryable entities | Indexed by owner + attributes; expiry models renewals; creator metadata proves who issued each entity |
| **Provenance Trail** — an asset's history as a chain of time-stamped, verifiable entities | Query the full trail by asset id; each step is a signed write; expiry can scope custody windows |
| **Governance Log** — proposals, votes and rationales stored per cycle | Filter by proposal / voter / status; verifiable authorship on every vote; epochs prune old cycles |
| **Social Graph Snippets** — follows, reactions or badges as lightweight, self-expiring entities | Query by actor + type; ephemeral signals stay cheap; owners are verifiable |
| **Game / World State** — off-chain-fast game events mirrored as queryable, verifiable entities | Query by session / player; the expiry fits a match; verifiable results without a central server |

**A strong submission:** a clear pitch for something outside the three named challenges — the entity model, the queries, and a straight answer to "why Arkiv and not a normal database?"

---

## Answer the counterfactual — and name what stays off

The two questions that separate a 3 from a 5 on the rubric:

**"Why Arkiv, not a plain database?"** A plain database is a fine answer for most software. Your idea should have at least one property that materially breaks without Arkiv: authorship a platform can't forge, expiry as a protocol guarantee, an audit trail readers verify themselves, state no single operator can rewrite.

**"What stays off Arkiv?"** Naming it shows you understand the model. Typical answers: hot-path execution, private or heavy payloads, secrets, anything latency-critical. An idea that puts *everything* on Arkiv usually hasn't been thought through.
