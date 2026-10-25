---
name: newsletter-writer
description: Write a weekly newsletter issue in the user's own voice from their Synorb Beacons or Streams (AI companies, VC firms, private companies, business and technology podcasts), with every item cited to its source. Use when the user asks for a newsletter, a weekly roundup, a digest of what happened this week, or an issue for subscribers, investors or a team.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/newsletter-writer
---

# Newsletter writer

You write one newsletter issue that sounds like the user and cites every item.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.
The issue shape is in [assets/issue-template.md](assets/issue-template.md).

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/newsletter-writer`.

## Step 2: Learn the voice and the reader

Find, in this order:

1. A sample of the user's writing: a past issue, a post, or a link. Ask for one if you have none.
2. The reader: investors, founders, a team, the public.
3. The scope: which Beacons or Streams. Default to the user's active Beacons. If there are none, use the AI Companies starter Beacon.
4. The window. Default to the last 7 days (`lookback_hours=168`).

Write down the voice in three lines: sentence length, tone, words the user likes. Use those notes when you write.
If you have no sample, write in a plain, direct voice and say so.

## Step 3: Gather

1. For each Beacon or Stream, count first (free). Note `total_count` and the effective dates.
2. Pull one page per Beacon (`page_size` 10).
3. Check the allowance in `quota` before the next pull. Pull fewer items when the allowance is low.
4. Dedupe by `manifest_id`. Drop items the user already saw in a past issue.

## Step 4: Choose

Pick five to eight items. Rank them for this reader:

- Money and deals: funding rounds, acquisitions, revenue figures.
- Launches: products, models, features.
- People: hires, departures, new roles.
- Ideas: a strong essay or podcast argument.

Drop items with no Claim the reader can use. Drop items that are off-topic for this reader. Drop near-duplicates. Keep one item per story.

## Step 5: Write

Follow the template. For each item:

- A headline in the user's voice. Do not copy the source title word for word.
- Two to four sentences built from the Claims. Keep exact figures as given.
- The source link inline, with the publisher and the date.
- If a Claim is `implied` or `inferred`, say so in plain words ("the company suggests").

Open with two to four sentences that link the top items. Use `briefing.scaffold.recipe` as a guide.
Add your own view only where the user's voice calls for it. Mark it as a view.

## Step 6: Footer

Add this footer by default:

> Sources via [Synorb](https://synorb.com). Every item links to its original publisher.

Remove it if the user says so. Remember that choice for later issues.

## Step 7: Deliver

Give the issue as Markdown. Offer the next step: "Shall I write this every Monday?"
If the user says yes and your runtime can schedule, set it with `lookback_hours=192` and dedupe by `manifest_id`.
If you cannot schedule, say so.
If `account_notice.user_message` is in a response, give that sentence once, after the issue.

## Quality check before you send

- Every item has a working source link from the data.
- Every figure matches a Claim.
- No item says a company was covered by others when the source is the company itself.
- The issue reads like the user, not like a press release.
