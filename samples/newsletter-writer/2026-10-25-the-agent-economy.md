# Sample: newsletter-writer

- Skill: newsletter-writer 1.0.0
- Date: 2026-10-25
- Tested live against production Synorb over REST, demo key (no MCP tools).
- Beacons used: AI Companies (`synorb_bcn_dtv22kVe0RPL0Y7wpA_ZuQ`) and Business & Technology Podcasts (`synorb_bcn_cA10tPsx057wKbsJmRExMg`), both starter Beacons.
- Window: `lookback_hours=168` (7 days). Items published 22 to 24 October 2026.

## User request

"Write this week's issue of my newsletter, The Agent Economy, for AI founders and early-stage investors. Here's how I write: 'Three things mattered this week. None of them were model launches. Money is moving to the application layer, and the people writing the checks are saying so out loud.' Use the AI companies and podcasts you have."

## The issue

# The Agent Economy: Follow the checks

*18 to 25 October 2026*

Three things mattered this week. None of them were model launches. Money is moving to the application layer, and the people writing the checks are saying so out loud.

Legora raised big on top of someone else's model. Higgsfield took new money from NVIDIA and TCV. And a16z's Ben Horowitz said where he thinks the durable edge sits. One voice pushed the other way, and I give it space below.

## Money

### Legora raises $550 million without training its own model

Legora announced a $550 million Series E at an $8.8 billion post-money valuation. Atreides Management led the round. The company says it builds on the best frontier models and does not train its own general legal model. It also says it was the first large legal AI company to offer consumption-based pricing, and that it now employs more than 150 legal engineers. ([Legora Blog](https://legora.com/blog/scaling-fast-built-to-last), 23 Oct)

*My view:* this is the thesis in one paragraph. A $550 million round for a company that builds on other people's models. Note that every figure here is Legora's own, from its own post.

### Higgsfield adds TCV and NVIDIA, and says it passed $1 billion in run rate

Higgsfield extended its Series B with new investment from TCV and NVIDIA. The company says it crossed $1 billion in annualized revenue run rate in September, 18 months after launch. It also reports more than 40 million users across 238 countries and territories, and enterprise growth of more than 100% month over month. These are company-reported figures from its own blog. ([Higgsfield Blog](https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia), 23 Oct)

## Ideas

### Horowitz: the moat is data, not the model

On the a16z show, Ben Horowitz argues that durable advantage in AI applications comes from proprietary data and customer possession, not just model architecture. The episode also says AI applications can reach huge user numbers fast because they do not depend on network-effect adoption curves. Treat both as Synorb's reading of the conversation, not verbatim quotes. ([A16Z Podcasts - The a16z Show](https://a16z.simplecast.com/episodes/what-it-takes-to-win-as-a-founder-ben-horowitz-AjG_7MSY), 24 Oct)

### The counterpoint: Naveen Rao on 20VC

Not everyone is betting on apps. In the 20VC episode with Naveen Rao, the stated view is that the inference market will be a $10 trillion market within 10 years, that robotics will be 100 times larger than the market for coding agents, and that pure software investing is becoming much less viable than hardware-centric AI investing. Energy supply is named as the main bottleneck for AI scaling. ([20VC Podcast](https://thetwentyminutevc.libsyn.com/20vc-why-robotics-will-be-100x-bigger-than-coding-agents-inference-will-be-a-10trn-market-what-no-one-sees-why-software-investors-are-f-today-with-naveen-rao-unconventional), 24 Oct)

*My view:* if you are raising an application-layer round, expect to hear this objection in the room.

## Quick hits

- On the All-In podcast, one claim was that 1% of companies represent 90% of all AI spending, and that 80% of that 90% comes from unprofitable VC-backed companies. ([Official All-In Podcast](https://allinchamathjason.libsyn.com/ai-cyber-panic-ken-griffins-bubble-warning-the-fall-of-france), 23 Oct)
- Ex-Twitter CEO Parag Agrawal, on Sourcery, forecasts that AI agents will eventually use the web 5,000x to 10,000x more than humans. ([Sourcery - Official Podcast](https://podcasters.spotify.com/pod/show/sourcery/episodes/Ex-Twitter-CEO-Says-Were-Underestimating-AI-Agents-by-10-000x-e3r0fd5), 24 Oct)
- The U.S. Navy awarded Applied Intuition a production contract to deploy AI data infrastructure. The first deployment covers five Arleigh Burke-class destroyers. ([Applied Intuition - Official Newsroom](https://www.appliedintuition.com/press-releases/navy-selects-applied-intuition-field-ai-perception), 22 Oct)
- Kalshi's CEO said on Bloomberg that the company is expanding into compute and inflation futures. ([Bloomberg Podcast](https://omny.fm/shows/bloomberg-talks/kalshi-ceo-tarek-mansour-talks-prediction-markets-in-elections), 23 Oct)
- IBM reported Q3 2026 revenue of $17.1 billion. Software revenue was $7.8 billion, up 9% at constant currency. ([The Motley Fool, earnings call transcript](https://www.fool.com/earnings/call-transcripts/2026/10/21/ibm-ibm-q3-2026-earnings-call-transcript), 22 Oct)

---

Sources via [Synorb](https://synorb.com). Every item links to its original publisher.

## Message after the issue

I used your opening as written and kept the voice plain and short. I had only that paragraph as a sample, so tell me if you want it drier or warmer. Note that Naveen Rao pushes against your thesis, so I kept him in as a counterpoint. I cannot schedule from this runtime, so I cannot write this every Monday for you; you would need to set that up in your own tool.

Your Synorb demo is almost used up (5 of 25 Manifests left, ends Oct 28). Connect your email to keep the daily updates running - free, no card. Want me to set it up?

## Calls made

Base `https://api.synorb.com`. Key sent as Bearer (last 4 chars f752).

| # | Method and path | Body | Result | total_count | Quota remaining |
| --- | --- | --- | --- | --- | --- |
| 1 | POST /api/connect/demo-key | `{"client":"synorb-skill/newsletter-writer"}` | 200 | n/a | 25 of 25 |
| 2 | GET /account | none | 200 | n/a | 25 |
| 3 | GET /v3/beacons | none | 200, 3 starter Beacons | 3 | n/a |
| 4 | POST /manifests/query | `{"beacon_id":"<AI Companies>","lookback_hours":168,"mode":"count"}` | 200 | 864 | 25 |
| 5 | POST /manifests/query | same, Podcasts Beacon | 200 | 152 | 25 |
| 6 | POST /manifests/query | same, Central Banks Beacon (not used) | 200 | 327 | 25 |
| 7 | POST /manifests/query | AI Companies, `page_size:10`, `markdown_version:"2"` | 200 but `execution_status: planning_failed`, 0 manifests (`stream_not_yet_queryable`) | null | 25 |
| 8 | POST /manifests/query | Podcasts, `page_size:10`, `markdown_version:"2"` | same failure | null | 25 |
| 9 | POST /manifests/query | AI Companies, `page_size:10`, no `markdown_version` | 200, 10 manifests | 864 | 15 |
| 10 | POST /manifests/query | Podcasts, `page_size:10`, no `markdown_version` | 200, 10 manifests | 152 | 5 |
| 11 | Repeat checks of 7, plus `markdown_version` as integer 2 | n/a | Same failure for the string; the integer gives 422 | n/a | unchanged |

Two calls in the middle (a count and a pull with no `page_size`) returned an nginx `502 Bad Gateway` HTML page once and were not retried.
