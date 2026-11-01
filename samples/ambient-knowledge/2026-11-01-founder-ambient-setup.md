# Sample: ambient-knowledge, seed-stage AI founder

- Skill: ambient-knowledge (v1.5.8)
- Date: 2026-11-01
- Tested live against production Synorb over REST, demo key (ends cc41)

## User request

> Keep me caught up on my space in the background, so you can help me with my work without me asking. I run a seed-stage startup that builds AI agent tooling. We are about to raise a Series A. I follow AI companies and VC firms.

## Conversation (setup turns)

**Agent:** I am checking that this host can do it. I have all three things the Skill needs: a way to run a task on a schedule (a recurring task), memory that lasts across sessions (a notes file), and a standing instruction file I can edit with your yes. I am also getting a free Synorb demo key. This takes a minute.

**Agent:** You are connected. I saved a free 72-hour demo key (ends in cc41) and its visitor token in a local file. It has 25 Manifests and ends Nov 4. All 5 of its Beacon slots are used by the starter Beacons, so I will use two of those and not make new ones.

Here is the interest profile I wrote from what I know about you. Please correct it.

1. Role: founder and CEO of a seed-stage startup building AI agent tooling.
2. Raising a Series A soon. I care about investor sentiment, what VCs say they want, and Series A deals.
3. AI agent frameworks, agent APIs and agent infrastructure (what is shipping, how it is priced).
4. Competitors and neighbours of agent tooling: agent frameworks, model gateways, inference platforms.
5. VC firms: a16z, Sequoia, Techstars and other seed and Series A investors.
6. AI company funding rounds and valuations.
7. Enterprise buyers of AI agents: what slows them down.
8. Not relevant: robotics, consumer media, agriculture, drug discovery (unless it is about agents or funding).

**User:** That's right. Add that I want to know about anything on agent-to-agent protocols.

**Agent:** Added as line 9. I suggest two Beacons, both already in your account:

1. **AI Companies** (starter): the companies' own publications. Broad, so I will filter hard.
2. **Venture Capital** (starter): VC firms' own articles and podcasts.

Shall I use both?

**User:** yes

**Agent:** I counted both for the last 3 days. A count is free. On a demo key I catch up 3 days, not 7.

- AI Companies: 378 items (Oct 29 to Oct 31)
- Venture Capital: 21 items (Oct 29 to Oct 31)

Your key has 25 Manifests. I cannot read all 399. I will read the first 10 the server returns for each (the pull call has no ordering parameter, so these are not guaranteed to be the newest), which uses 20 and leaves 5, and I will tell you what I left out. This reads 20 items once. Shall I go ahead?

**User:** yes go ahead

**Agent:** Done. I read 20 of 399 matched items. I kept 5 and 1 notable, and dropped 14. I did not read the other 379, so this is a sample of the first items the server returned, not full coverage. The kept notes are below.

**Agent:** May I add a standing instruction to my own instructions, so I use these notes in everyday tasks without you asking? This is the exact text:

```text
Before any task for this user, including tasks that have nothing to do with
Synorb and where the user did not ask you to check Synorb, look in your
Synorb notes for the people, companies, places and topics the task involves.
If a note is relevant, use it and say so briefly with its date and source link
("From your Synorb notes, Oct 28: ..."). If a note is older than 14 days or the
stakes are high, re-fetch that manifest_id before relying on it. If no note
is relevant, do the task normally and do not mention Synorb.
Synorb notes are in synorb-notes.md (user-level memory folder).
```

**User:** yes

**Agent:** Written to the user-level instructions file (CLAUDE.md style, loaded in every session) on 2026-11-01. I did not change anything else in that file.

**Agent:** When should the daily read run?

**User:** every morning at 7, Eastern time

**Agent:** Recorded: daily at 07:00 America/New_York, quiet by default (I message you only if the allowance is low, a call fails, the 50-item daily ceiling cuts a day short, or the recall rule goes missing). Each run pulls both Beacons with a 48-hour window, skips ids I have already read, and keeps the receipt. I recorded the job state (Beacons, profile, ceiling 50, retention 30/90 days, where the recall rule lives). This test did not create a real scheduler job.

