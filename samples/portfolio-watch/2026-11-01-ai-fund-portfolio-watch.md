# Sample: portfolio-watch, early-stage AI-focused VC fund

- Skill: portfolio-watch (v1.6.0)
- Date: 2026-11-01
- Tested live against production Synorb over REST, demo key (ends cc41)

The persona is constructed: a platform lead at an early-stage, AI-focused VC fund. The portfolio below is an example list chosen for this test. It is not any real firm's holdings, and the competitor map is the tester's, not a statement about any real investment.

## User request

> I'm a platform lead at an early-stage AI-focused fund. Watch our AI portfolio and their competitors for me, and tell me every week what moved and what I should raise with the founders.

## Conversation (setup turns)

**Agent:** I am checking the connection. I have a free Synorb demo key saved (ends cc41). It has 5 Manifests left and ends Nov 4, and all 5 of its Beacon slots are in use. Which companies should I watch, and may I send their names to Synorb to check coverage? A name search sends only the name.

**User:** Six companies: LangChain, Decagon, OpenRouter, Baseten, E2B and ElevenLabs. None is confidential, search them.

**Agent:** For each one I propose competitors, and you keep the ones you agree with:

- LangChain: CrewAI, LlamaIndex, Letta
- Decagon: Sierra, Parloa
- OpenRouter: Together AI, Fireworks AI
- Baseten: Modal, Together AI
- E2B: Daytona, Modal
- ElevenLabs: Cartesia, Deepgram

**User:** Fine, keep all of those.

**Agent:** Coverage, from 26 free name searches:

- Portfolio: 6 of 6 companies have their own Synorb Stream.
- Competitors: 10 of 11 have one. **Letta has no Stream** (the search read the name as a stock ticker and matched nothing). I will not fill that gap from other companies' posts. You can ask Synorb to add it.
- "Sierra" returned the SEC and Sierra Bancorp first. I kept the AI-agent company Sierra (founded by Bret Taylor and Clay Bavor, by its Stream description) and rejected the bank.

I would like two Beacons, **Portfolio** (6 Streams) and **Competitors** (10 Streams). Your key has no free Beacon slot (5 of 5 are used by the starter Beacons), so I will not save or archive anything. I will run each pull on the same Stream ids, which means this scope is not saved. Saving later needs two free slots.

For the last 8 days (Oct 24 to Oct 31 is the newest window a demo key can see), a count is free:

- Portfolio: 31 items. Competitors: 35 items.

Your key has 5 Manifests. I will read portfolio items first and leave every competitor item unread. One page of 5. Shall I go ahead?

**User:** yes

**Agent:** Done. The watch is below. I read 5 of 66 matched items and one of those 5 was already on this key, so 4 Manifests were billed and 1 is left.

## The watch (Oct 24 to Oct 31)

This is a sample, not full coverage. I read 5 of the 31 portfolio items and none of the 35 competitor items. Everything below is the companies' own publications, which carry what a company says about itself, not independent reporting. Dates run from Oct 24 to Oct 31, the newest window this key can see.

### What needs attention

