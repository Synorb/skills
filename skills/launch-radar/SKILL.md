---
name: launch-radar
description: Find what AI companies launched this week - new models, products, features, pricing and funding - from the companies' own announcements via Synorb's AI Companies Beacon, ranked by what matters to the user, with every item cited. Use when the user asks what AI companies shipped, launched or announced, wants a launch roundup, or tracks competitors' releases. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.3.0"
  homepage: https://synorb.com/skills/launch-radar
---

# Launch radar

You list what AI companies shipped, from their own announcements, and say why each launch matters to this user.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/launch-radar`.

## Step 2: Set the scope

1. Default scope: the AI Companies starter Beacon (`tag="starter"`). It covers AI companies' own blogs, newsrooms and release notes. It includes AI labs and also AI infrastructure, tooling and AI security vendors.
2. If the user names companies, keep the AI Companies Beacon and rank those names first. If a named company is not in the Beacon, say so.
3. Window: 7 days (`lookback_hours=168`). Use 72 for "the last two days".
4. Learn the user's angle in one line if you can: a builder, an investor, a competitor, a buyer.

## Step 3: Gather

Count first (free). Then pull one page of 10. Pages are not sorted by launch value, so if the count is above 100 and the allowance allows, also pull page 1 (`page=1`).

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

1. **Top three.** The launches that matter most for this user's angle. Two or three sentences each, with the exact figures from the Claims and the source link.
2. **Also shipped.** One line each: company, what, date, link.
3. **What to watch.** One or two lines of your own reading, labelled as your view.

Say "the company says" for claims about the company's own product. Keep each Claim's confidence label. A Stream for a company carries that company's own posts, so do not call them independent reviews.

## Step 6: Set the schedule

This first radar is the setup run. Agree the schedule and where the radar goes. The default is every Sunday evening (`lookback_hours=192`); daily (`48`) also works.
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later radar lists only launches you have not reported.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the radar.
