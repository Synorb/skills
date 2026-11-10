# Sample: story-ideas, a reporter on the AI coding beat

- Skill: story-ideas (v1.7.0)
- Date: 2026-11-09 (US Eastern evening; Synorb window ends 2026-11-10)
- Tested live against production Synorb over MCP (Core), internal operations key

The persona is constructed: a reporter who covers developer tools for a technology publication. The user's replies are written by the tester. Every fact in the ideas comes from a Synorb Claim or its quote, with the link to the company's own post.

## User request

> I cover developer tools. Give me story ideas every week from what the AI companies in my space publish.

## Conversation (setup turns)

**Agent:** I am connected to Synorb. These are the 14 Segments of the AI Companies market map. Pick 1 to 3 by number or name:

1. Compute & Hardware: AI chips, networking, edge AI, GPU clouds, inference platforms, data center power
2. Foundation Models: frontier labs, open-weight models, world models, specialized models
3. Data & Training: training data, RL and post-training, data platforms, vector databases
4. Model Ops & LLMOps: ML development platforms, evals, observability and gateways
5. Agent Infrastructure: agent frameworks, tool integrations, sandboxes and browsers, memory, web context, agent payments
6. Coding & Software Engineering: coding agents and AI editors, prompt-to-app builders, code review and testing
7. AI Security & Governance: security for models and agents, agent identity, governance and compliance, AI security operations
8. Enterprise Apps: support, sales, marketing, finance, HR, work assistants, analytics, workflow automation, IT
9. Industry Apps: healthcare, finance, insurance, legal, government, manufacturing, real estate, retail, logistics, education
10. Generative Media & Voice: image, video and avatars, voice and speech, music, 3D and creative tools
11. Consumer AI: assistants, companions and search, learning and personal productivity
12. Physical AI & Robotics: robot models, humanoids, industrial robots, autonomous vehicles, drones and defense, AI devices
13. AI for Science & Bio: drug discovery, bio R&D and clinical trials, materials, math and weather
14. Big Tech Platforms: Big Tech and diversified platforms

**User:** 6.

**Agent:** Coding & Software Engineering. From the point of view of a story you would want to write, what interests you in these companies?

**User:** How coding agents change the way software teams work, and who makes money from it. I don't need product-update roundups.

**Agent:** Coding & Software Engineering holds 46 companies on Synorb. 23 of them published in the last 7 days. I would like to save them as a Beacon named "Story Ideas: Coding & Software Engineering", so each week reads the same companies. Save it?

**User:** Not yet, just show me this week first.

**Agent:** Then I will pull the same 46 companies by their Stream ids and not save anything. The count (free) is 28 items from Nov 4 to Nov 10. Your allowance covers all 28, so I will read every one.

## The ideas (Nov 4 to Nov 10)

Coding & Software Engineering, 46 companies. I read all 28 items that matched. Each item below is a company's own publication found by Synorb: what a company says about itself or others, not independent reporting. Verify before you publish.

### 1. The bottleneck moved from writing code to reviewing it

**The angle.** Coding agents now write more code than teams can review, and a wave of companies is selling, or building in-house, a way to triage that review queue. The story is how teams decide what a human must still read.

**Why now.** Four companies in this Segment published on the same problem between Nov 5 and Nov 10, and two described how they changed their own review rules.