1. **Decagon opened a partner community and four cloud marketplaces (Oct 30).** The company says Decagon is on AWS, Google Cloud, Databricks and OpenAI marketplaces, and that "eligible customers can apply existing commitments toward Decagon." It also says partners can build on the platform in plain language without an SDK, and that its Voice 3 agent runs on Chord, a speech model built by Decagon Labs. For the fund, this is a distribution change: buyers can pay for Decagon from budgets they already hold. Sierra (4 items) and Parloa (6 items) both published this week, but I did not read them, so I cannot say whether they overlap. [Source](https://decagon.ai/blog/decagon-partner-community)
2. **LangChain added a managed browser to its Managed Deep Agents (Oct 29).** The company reports its browser tools passed 90% of 100 WebVoyager tasks for $1.98 in total (a company-run benchmark, labelled measured). Its post says the tools are built on Stagehand, "Browserbase's open source SDK," and that a handoff lets the user log in so the agent never sees a password. This moves LangChain from a framework toward a hosted runtime. CrewAI (4 items) and LlamaIndex (2 items) published this week; unread. [Source](https://www.langchain.com/blog/browser-use-in-managed-deep-agents)
3. **Baseten published a faster way to sync model weights (Oct 30).** The company reports a 770GB sync fell from about 36 to 15 seconds, with the request pause down from 6 to 0.8 seconds. It also reports that moving the cache offload to host memory raised output throughput per GPU 3.2x at a concurrency of 48, with the hit rate going from 2% to 92%. The use case in the post is reinforcement-learning rollouts on large models. These are Baseten's own measurements. Modal has no items this week; Together AI has 2, unread. [Source](https://www.baseten.co/blog/the-fastest-delta-weight-syncs-in-the-world)

### Portfolio companies

- **LangChain:** the browser post above (Oct 29), plus a `langchain-core` 1.7.2 patch release the same day that fixes a message-merge bug and adds notification metadata ([release](https://github.com/langchain-ai/langchain/releases/tag/langchain-core%3D%3D1.7.2)). 11 items this week; I read 2.
- **Decagon:** the partner community above. It also lists integrations with Databricks, Plaid and Five9, and a partnership with Instinct and Muse "to help businesses prepare for" personal AI agents. Synorb's Brief notes the post did not name any initial partner firms. 3 items; I read 1.
- **OpenRouter:** one item, a how-to tutorial (Oct 31) on building a scheduled agent, which I do not count as a move. It does contain a claim worth knowing: "At DevDay 2026, OpenAI announced Dots, its version of always-on agents" ([source](https://openrouter.ai/blog/tutorials/build-always-on-ai-agent)). 10 items; I read 1.
- **Baseten:** the weight-sync post above. 7 items; I read 1.

### Competitor moves

I did not read any competitor item this run, so I report no competitor moves and claim no threats. What I counted for the window, by the portfolio company it maps to:

| Portfolio company | Competitor (items this week) |
| --- | --- |
| LangChain | CrewAI 4, LlamaIndex 2, Letta no Stream |
| Decagon | Sierra 4, Parloa 6 |
| OpenRouter | Together AI 2, Fireworks AI 0 |
| Baseten | Modal 0, Together AI 2 |
| E2B | Daytona 2, Modal 0 |
| ElevenLabs | Cartesia 14, Deepgram 1 |

Cartesia (14) and Parloa (6) are the most active. Reading them is the first use of any larger allowance.

### Quiet this week

E2B and ElevenLabs published nothing in the window. That is a count of 0 for each, not an item I failed to read.

### Worth raising with the founders

My view, not Synorb's:

- **Decagon:** ask how much of new business now comes through the four marketplaces, since the company says buyers can use existing cloud commitments.
- **LangChain:** ask how it plans to depend on Browserbase's Stagehand now that the browser is a core Managed Deep Agents feature.
- **Baseten:** ask whether reinforcement-learning rollouts are a customer segment or a one-off benchmark.

Your demo key has 1 Manifest left and ends Nov 4. A weekly run needs a free email-bound key (100 Manifests a month, same Beacons). I did not create a schedule in this test. The default would be Mondays at 8:00, `lookback_hours=192`, reporting only items not yet delivered.

## Calls made

Base: https://api.synorb.com. All use `Authorization: Bearer <key ending cc41>`.

1. `GET /account` -> 200. manifests_limit 25, remaining 5, beacons_limit 5, beacons_used 5, `available_through` 2026-10-31.
2. `POST /streams/search` body `{"query": "<name>"}` x26 -> 200 each. Names: LangChain, CrewAI, LlamaIndex, Agno, Decagon, Sierra, Parloa, Harvey, Legora, OpenRouter, Together AI, Fireworks AI, Baseten, Modal, Pinecone, Weaviate, ElevenLabs, Cartesia, Daytona, E2B, Deepgram, AssemblyAI, Browserbase, Letta, Relevance AI, Cognition. 23 returned a strong match, `Letta` returned `none`, `Relevance AI` returned `weak`, and `Sierra` was strong but listed the SEC and Sierra Bancorp first. Not all of these were kept. Agno, Harvey, Legora, Pinecone, Weaviate, AssemblyAI, Browserbase, Relevance AI and Cognition were tried while choosing the list and are not in it.
3. `POST /manifests/query` `{"stream_ids": [6 portfolio ids], "lookback_hours": 192, "mode": "count"}` -> 200. total_count 31 (exact), effective 2026-10-24 to 2026-10-31, billed 0.
4. Same with the 10 competitor Stream ids -> 200. total_count 35, billed 0.
5. 16 more counts, one per Stream, same window -> 200, billed 0. Portfolio: LangChain 11, Decagon 3, OpenRouter 10, Baseten 7, E2B 0, ElevenLabs 0 (sum 31). Competitors: CrewAI 4, LlamaIndex 2, Sierra 4, Parloa 6, Together AI 2, Fireworks AI 0, Modal 0, Daytona 2, Cartesia 14, Deepgram 1 (sum 35). The Skill does not ask for these. I needed them to tell "quiet" from "unread".
6. `POST /manifests/query` `{"stream_ids": [6 portfolio ids], "lookback_hours": 192, "page_size": 5}` -> 200, 176 KB. 5 returned (OpenRouter 1, Baseten 1, Decagon 1, LangChain 2), billed 4, remaining 1. The OpenRouter Manifest had already been received by this key earlier, so it billed 0.

No `POST /v3/beacons`, fork or archive call was made.

## Honest notes

- The persona, the portfolio, the competitor map and the user's replies are written by the tester. The portfolio is not a real firm's holdings.
- The Skill's Step 3 says to save two Beacons. The key had no free slot, so per Step 3.4 nothing was saved or archived and the pull used `stream_ids`. `stream_ids` in `POST /manifests/query` worked as the Skill says.
- With 5 Manifests, one page read 5 of 31 portfolio items and 0 of 35 competitor items. The pull has no ordering parameter. The five returned were dated Oct 29 to Oct 31 and looked newest first, but the server does not promise that. E2B and ElevenLabs could only be called quiet because of the free per-Stream counts.
- The portfolio page came from four of six Streams (LangChain gave two). I did not read any item from OpenRouter beyond one tutorial, so the OpenRouter block says little.
- I read the full Claims and quotes of the three featured items and the Claims of the other two. I did not open the full Brief bodies, only the summaries and open-question lists.
- Refinement decisions (the draft itself is not kept): the OpenRouter tutorial was left out of the attention list because Step 5 drops how-to guides. The Baseten Claim "Kimi K3 can now run on two GB300 nodes" was not used, because its quote says "8:GB300" and disagrees with the Claim text. No overlap with Sierra or Parloa is claimed, because no item from either was read.
- The `langchain-core` release Brief said "No substantive source content was available." I report it only as a release with the three Claims given.
- No schedule or Beacon was created. Step 8 was described, not run.
- No visual was made: the comparison in the Skill's visuals reference needs a numeric series, and this watch has no material one.
