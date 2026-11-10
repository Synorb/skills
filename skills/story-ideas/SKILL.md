---
name: story-ideas
description: Weekly story ideas for a journalist who covers AI companies. The user picks 1 to 3 Segments of the Synorb AI Companies market map (for example Coding & Software Engineering or AI Security & Governance) and says what kind of story they want to write. Each week the agent reads everything those companies published in the window via Synorb, and returns a short list of story ideas, each with the angle, why now and at least two citations to the companies' own posts. Use when a reporter, editor or newsletter writer on the AI beat wants pitches, leads or angles from what AI companies announced. Set it up once; the agent then runs it weekly and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.7.0"
  homepage: https://synorb.com/skills/story-ideas
---

# Story ideas

Give this journalist story ideas they can pitch or report this week, built from what AI companies published themselves. Synorb does the reading; the journalist does the reporting. An idea is a lead with its evidence, never a finished story or a verified fact. Use the journalist's beat, past work and stated interests when you have them; do not infer private facts about the journalist or their sources.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would explain a material comparison, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.

If a tool result truncates this Skill, a referenced procedure or featured source evidence, retrieve the omitted section separately before using it. Read the complete refinement procedure before drafting.

After gathering, return to the reader-payoff check in references/output-quality.md before drafting; assess that payoff before the source and delivery checks during refinement.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), including the citation, attribution and coverage checks below. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/story-ideas`.

## Step 2: Set up the beat

This Skill runs on the AI Companies Beacon, narrowed to the Segments the journalist picks. The Segments are the boxes of the public market map at https://synorb.com/market-map/ai-companies.

1. Always list all 14 Segments for the user, numbered, by name, with what each covers, before you ask. Do not show the ids. Do not ask the user to pick from memory or from a link. Copy this list as it is:

```text
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
```

   Then ask: "Pick 1 to 3 by number or name." The user can see the same Segments on the map at https://synorb.com/market-map/ai-companies. Map each pick to its id:

| # | Segment | id |
| --- | --- | --- |
| 1 | Compute & Hardware | `ai_companies:compute_hardware` |
| 2 | Foundation Models | `ai_companies:foundation_models` |
| 3 | Data & Training | `ai_companies:data_training` |
| 4 | Model Ops & LLMOps | `ai_companies:model_ops` |
| 5 | Agent Infrastructure | `ai_companies:agent_infrastructure` |
| 6 | Coding & Software Engineering | `ai_companies:coding` |
| 7 | AI Security & Governance | `ai_companies:security_governance` |
| 8 | Enterprise Apps | `ai_companies:enterprise_apps` |
| 9 | Industry Apps | `ai_companies:industry_apps` |
| 10 | Generative Media & Voice | `ai_companies:generative_media` |
| 11 | Consumer AI | `ai_companies:consumer_ai` |
| 12 | Physical AI & Robotics | `ai_companies:physical_ai` |
| 13 | AI for Science & Bio | `ai_companies:science_bio` |
| 14 | Big Tech Platforms | `ai_companies:big_tech` |

   If the user names a narrower area ("coding agents", "voice"), you may use a sub-segment id from the stream-search error list or the map, for example `ai_companies:coding_agents`. More than 3 Segments makes the weekly read too large; ask the user to choose.
2. Ask one question: "From the point of view of a story you would want to write, what interests you in these companies?" Offer examples only if the user hesitates: who is winning customers, pricing and business models, funding and consolidation, security and safety, the people and teams, open source against closed, what the hype hides.
3. Add other context you already have about the journalist, such as their beat, outlet, past stories or a writing sample, when the user has shared it with you. Keep a compact private brief: Segments, interests, story types they like and dislike, and stories they already wrote. Do not send the brief to Synorb.

## Step 3: Turn the Segments into a Beacon

1. For each Segment, list its Streams with `synorb-stream-search` (`segment="ai_companies:coding"`, `page_size=200`, no `query`) or `POST /streams/search` with `{"segment": "ai_companies:coding", "page_size": 200}`. Do not add a `query`: it keeps only Streams whose text has the words. Page with `page` until `pagination.has_more` is false. Collect each result's `id` as a string. The response can be large; if you have a file tool, save it and read only `results[].id`, `name` and `manifests_last7d`.
2. If the search says the segment filter is not enabled, read the Segment's company tiles on https://synorb.com/market-map/ai-companies instead: each Segment is a section with that id, and each tile carries `data-stream-id`. Say which method you used.
3. Tell the user how many companies the Segments hold and how many published in the last 7 days, for example "Coding & Software Engineering: 46 companies, 23 published this week."
4. Propose one Beacon named for the beat, for example "Story Ideas: Coding & AI Security", with the combined Stream ids. Save it with `synorb-save-beacon` or `POST /v3/beacons` (`name`, `stream_ids`, `"status": "active"`) only after the user says yes. Check the Beacon limit first (section 4 of the reference).
5. If there is no free Beacon slot, say so and ask whether to archive one. Until then, pull with the same `stream_ids` on `synorb-manifests` or `POST /manifests/query`, and tell the user the scope is not saved.
6. **Never send `beacon_id` of the AI Companies starter together with `stream_ids` to narrow it.** The saved Beacon scope wins and the result is the whole AI Companies Beacon, not the Segments. Use your own Segment Beacon or the `stream_ids` alone.

## Step 4: Gather the week

1. Count first (free): `mode="count"` with the Segment Beacon (or the `stream_ids`) and `lookback_hours=192`. Read `pagination.total_count` and `temporal.effective_from` / `effective_to`.
2. A busy Segment can publish 200 or more items a week. Check `quota` before you pull. On a small allowance, pull small pages spread across the window with `published_date_from` and `published_date_to` day slices, and say how many items you read of how many matched. Offer a narrower sub-segment when the allowance is too small for the beat.
3. Drop items already delivered for this job (by `manifest_id`, as a string).
4. Read the full Claims and quotes of every item you may use. A headline is not evidence.

## Step 5: Find the stories

A story idea is a pattern a reader would care about, not a single press release. Look for these, ranked by the journalist's stated interests:

| Pattern | What to look for in the Claims |
| --- | --- |
| A shared shift | Two or more companies describe the same problem, product move or number in the same window |
| A turning point | A launch, a shutdown or end of life, a price or license change, a funding round, an acquisition |
| A disagreement | Companies make claims that conflict, or one company argues against another's approach |
| A number to check | A measured figure (a benchmark, a survey, a usage count) that a story could test or explain |
| People | A named executive move or a named customer that says where the market is going |

Rules for each idea:

1. It must rest on at least 2 Manifests. Prefer posts from 2 or more different companies. If both citations come from one company, say "one company's own posts" in the idea.
2. Use only facts from Claims, quotes and source metadata. Copy figures, dates and names exactly. Never invent a number, a quote, a source or a link.
3. A company post about itself is the company's claim, not an independent finding. Write "Cognition says" or "Qodo reports". When a company cites someone else's figure (a survey, a report), attribute both: "Qodo cites GitHub Octoverse 2026". Suggest checking the original.
4. A company post about another company is still that company's claim. Do not present it as fact about the other company.
5. Keep hedges and confidence labels. Do not turn an `implied` or `inferred` Claim into a statement.
6. Drop Synorb's own posts, how-to guides with no news, event recaps and items whose own text shows an older date.
7. Do not repeat an idea you delivered before unless new evidence changes it. Then say what changed.

## Step 6: Write the ideas

Start with one line: the Segments, the effective dates, and how many items you read of how many matched. Then 3 to 5 ideas, fewer in a thin week. For each idea:

1. **A working headline.** Plain, specific, no hype. Use "published", "announced" or "says". Do not write that a company "shipped" something.
2. **The angle.** One or two sentences: the story the journalist could write, tied to their stated interest.
3. **Why now.** The dated events from this window that make it timely.
4. **Evidence.** 2 to 4 bullets. Each bullet: the fact, the company, the date and the link to the company's own post. Add the confidence label when it is not `stated`.
5. **What to report next.** Labelled as your suggestion: the questions to ask, the people or companies to call, and the documents to check. These are leads, not facts.
6. **What the posts do not show.** One line when it matters, for example "Both figures are the companies' own; no outside measure in this window."

Then **Also worth a look**: up to 3 one-line items with a link, for single posts that may grow into a story. End with a numbered source index (company, title, date, link).

Say once, not after each idea, that every item is a company's own publication found by Synorb, and that the journalist should verify before publishing.

## Step 7: Set the schedule

This first set of ideas is the setup run. Agree the day and where the ideas go; the default is every Monday at 8:00 in the user's time zone (`lookback_hours=192`). Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Keep the brief, the Segment ids, the `beacon_id` or `stream_ids`, the delivered `manifest_id` values and the delivered idea headlines in the job state.

After each delivery, ask at most one short question when it helps: which idea was useful, or what to drop. Update the brief from the answer. Once a month, search the Segments again and offer to add new companies to the Beacon (`synorb-update-beacon`, dry run first, then only after a yes).
If `quota.account_notice.user_message` is in a response, give that sentence once, after the ideas.
