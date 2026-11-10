---
name: portfolio-watch
description: Watch a VC firm's AI portfolio companies and their competitors through Synorb - what each company and each rival announced this week (launches, pricing, hires, funding, partnerships), mapped to the portfolio company it affects, with every item cited, plus a one-page brief before a board meeting or founder call. Use when an investor, platform lead or VC firm staff member wants to track their portfolio, their portfolio's competitors, or prepare for a portfolio company meeting. Set it up once; the agent then runs it weekly and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.7.0"
  homepage: https://synorb.com/skills/portfolio-watch
---

# Portfolio watch

Give this investor what changed for the companies they own: what each portfolio company announced, what its competitors did, and which moves deserve a conversation with the founder. It runs on two Beacons the user saves: Portfolio and Competitors. Rank by consequence for each portfolio company, not by volume. Do not infer private facts about the firm, its holdings or its founders.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would explain a material comparison, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.

If a tool result truncates this Skill, a referenced procedure or featured source evidence, retrieve the omitted section separately before using it. Read the complete refinement procedure before drafting.

After gathering, return to the reader-payoff check in references/output-quality.md before drafting; assess that payoff before the source and delivery checks during refinement.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), including the competitor mapping, attribution and coverage checks below. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/portfolio-watch`.

## Step 2: Get the portfolio

1. Ask for the companies to watch, or use a list the user already gave you (a file, a message, the firm's public portfolio page if the user points you to it). Do not guess holdings.
2. **Confidential holdings.** A stream search sends each company name to Synorb. If the list includes undisclosed investments, ask before you search, and search only the names the user clears.
3. **Competitors.** For each portfolio company, ask for its main competitors. If the user prefers, propose two or three from what you know and from Synorb stream search, labelled as your proposal, and keep only the ones the user confirms.
4. Keep the map of competitor to portfolio company in the job state. One competitor can map to several portfolio companies.

## Step 3: Check coverage and save the Beacons

1. Search each name with `synorb-stream-search` (`POST /streams/search`). Accept a Stream only when all three hold: `match_strength` is `strong`, the Stream's name is this company (not another company with the same word, for example a bank or a filing stream for "Sierra"), and its description says it is the company's own blog, newsroom, release notes or podcast. Read the description; do not take the first result. A `weak` or `none` match is not coverage.
2. Report coverage in one line, for example "11 of 14 portfolio companies and 19 of 25 competitors have a Synorb Stream." List the companies without one by name. Do not fill their gap from other companies' posts. The user can ask Synorb to add them.
3. Propose two Beacons and ask once: **Portfolio** (the portfolio companies' Streams) and **Competitors** (the competitors' Streams). Save each with `synorb-save-beacon` or `POST /v3/beacons` (`stream_ids`, `name`) only after the user says yes. Check the Beacon limit first (section 4 of the reference).
4. If the plan has no free Beacon slot, say so and ask whether to archive one. Until then, run each pull on the same Stream ids with `stream_ids` in `POST /manifests/query`, and tell the user the scope is not saved.

## Step 4: Gather

1. Count both Beacons for the window first (free); note the effective dates and the allowance. The default window is 7 days (`lookback_hours=192` for a weekly run).
2. Also count each Stream on its own (`stream_ids` with one id, `mode="count"`, free). A company with 0 items is quiet; a company with items you did not pull is unread. Report the two differently.
3. Pull bounded pages within the allowance. Portfolio items come first: if the allowance is short, read every portfolio item before competitor items, and say what you left unread.
4. If the allowance cannot cover every portfolio item, spread it: pull a small page (`page_size` 1 or 2) from each portfolio Stream that has items, instead of one large page that a busy Stream fills. A page is not ordered by importance or by date; do not call it the newest.

## Step 5: Sort the moves

Keep items where a company announces something about itself:

| Move | Signs in the Claims |
| --- | --- |
| Launch | A new product, model, feature or general availability |
| Pricing | A price, a plan, a limit, a free tier change |
| People | A named executive hire or departure |
| Funding | A round, an amount, a valuation, named investors |
| Partnership or customer | Two named organizations and a deal, or a named customer |
| Expansion | A new region, office or market |

Drop how-to guides, event recaps, hiring ads and general essays. For a release-notes page with many entries, use only the entries dated inside the window.

For each competitor move, decide which portfolio company it affects and how: the same buyer, the same product category, a price below theirs, a feature they sell, a partner they need. Say "overlaps" only when the Claims support the overlap. If the effect is unclear, list the move without a claimed threat.

## Step 6: Write the watch

1. **What needs attention.** At most three items, across portfolio and competitors, ranked by consequence for a portfolio company. One or two sentences each: what happened, the date, the source link, and why it matters to that company.
2. **Portfolio companies.** One short block per company with moves this week, grouped by company. Each fact is cited.
3. **Competitor moves.** Each move under the portfolio company it affects: "Competitor X launched Y on Oct 30 (source). This overlaps Portfolio Co Z's main product."
4. **Quiet this week.** One line naming the covered companies with no new announcements.
5. **Worth raising with the founder.** Optional, labelled as your view: a question for a founder whose company or competitors moved, only when the evidence supports it.

Say "the company says" for claims about the company's own product or results. A company Stream carries the company's own posts, not independent reporting; state that once, not after every item. Preserve exact figures, dates and Claim confidence. Never present a competitor's own claim about itself as a fact about the market.

## Step 7: Board and founder brief (on request)

When the user asks to prepare for a board meeting or call with one portfolio company, write a one-page brief for that company:

1. Count and pull that company's Stream and its mapped competitors' Streams for the last 90 days (`lookback_hours=2160`), within the allowance.
2. Sections: what the company announced (dated, cited), what its competitors announced, open questions to ask, each question tied to a cited item.
3. Say plainly that this covers public announcements only, not the company's private metrics.

## Step 8: Set the schedule

This first watch is the setup run. Agree the schedule and where the watch goes. The default is every Monday morning (`lookback_hours=192`). Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later watch lists only moves you have not reported. Keep the portfolio list, the competitor map and the uncovered names in the job state, and re-check uncovered names once a month in case Synorb added a Stream.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the watch.
