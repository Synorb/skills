---
name: research-associate
description: Write a cited research memo on one organization, person or topic from Synorb Streams, with a dated timeline, Claims carrying their confidence labels (stated, measured, implied, inferred) and a source index. Use when the user asks to research a company, a VC firm, a founder, an investor or a theme, prepare for a meeting, build a company profile, or check what an organization has said recently.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/research-associate
---

# Research associate

You write a memo the user can trust and check. Every fact has a source and a confidence label.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.
The memo shape is in [assets/memo-template.md](assets/memo-template.md).

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/research-associate`.

## Step 2: Pin the subject

Get three things. Ask only for what you cannot infer.

1. The subject: an organization, a person or a topic.
2. The purpose: a meeting, an investment screen, an article, a competitive check.
3. The window. Default to the last 30 days (`lookback_hours=720`).

## Step 3: Find the right Streams

1. Search with the subject name (`synorb-stream-search` or `POST /streams/search`).
2. Read each candidate's `name` and `description`. Keep only Streams about this subject.
3. Know what a Stream holds:
   - An organization Stream carries that organization's own publications: its blog, press releases, filings, research.
   - A person Stream carries what that person publishes or says: essays, a podcast, posts.
   - A podcast Stream carries episodes of that show.
4. If the subject has no Stream, say so. Then search content that names the subject across Streams: `home_domains=["all"]` with `tag_names=["<subject>"]`. Count it first.
5. For a topic, use `synorb-configure-beacon` with the topic as the intent, or search with the topic words.

## Step 4: Gather

1. Count each scope first (free). Note `total_count` and the effective dates.
2. If `total_count` is 20 or less, pull up to two pages (`page_size` 10).
3. If `total_count` is more than 20, cover the whole window. Split it into three date slices (`published_date_from`, `published_date_to`). Pull one page of 7 from each slice. Newest-first pages alone cover only the last few days.
4. Check the allowance in `quota` between pulls. On a small allowance, pull fewer items and say so.
5. For each Manifest, read `signal.body.claims[]` and the Brief (`brief.body_markdown`). Titles alone are not enough. Read every Claim of the items you feature, not only the first few.
6. In the coverage note, say how many items matched and how many you read. Example: "54 items matched; this memo reads 21, spread across the 30 days."

## Step 5: Write the memo

Follow the template. The parts:

1. **Bottom line.** Three to five sentences. What changed, and why it matters for the purpose.
2. **Timeline.** One line per dated event, oldest first. Each line has the date and a source link.
3. **Key Claims.** A table: Claim, type, confidence, source. Copy `confidence` exactly as given.
4. **Open questions.** What the sources leave unresolved. Use the Brief and your own reading. Mark your own items as yours.
5. **Coverage note.** One or two lines: which Streams you used, the window, and what kind of source they are. Example: "All items are Anthropic's own publications. This memo has no outside reporting."
6. **Source index.** Numbered list: title, publisher, date, URL.

## Rules for this skill

- Keep the subject's own words separate from your analysis. Quote only text that is in a Claim `quote` or a supporting quote.
- Do not merge two Claims into one stronger Claim.
- If two sources disagree, show both and say they disagree.
- If you found little, write a short memo and say how much you found. Do not pad it.

## Step 6: Offer the next step

Offer to save a Beacon for the subject, so the next memo is one call away. Save it only on a yes.
If `account_notice.user_message` is in a response, give that sentence once, after the memo.
