---
name: thesis-tracker
description: Track what venture capital firms and their partners publish - investment theses, market maps, new funds, portfolio news and podcast arguments - from the firms' own essays, blogs and podcasts via Synorb Streams, and map it to the user's own thesis with citations. Use when the user asks what VCs are saying, what a16z, Sequoia or another firm published, where investors are leaning, or how VC views match their own thesis or pitch.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/thesis-tracker
---

# Thesis tracker

You read what VC firms publish and show the user where the firms agree, disagree, and point.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/thesis-tracker`.

## Step 2: Set the scope

1. **Named firms or partners.** Search each name (`synorb-stream-search` or `POST /streams/search`). Firm Streams carry the firm's essays, announcements and podcasts. Some partners have their own Stream (for example an author page or a personal blog).
2. **All VC firms.** Use the Venture Capital recipe:
   - MCP: `synorb-configure-beacon` with the intent "venture capital firms", then save it only after the user says yes.
   - REST: `POST /v3/beacons/fork` with `{"pack_id": "venture-capital", "dry_run": true}` to preview, then the same call with `"status": "active"` and without `dry_run` after a yes.
   Check the Beacon limit first (see the reference).
3. **The user's thesis.** Ask for it in one or two sentences, or read it from a deck, a memo or past conversations. Skip this if the user only wants a summary.
4. Window: 30 days (`lookback_hours=720`). Firms post less often than companies.

## Step 3: Gather

Count first (free). If the count is more than 20, split the window into three date slices (`published_date_from`, `published_date_to`) and pull 7 from each, or 5 from each on a demo key. Otherwise pull up to two pages of 10.
The Venture Capital recipe is broad. Expect off-topic items (climate funds, accelerator portfolio news) and skip them for a focused question.

## Step 4: Extract positions

For each item, note:

- **Who:** the firm, and the partner or guest if a Claim, a quote or the title names them.
- **Position:** the claim the firm makes about a market, a technology or a company. Keep the confidence label.
- **Action:** a new fund, an investment, a program, an application deadline.

A podcast Claim often does not name the speaker. Say "on the firm's podcast" when no one is named.

## Step 5: Write the tracker

1. **Headline moves.** New funds, renamed funds, programs and deadlines. Exact figures, dates and links.
2. **Themes.** Two to four themes several firms touch. For each, list who said what, with links. Show disagreement when sources differ.
3. **Your thesis vs the firms** (only if the user gave one). Where the firms support it, where they push against it, and what is missing. Label this part as your analysis.
4. **Sources.** A numbered list.

Say plainly that these are the firms' own publications, not outside reporting.

## Step 6: Offer the next step

Offer a monthly tracker, or a Beacon for the firms the user cares about most. Save or schedule only on a yes.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the tracker.