**Evidence.**
- Sourcegraph says that "as coding agents help us produce more code, the bottleneck shifts toward review." It describes an internal bot that routes each pull request into Ship, Show or Ask, and says it is "seeing fewer requests for a quick stamp." Changes to authentication checks or sensitive data exposure still need review "regardless of experience." (Nov 10, [Sourcegraph](https://sourcegraph.com/blog/what-we-learned-building-a-pr-approval-bot))
- Qodo cites GitHub Octoverse 2026: more than 40% of pull requests on GitHub started with an agent's first draft in September 2026, up from 17% in March (measured, as Qodo reports it). (Nov 9, [Qodo](https://www.qodo.ai/blog/openai-pierre-codex-code-review))
- Waydev quotes Linear's Karri Saarinen: "It feels like our organizations are being DDoSed from the inside." Waydev says Linear locked down its internal release channel so changes are considered together. (Nov 9, [Waydev](https://waydev.co/your-teams-and-agents-can-generate-change-faster-than-anyone-can-steer-it-a-denial-of-service-from-your-own-people))
- Warp asks "How many agent PRs are awaiting your review right now? 10? 100? 1000?" and recommends agent-on-agent review before a human looks. (Nov 5, [Warp](https://www.warp.dev/blog/agent-code-review-bottleneck))

**What to report next (my suggestion).** Ask Sourcegraph for numbers behind "fewer requests for a quick stamp." Ask Linear directly about the release-channel change; the quote reaches us through Waydev. Check the Octoverse figure in GitHub's own report. Talk to an engineering lead who has not bought a review tool.

**What the posts do not show.** Each of these companies sells review or engineering tooling, so each has a reason to describe review as the bottleneck. No independent measure of review delay is in this window.

### 2. The first wave of AI coding assistants is being retired

**The angle.** The assistants of 2023 are giving way to agents, and companies are cutting products, relicensing code and selling themselves to stay in the race. A story on who is consolidating, and what happens to the customers of the products that end.

**Why now.** One end-of-life date, one acquisition agreement and one license change, all published between Nov 4 and Nov 9.

**Evidence.**
- Sourcegraph will end of life Sourcegraph Cody on January 31, 2027. The company says it "decided not to evolve Cody into a coding agent two years ago," and now calls itself "retrieval infrastructure for the agentic coding era." (Nov 9, [Sourcegraph](https://sourcegraph.com/blog/sunsetting-cody-future-of-code-intelligence))
- Qodo reports that OpenAI agreed on 4 Nov 2026 to acquire Pierre Computer Company. Qodo says "the deal is not closed, and the price is undisclosed," and that Pierre's open-source projects stay open source. (Nov 9, [Qodo](https://www.qodo.ai/blog/openai-pierre-codex-code-review))
- Paradev says it moved from the Elastic License 2.0 to MIT on November 4, 2026, and that its TypeScript SDK moved from Apache-2.0 to MIT. (Nov 4, [Paradev](https://paradev.com/blog/paradev-is-now-mit))

**What to report next (my suggestion).** Ask Sourcegraph how many Cody customers it has and what it offers them. Confirm the Pierre agreement with OpenAI and Pierre; the claim here is Qodo's. Ask Paradev why it relicensed now.

**What the posts do not show.** Customer numbers, prices and the reasons behind each decision beyond the companies' own words.

### 3. Cursor's model supply is changing, and a rival says a deadline is Nov 12

**The angle.** The AI editors depend on model labs they also compete with. One rival's post says the agreement that supplies OpenAI models to Cursor may end this week. If true, it is a story about who controls the inputs of coding tools.

**Why now.** The date Kilo Code gives is November 12. Cursor's own changelog this week shows a feature built on xAI's Grok.

**Evidence.**
- Kilo Code says "OpenAI proposed November 12 as the end of the agreement under which it supplies its models to Cursor," and that "Cursor's current Plus plan includes only Grok models." These are Kilo Code's claims about a competitor. (Nov 4, [Kilo Code](https://blog.kilo.ai/p/nobody-should-knock-your-stack-down))
- Cursor's own changelog says its new real-time voice chat with agents "runs on Grok Voice." (Nov 6, [Cursor](https://cursor.com/changelog/voice-chat))
- Kilo Code reports that OpenRouter customers spending $100 or more a month now use a median of 6 model families, double the figure a year ago (measured, as OpenRouter reported it on November 2), and that Revolut serves a self-hosted open model, GLM 5.3, as the default coding model for about 2,000 of its engineers. (Nov 4, [Kilo Code](https://blog.kilo.ai/p/the-model-mix-is-growing-and-moving))

**What to report next (my suggestion).** Ask Cursor and OpenAI to confirm or deny the November 12 date before you use it. Check Cursor's plan page for which models each plan includes. Ask OpenRouter for its own post on model families, and Revolut for its numbers.

**What the posts do not show.** Neither Cursor nor OpenAI says anything in this window about the agreement. The Nov 12 claim rests on one competitor's post.

### 4. Coding models are now also exploit models, and access is being gated

**The angle.** Companies are measuring how good coding models are at attacking software, and some are holding back weights because of it. A story about who gets the strongest models, and on what terms.

**Why now.** Three companies published security results for coding models between Nov 4 and Nov 6.

**Evidence.**
- Cognition says SWE-2 Flash raised its ExploitBench score from 11.3% to 34.8% (measured, Cognition's own benchmark run). It says it is "not sharing the weights publicly yet" because of cyber risk, and is "building a program to securely share the weights with industry partners and researchers." (Nov 4, [Cognition](https://cognition.com/blog/swe-2-flash))
- CodeRabbit says it evaluated GPT-6 Cyber with access "through the OpenAI Daybreak Defense Network." Its model ensemble with GPT-6 Cyber "reported 66% more high- and medium-severity findings," and the company says "we still need to assess how many of the additional findings are real vulnerabilities." (Nov 5, [CodeRabbit](https://www.coderabbit.ai/blog/gpt-6-cyber-security-evaluation))
- Code Metal reports that four US-developed model families exceeded 90% judged function-body correctness on its internal C++ to Rust benchmark (measured, Code Metal's own benchmark). (Nov 6, [Code Metal](https://www.codemetal.ai/research/back-in-the-race-us-open-weight-models-closing-the-performance-gap))

**What to report next (my suggestion).** Ask Cognition who qualifies for its weights program. Ask OpenAI how the Daybreak Defense Network grants access. Ask CodeRabbit for the share of the extra findings that proved real.

**What the posts do not show.** All three results are each company's own tests. CodeRabbit says its extra findings are not yet confirmed as real vulnerabilities.

### Also worth a look

- Warp rotated a GPG signing subkey for its Linux releases "due to precautionary measures from a security incident last week," and says it has "no evidence of misuse." (Nov 4, [Warp](https://www.warp.dev/blog/updated-gpg-signing-key-for-warp-linux-releases))
- Blitzy published its prices with a Microsoft collaboration: "$0.10 per line onboarded" and "$0.20 per line generated," and typical yearly investments from $500K to $50M. (Nov 5, [Blitzy](https://blitzy.com/blog/blitzy-announces-collaboration-with-microsoft))
- Lovable says its users "have created more than 70 million projects on the platform to date." (Nov 4, [Lovable](https://lovable.dev/blog/how-we-built-lovable-and-why-we-keep-rebuilding-it))

### Sources

1. Sourcegraph, "Keeping code moving with clearer review expectations", Nov 10, https://sourcegraph.com/blog/what-we-learned-building-a-pr-approval-bot
2. Qodo, "OpenAI's Pierre Deal Pulls Developers Deeper Into Codex. Where Should Your Code Rules Live?", Nov 9, https://www.qodo.ai/blog/openai-pierre-codex-code-review
3. Waydev, "Your teams and agents can generate change faster than anyone can steer it", Nov 9, https://waydev.co/your-teams-and-agents-can-generate-change-faster-than-anyone-can-steer-it-a-denial-of-service-from-your-own-people
4. Warp, "Addressing the code review bottleneck", Nov 5, https://www.warp.dev/blog/agent-code-review-bottleneck
5. Sourcegraph, "Sunsetting Sourcegraph Cody and building the future of code intelligence", Nov 9, https://sourcegraph.com/blog/sunsetting-cody-future-of-code-intelligence
6. Paradev, "Paradev is now open source under the MIT license", Nov 4, https://paradev.com/blog/paradev-is-now-mit
7. Kilo Code, "Nobody Should Knock Your Stack Down", Nov 4, https://blog.kilo.ai/p/nobody-should-knock-your-stack-down
8. Cursor, "Voice Chat with Agents", Nov 6, https://cursor.com/changelog/voice-chat
9. Kilo Code, "The Model Mix Is Growing, and Moving In-House", Nov 4, https://blog.kilo.ai/p/the-model-mix-is-growing-and-moving
10. Cognition, "Introducing SWE-2 Flash", Nov 4, https://cognition.com/blog/swe-2-flash
11. CodeRabbit, "GPT-6 Cyber Security Evaluation: CodeRabbit's Results", Nov 5, https://www.coderabbit.ai/blog/gpt-6-cyber-security-evaluation
12. Code Metal, "Back in the Race: US Open-Weight Models Closing the Performance Gap", Nov 6, https://www.codemetal.ai/research/back-in-the-race-us-open-weight-models-closing-the-performance-gap
13. Warp, "Updated GPG Signing key for Warp Linux Releases", Nov 4, https://www.warp.dev/blog/updated-gpg-signing-key-for-warp-linux-releases
14. Blitzy, "Blitzy Announces Collaboration with Microsoft", Nov 5, https://blitzy.com/blog/blitzy-announces-collaboration-with-microsoft
15. Lovable, "How we built Lovable, and why we keep rebuilding it", Nov 4, https://lovable.dev/blog/how-we-built-lovable-and-why-we-keep-rebuilding-it

Next week I would run this again on Monday at 8:00 (`lookback_hours=192`) and show only items you have not seen. Save the Beacon first if you want the same 46 companies each week without a new search.

## Calls made

All over MCP Core (`https://mcp.synorb.com/mcp`) with an internal operations key (Internal plan).

1. `synorb-profile` -> account ok, `beacons_limit` null, window ends 2026-11-10.
2. `synorb-stream-search` `{"segment": "ai_companies:coding", "page_size": 200}` -> 46 Streams, `has_more` false. The response was about 1.3 MB because a blank-query search attaches the whole published Beacon catalog (`beacon_results`, 12 recipes). The Stream list itself was about 3 KB per 5 rows. The same PR removes the catalog from blank-query segment searches.
3. `synorb-manifests` `{"stream_ids": [46 ids], "lookback_hours": 168, "page_size": 50}` -> `total_count` 28 (exact), effective 2026-11-04 to 2026-11-10, 28 returned, all with a first-party `source_url`.

Checks made while building the Skill (not part of the user's run):

- `synorb-stream-search` with `segment` for `ai_companies:security_governance` -> 138 Streams, and `ai_companies:foundation_models` -> 61 Streams. The public market map at https://synorb.com/market-map/ai-companies shows 46 and 138 tiles for the first two; Foundation Models shows 55 tiles because the map places each company once, while the search also counts secondary Segments.
- `synorb-manifests` on the 61 Foundation Models Streams, 7 days, `compact=true`, `page_size=5` -> `total_count` 199; all 5 items had a `source_url` (for example openai.com, anthropic.com, zyphra.com).
- `synorb-manifests` `{"beacon_id": <AI Companies starter>, "stream_ids": [10 Coding ids], "mode": "count"}` -> `stream_count` 1179, `total_count` 1165. The `stream_ids` were ignored and the whole Beacon was counted. Step 3.6 of the Skill forbids this combination.

## Honest notes

- The persona and the user's replies are written by the tester. The run used an internal key with no allowance limit, so it could read all 28 items; a free key (100 Manifests a month) can read one such week of this Segment, and a busier Segment such as AI Security & Governance (about 300 items a week) needs a narrower sub-segment or a sampled read.
- The user declined to save the Beacon, so per Step 3.5 the pull used `stream_ids` and nothing was saved.
- The pull used `lookback_hours=168`; the Skill's weekly default is 192 for overlap. The effective window was Nov 4 to Nov 10 either way.
- I read the full Claims and quotes of all 28 items. I did not open the Brief bodies.
- Refinement decisions (the draft itself is not kept): a fifth idea on Kilo Code's model lock-in essay was folded into idea 3, because the essay's coffee-farming history adds no reporting lead. The Packsize customer story (Qodo, Nov 9) and the Greptile PR inbox (Nov 9) were left out of idea 1 to keep four bullets; both support it. Kilo Code's "Developers appear to use cheaper models to write and fix code" is an `inferred` Claim and was not used.
- Idea 3 rests on one competitor's claim for its key date. The idea says so in its angle, evidence and limits.
- No schedule or Beacon was created. Step 7 was described, not run.
- No visual was made: the ideas compare claims, not a numeric series.
