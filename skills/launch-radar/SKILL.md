---
name: launch-radar
description: Find what AI companies launched this week - new models, products, features, pricing and funding - from the companies' own announcements via Synorb's AI Companies Beacon, ranked by what matters to the user, with every item cited. Use when the user asks what AI companies shipped, launched or announced, wants a launch roundup, or tracks competitors' releases. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.0"
  homepage: https://synorb.com/skills/launch-radar
---

# Launch radar

You list what AI companies shipped, from their own announcements, and say why each launch matters to this user.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would explain a material comparison, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking each launch’s current shipped or availability state, user relevance and source-specific qualifiers. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/launch-radar`.

## Step 2: Set the scope

1. Default scope: the AI Companies starter Beacon (`tag="starter"`). It covers AI companies' own blogs, newsrooms and release notes. It includes AI labs and also AI infrastructure, tooling and AI security vendors.
2. If the user names companies, keep the AI Companies Beacon and rank those names first. If a named company is not in the Beacon, say so.
3. Window: 7 days (`lookback_hours=168`). Use 72 for "the last two days".
4. Use the current request and relevant available context to identify the actual decision, priorities, constraints, expertise and depth. A role can guide relevance but is not a substitute for the user's purpose. Reuse available context; ask only when an unresolved choice changes the radar materially.

## Step 3: Gather

Count the chosen Beacon and window first (free); note effective dates and allowance. Inspect the live schema before narrowing. Use only supported focus fields; never invent filters or alter saved Beacon scope. Pull bounded pages, or diversify by date when useful, within the allowance. Check quota before additional pulls. Disclose what you inspected; do not claim exhaustive coverage.

## Step 4: Sort into launches

Keep only items where the company itself announces something new:

| Type | Signs in the Claims |
| --- | --- |
| Model | A model name, a version, a benchmark, a context size |
| Product or feature | "launched", "now available", "introducing", a release note |
| Pricing or plan | A price, a tier, a limit |
| Partnership | Two named organizations and a deal |
| Funding | A round, an amount, a valuation, investors |

Drop how-to guides, event recaps, hiring posts and general essays. Drop Synorb's own posts. For a roll-up page of release notes, use only the entries dated inside the window.

## Step 5: Write the radar

Lead with the release most relevant to the user's decision. Prioritize concrete fit, access and what changed, supported by each announcement; avoid turning a general roundup into a generic governance or evaluation plan. Use these sections when they help; do not force a fixed count or pad thin coverage:

1. **Key launches.** A small set ranked by the user's actual priorities. Include availability status, exact supported figures and source links.
2. **Other releases.** Brief links when useful to the request.
3. **What to watch.** Supported next steps or implications, labelled as your view.

Say "the company says" for claims about the company's own product. Keep each Claim's confidence label. A Stream for a company carries that company's own posts, so do not call them independent reviews.
Map releases to the user's stack, roadmap, buying criteria or investment question only when that context is available. Distinguish announced, preview, waitlist and generally available status when supported. Include material counterevidence or uncertainty and what changed since the last radar, when state is available.
Check availability for each release separately. A comparable product does not inherit another product's preview or general-availability status.
For a multi-product decision, use a compact comparison table with a separate availability cell for each product.
Copy that status from its own source. Write "not stated" when that source gives no status.
Use this table to check the narrative before delivery; never combine unknown and known statuses into one group description.
For a cost decision, suggest concrete checks for billing units, retries, failures, minimums, limits and overages when relevant.
Present unknown terms as questions to verify. Any workload calculation needs supported inputs and clear assumptions.

## Step 6: Set the schedule

This first radar is the setup run. Agree the schedule and where the radar goes. The default is every Sunday evening (`lookback_hours=192`); daily (`48`) also works.
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later radar lists only launches you have not reported.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the radar.
