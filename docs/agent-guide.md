# Agent Guide — arm your AI with the Ideathon MCP

Using an AI assistant to develop your idea is allowed and encouraged. But an agent that
doesn't know Arkiv will guess — inventing API calls and generic "blockchain storage"
designs. One connection fixes that.

---

## 1. Connect the Ideathon MCP (one URL, no key)

Point Claude, Cursor, or any MCP client at the event's read-only server:

```
https://arkiv-ideathon-mcp.vercel.app/api/mcp
```

```bash
# Claude Code
claude mcp add --transport http arkiv-ideathon https://arkiv-ideathon-mcp.vercel.app/api/mcp

# Cursor / any MCP client (mcp.json)
{ "arkiv-ideathon": { "url": "https://arkiv-ideathon-mcp.vercel.app/api/mcp" } }
```

Your agent gets the four tracks with their briefs and idea seeds, the official rules,
the **exact 100-point judging rubric**, Arkiv fundamentals (entities, typed attributes,
queries, Entity Expiration, verifiable ownership) and the current network status. No
wallet, no key, nothing to deploy — this is an ideathon.

Then try:

> Add the Arkiv Ideathon MCP to my tools, then list its tools, resources and prompts so
> we know exactly what context we have.

## 2. Work the tracks with real context

> Using the Ideathon MCP, pull the brief for the track that fits my idea and tell me the
> 3 things the rubric rewards most.

Tools: `list_tracks` (start here) · `get_doc` (full docs: ideation-guide · rubric · rules ·
faq · ideathon-overview · arkiv-fundamentals · network-status · agent-guide) · `search_kb`
(keyword search across everything).

## 3. Pressure-test with the built-in idea coach

The `review_my_idea` prompt coaches your idea instead of scoring it: it reads your draft,
places it on a readiness band (**Early / Shaping / Submission-ready**), and asks the 3–5
highest-leverage questions across the angles judges will look at — the Arkiv
counterfactual, data & query design, growth, DevEx, scalability, scope, uniqueness.
Answer its questions, iterate, then submit sharp. (Judges score separately, with the
rubric — the coach never emits points.)

> Run the Ideathon MCP's review_my_idea prompt on my idea and ask me the questions that
> make it stronger.

In Claude Code it's also a slash command: `/arkiv-ideathon:review_my_idea`

---

## Prompts that produce strong submissions

Once your agent has the context, work the form's own questions:

> Here's my idea: [pitch]. Design the Arkiv entity schema — entity types, typed
> attributes (numeric where I'll need range queries), and how entities link via shared
> attribute keys.

> Which 2–3 queries does this product live on? Write them as filters (eq / gt / lt),
> with pagination where result sets grow.

> Propose an expiry per entity type — what's short-lived, what gets extended, and why.
> Where do `$creator` / `$owner` show up as user-facing features?

> Steelman the counterfactual: would a plain Postgres do? What materially breaks without
> Arkiv? And what should deliberately stay OFF Arkiv?

That last prompt is one of the rubric's heaviest criteria. If your agent can't answer
it, the idea isn't ready.

## More Arkiv, if you want it

- Docs: [docs.arkiv.network](https://docs.arkiv.network)
- Build-recipe skills your agent pulls on demand: [arkiv-hub.vercel.app/skills](https://arkiv-hub.vercel.app/skills)