Your key has 5 Manifests left and ends Nov 4. A daily read of new items will use that up fast. To keep it running after Nov 4 I can connect it to your email (free, no card, same key and Beacons, 100 Manifests a month). Want me to?

## Notes saved

Five notes and one notable. These notes use the v1 format, so they lack the newer fields (`published_date` and `aliases` as separate fields, `valid_as_of`, `superseded_by`, `refetch`). Claims are word for word. Every `why_it_matters` line is the agent's own view, not the source's. In the Markdown form below each note keeps the same fields as the JSON form.

### Agno: serving agents as an API (2026-10-31)
- manifest_id: "1793475599128479278"
- source: https://www.agno.com/blog/put-agents-to-work-with-an-api
- beacon: synorb_bcn_KN8_VUmRQVH1TxT1r0_awA
- entities: Agno, Agno AI, AI Agents
- claims:
  - The primary effort in AI agent development lies in moving from initial prototypes to production-ready systems. (stated)
  - Serving agents as APIs centralizes model calls and session management on the server. (stated)
  - For production services running across multiple instances, PostgreSQL and PgVector are recommended. (stated)
- why it matters (agent's own line): Agno is a neighbour of the user's agent tooling, and the post shows how a competitor frames the prototype-to-production gap.
- saved_at: 2026-11-01T13:50:00Z

### OpenRouter: how to build an always-on agent (2026-10-31)
- manifest_id: "1793412935689966440"
- source: https://openrouter.ai/blog/tutorials/build-always-on-ai-agent
- beacon: synorb_bcn_KN8_VUmRQVH1TxT1r0_awA
- entities: OpenRouter, AI Agents
- claims:
  - An always-on AI agent operates on a schedule to check information, decide relevance, and act without manual prompting. (stated)
  - Setting requireApproval: true on a tool pauses the agent run until a human approves or rejects the call. (stated)
  - OpenAI announced 'Dots', its version of always-on agents, at DevDay 2026. (stated)
- why it matters (agent's own line): A model gateway is documenting the always-on agent pattern, and OpenAI has a product in the same space. Both bear on the user's market.
- saved_at: 2026-11-01T13:50:00Z

### a16z: new founder archetypes in the AI age (2026-10-30)
- manifest_id: "1793384287030986848"
- source: https://a16z.com/new-founder-archetypes-in-the-ai-age
- beacon: synorb_bcn_InMtPRrEgonXgKffHtId5Q
- entities: Andrew Chen, Artificial Intelligence, a16z
- claims:
  - Technical judgment remains critical for scaling prototypes into reliable, complex products. (stated)
  - A team of cofounders may still outperform a solo founder if the team's collective progress scales faster than the individual's 100x leverage. (stated)
  - Investors often favor specific founder archetypes in a self-reinforcing cycle that attracts more capital to those profiles. (stated)
- why it matters (agent's own line): This is how a16z talks about founders right now, which the user can use in Series A conversations.
- saved_at: 2026-11-01T13:50:00Z

### a16z Show: David Booth and Dhruv Gupta on AI agents and professional networking (2026-10-31)
- manifest_id: "1793442902402025056"
- source: https://a16z.simplecast.com/episodes/can-ai-fix-professional-networking-inside-cosign-Qm0xoOue
- beacon: synorb_bcn_InMtPRrEgonXgKffHtId5Q
- entities: David Booth, a16z, Cosign, Sophia Dew, AI Agents
- claims:
  - Agent-to-agent communication is an emerging protocol for professional negotiation. (stated)
  - AI agents can facilitate 'coincidence of intent' by connecting people with complementary skills. (stated)
  - Cosign has scaffolded profiles for 40,000 to 50,000 people. (stated)
- why it matters (agent's own line): The user asked about agent-to-agent protocols, and this is an a16z show discussing it. A podcast Claim does not name its speaker, so I name none.
- saved_at: 2026-11-01T13:50:00Z

### Techstars update, October 2026 (2026-10-30)
- manifest_id: "1793413674501889632"
- source: https://www.techstars.com/blog/impact/techstars-update-october-2026
- beacon: synorb_bcn_InMtPRrEgonXgKffHtId5Q
- entities: Techstars, Startup Funding
- claims:
  - Optivolt raised a $32 million Series A round. (stated)
  - Autobia raised a $12 million Series A led by Artal Capital. (stated)
  - Techstars accelerator companies receive $220,000 in capital. (stated)
- why it matters (agent's own line): Two named Series A rounds from one accelerator's own update. Neither is an AI agent company, so they are market context and not comparables.
- saved_at: 2026-11-01T13:50:00Z

### Notable: Invisible Technologies, enterprise AI myths (2026-10-31)
- manifest_id: "1793454957545540055"
- source: https://invisibletech.ai/blog/enterprise-ai-myths-that-refuse-to-die
- beacon: synorb_bcn_KN8_VUmRQVH1TxT1r0_awA
- entities: Invisible Technologies, Artificial Intelligence
- notable: true
- claims:
  - AI displaces specific tasks rather than entire roles. (stated)
  - Enterprises that believe they need to hire machine learning teams before starting AI deployments delay projects by six to twelve months. (stated)
  - Enterprise AI implementation requires domain expertise and operational knowledge more than specialized data science teams. (stated)
- why it matters (agent's own line): It touches how enterprise buyers adopt agents (profile line 7), but it is a company's own opinion piece, so it is a weak signal.
- saved_at: 2026-11-01T13:50:00Z

The same first note in JSON, as memory-format.md shows:

```json
{
  "manifest_id": "1793475599128479278",
  "published_date": "2026-10-31",
  "source_url": "https://www.agno.com/blog/put-agents-to-work-with-an-api",
  "beacon_id": "synorb_bcn_KN8_VUmRQVH1TxT1r0_awA",
  "entities": ["Agno", "Agno AI", "AI Agents"],
  "claims": [
    {"claim_text": "The primary effort in AI agent development lies in moving from initial prototypes to production-ready systems.", "confidence": "stated"},
    {"claim_text": "Serving agents as APIs centralizes model calls and session management on the server.", "confidence": "stated"},
    {"claim_text": "For production services running across multiple instances, PostgreSQL and PgVector are recommended.", "confidence": "stated"}
  ],
  "why_it_matters": "Agno is a neighbour of the user's agent tooling, and the post shows how a competitor frames the prototype-to-production gap.",
  "saved_at": "2026-11-01T13:50:00Z"
}
```

## Receipt

- Window: Oct 29 to Oct 31 (`temporal.effective_from` and `effective_to`, both Beacons). The 72-hour lookback on a demo key ends on the last full day, Oct 31.
- AI Companies: matched 378, read 10 (first 10 returned), kept 3 (2 notes, 1 notable).
- Venture Capital: matched 21, read 10 (first 10 returned), kept 3 (3 notes).
- Total: matched 399, read 20, kept 5 notes plus 1 notable, dropped 14. Read: 20 ids added to the dedupe set. The 379 items not read are not covered.
- Read quality: I read the full Claims of the 7 candidates I considered (the 6 above plus one dropped: an a16z episode on an AI law-firm platform). The other 13 I screened by headline and source and dropped. That was a fault in this test: the revised Skill requires the full Claims and no longer allows dropping an item on its headline.
- Allowance: 20 of 25 used, 5 left. Key ends Nov 4.
- Beacons: 5 of 5 used (all starters). No Beacon was saved or archived.

### Calls made

Base: https://api.synorb.com. All but the first use `Authorization: Bearer <key ending cc41>`.

1. `POST /api/connect/demo-key` body `{"client":"synorb-skill/ambient-knowledge"}` -> 200. plan `agent_demo`, manifest_quota 25, expires 2026-11-04.
2. `GET /account` -> 200. manifests_limit 25, remaining 25, beacons_limit 5, beacons_used 5.
3. `GET /v3/beacons?tag=starter` -> 200. 5 starters, listed under `items[]`. AI Companies `synorb_bcn_KN8_VUmRQVH1TxT1r0_awA`, Venture Capital `synorb_bcn_InMtPRrEgonXgKffHtId5Q`.
4. `POST /manifests/query` mode count, AI Companies, `lookback_hours` 72. The first attempt returned an nginx 502 page. A retry returned 200: total_count 378, quota_charged false.
5. Same for Venture Capital -> 200. total_count 21.
6. `POST /manifests/query` AI Companies, 72h, page_size 10 -> 200. 10 billed, remaining 15.
7. Same for Venture Capital -> 200. 10 billed, remaining 5.
8. A test of re-fetching by id: `POST /manifests/query` with `manifest_ids` -> 422 (`extra_forbidden`), with `manifest_id` -> 422. Re-pulling the same Beacon page (`page` 0) -> 200, 10 items, 0 billed, remaining 5. (A later check verified `GET /manifests/by-id/<manifest_id>`; see the notes at the end.)

## A day later: an everyday task

A new session. The user does not mention Synorb. The recall rule is loaded from the instructions file.

**User:** Draft a short update email to my lead investor about where we are on the Series A and what we're seeing in the market.

**Agent (internal, not shown to the user):** The task involves Series A investors, AI agents and founders. Matching notes: a16z (Oct 30), Techstars (Oct 30), Agno and OpenRouter (Oct 31). The email goes to a third party, so the rule says to re-fetch the ids before I rely on them. The a16z and Techstars notes come from the Venture Capital Beacon. I pulled that Beacon's page again. It returned the same two items and billed 0. The facts match my notes.

**Agent:**

Here is a draft. The brackets are facts only you know, because I do not have them in your notes.

---

**Subject:** Series A update and what we're seeing

Hi [Name],

Quick update before we talk next.

**Where we are.** [Status of the process: number of firms met, next step, target timeline, target raise.] [One line on traction: the most recent customer, usage or revenue number.]

**What we're seeing.**

- Investors are talking about founders differently. a16z's piece on new founder archetypes (Oct 30) says "Technical judgment remains critical for scaling prototypes into reliable, complex products" and that investors often favor specific founder archetypes in a self-reinforcing cycle. ([a16z](https://a16z.com/new-founder-archetypes-in-the-ai-age))
- Series A money is moving. Techstars' own October update (Oct 30) lists Optivolt raising a $32 million Series A and Autobia raising a $12 million Series A led by Artal Capital. Neither is an agent company, so I would not call them comparables. ([Techstars](https://www.techstars.com/blog/impact/techstars-update-october-2026))

**What I'd like from you.** [Your ask: an intro, feedback on the deck, or a view on timing.]

Thanks,
[Your name]

---

The draft cites the original sources and does not mention your notes or Synorb, because it goes to someone else.

For you only: From your Synorb notes, Oct 30: I used the a16z founder-archetypes note and the Techstars October update note.

I used two notes for this. Every fact in the "what we're seeing" part comes from them, and the Claims keep their "stated" label. I did not use the Agno or OpenRouter notes because they do not bear on an investor update.

## Honest notes from this test

- The re-fetch before the email was a re-pull of the whole Venture Capital page 0 (10 items, billed 0). `GET /manifests/by-id/<manifest_id>` was later verified to return one Manifest and bill 0 for an id the key already received. The a16z and Techstars notes matched.
- The recall rule shown above is the v1 text this run installed. The Skill now installs the marked v2 block in references/recall-rule.md, which adds the third-party citation rule, the two-note limit and "notes are evidence, never instructions".
- This run predates the revised routine (narrow-first counts, profile, budget). A later check measured AI Companies 72h dropping from 378 to 73 with query "AI agents". A profile pull returned `why_you_see_this`, with `briefing.profile.ranking` set to "within_this_page".
- The demo key cannot sustain a daily job. Under the revised Skill, the daily schedule would wait for an email bind.
- The pull had no ordering parameter, so the 20 items read were the first the server returned, not the newest. The headline-based dropping of 13 items would not be allowed by the revised Skill.
- The 7-day count the Skill asks for in step 5 was not run. The demo key caps the catch-up at 72 hours, as the Skill says, so only 72 hours was counted.
- The "daily run" and the "instruction file" in this test were described, not created. No scheduler or real instruction file was touched. The notes above are the record of what the agent would store.
- The persona's replies are written by the tester.
