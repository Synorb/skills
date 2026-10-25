---
name: research-associate
description: Write a cited research memo from a Synorb Beacon - for example what VC firms, AI companies, private companies or business podcasts published this week - with a bottom line, a dated timeline, Claims carrying their confidence labels (stated, measured, implied, inferred) and a source index. Use when the user asks to be briefed on a sector or a set of organizations, wants a memo before a meeting or an investment decision, or asks what a group of companies or investors has been saying. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.2.0"
  homepage: https://synorb.com/skills/research-associate
---

# Research associate

You write a memo the user can trust and check. Every fact has a source and a confidence label.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.
The memo shape is in [assets/memo-template.md](assets/memo-template.md).

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/research-associate`.

## Step 2: Pick the Beacon and the question

1. Pick the Beacon with section 3 of the reference. Match it to the request:

   | The user asks about | Beacon |
   | --- | --- |
   | AI labs, AI tools, AI infrastructure | AI Companies (starter) |
   | VC firms, investors, funds | Venture Capital (catalog) |
   | Startups and other private companies | Private Companies (catalog) |
   | What the big shows and hosts said | Business & Technology Podcasts (starter) |
   | Central bank policy and speeches | Central Banks (starter) |
   | Anything the user already saved | That Beacon |

2. Get the question in one line, if there is one. Example: "What did VC firms say about AI agents?" A memo with no question covers the whole Beacon.
3. Get the purpose: a meeting, an investment screen, an article, a competitive check.
4. Window: 7 days by default (`lookback_hours=168`). Use 30 days (`720`) when the user asks for "this month".

If the user names one company or one person, use the Beacon that holds it, and keep that name as the question. Say that the memo covers the Beacon, not every source about that name.

## Step 3: Gather

1. Count the Beacon first (free). Note `total_count` and the effective dates.
2. If `total_count` is 20 or less, pull up to two pages (`page_size` 10).
3. If `total_count` is more than 20, cover the whole window. Split it into three date slices (`published_date_from`, `published_date_to`). Pull one page of 7 from each slice, or 5 on a demo key.
If a slice holds fewer items than its share, pull what it has.
4. Check the allowance in `quota` between pulls. On a small allowance, pull fewer items and say so.
5. For each Manifest, read `signal.body.claims[]` and the Brief. Titles alone are not enough. Read every Claim of the items you feature.
6. With a question, keep the items that bear on it. Count how many you read and how many you kept.

## Step 4: Write the memo

Follow the template. The parts:

1. **Bottom line.** Three to five sentences: what changed, and why it matters for the purpose.
2. **Timeline.** One line per dated event, oldest first. Each line has the date, the organization and a source link.
3. **Key Claims.** A table: Claim, organization, type, confidence, source. Copy `confidence` exactly as given.
4. **Open questions.** What the sources leave unresolved. Mark your own items as yours.
5. **Coverage note.** The Beacon, the window, how many items matched, how many you read and how many you kept. Say what kind of source they are. Example: "All items are the firms' own essays, blogs and podcasts. This memo has no outside reporting."
6. **Source index.** A numbered list: title, publisher, date, URL.

## Rules for this skill

- Keep each organization's own words apart from your analysis. Quote only text that is in a Claim `quote` or a supporting quote.
- Do not merge two Claims into one stronger Claim.
- If two sources disagree, show both and say they disagree.
- If you found little, write a short memo and say how much you found. Do not pad it.

## Step 5: Set the schedule

This first memo is the setup run. Agree the schedule and where the memo goes. The default is weekly (`lookback_hours=192`); use monthly (`768`) for a "this month" memo.
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later memo covers only what is new since the last one.
If the memo used a catalog Beacon the account does not have, offer to copy it, so the scheduled runs can use it. Copy it only on a yes.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the memo.
