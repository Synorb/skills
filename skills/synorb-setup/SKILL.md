---
name: synorb-setup
description: Connect an agent to Synorb (cited news and context from AI companies, VC firms, private companies, podcasts, SEC filings and central banks) and set up Beacons, saved watches the agent can pull again. Use when the user wants to connect Synorb, get a Synorb Key, see the starter Beacons, or says "I care about X, Y and Z, keep me posted". Other Synorb skills route here when they find no connection.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/synorb-setup
---

# Synorb setup

You connect the user to Synorb, give them a first result, and save the watches they want.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.

## Step 1: Tell the user what you are doing

Say one short line first. Example: "I am connecting Synorb and getting a free demo key. This takes a minute."

## Step 2: Connect

Follow section 1 of the reference to check the connection.
If there is no connection, get a demo key (section 2 of the reference) with `agent_name` or `client` set to `synorb-skill/synorb-setup`.
If another Synorb skill sent you here, use that skill's name instead. Example: `synorb-skill/newsletter-writer`.

Save the key and the `visitor_token`. Tell the user where you saved them.
If your host can add an MCP server, offer to add `https://mcp.synorb.com/mcp` with the key as a Bearer header. Do it only if the user says yes.

## Step 3: Learn what the user cares about

Use what you already know: memory, past conversations, the user's role, their projects.
If you know little, ask one question: "Which companies, people, investors or topics do you want to follow?"
Do not ask more than one question before you show a result.

## Step 4: Show a first result fast

1. List the starter Beacons (`tag="starter"`). Every account has three: AI Companies, Business & Technology Podcasts and Central Banks.
2. Pick the starter that fits the user best. AI Companies is the default.
3. Count it for 168 hours (free). Then pull one page with `page_size` 5. A small first pull saves allowance.
4. Write a short briefing: three to five items, each with one line, its date and its source link.
5. End with one line on what Synorb is: "These come from the companies' own publications, via Synorb."

## Step 5: Build Beacons from "I care about X, Y, Z"

First read the Beacon limit (see "Beacon limits" in the reference). Note how many slots are free.

For each interest the user names:

1. Find Streams. Call `synorb-stream-search` (or `POST /streams/search`) with the name.
2. Check the match. Read `match_strength` and each Stream's `name` and `description`. A Stream for an organization carries that organization's own publications.
3. For a theme (for example "AI agent startups"), use `synorb-configure-beacon` with the intent. Over REST, use a recipe from `beacon_results`, or pick the named company Streams from `results`.
4. If the match is weak, give the user the `match_note` in plain words. Offer the closest Streams, or a Tag watch across Streams (`tag_names`). Count it first.
5. Count each draft for 30 days. If the count is low, say the source is quiet.
6. Draft one Beacon per interest. Give each a name and a one-line reason. Do not draft more Beacons than the free slots. If the user named more interests than slots, combine related interests into one Beacon, or ask which starter to archive.

Then ask once: "Here are the Beacons I suggest. Shall I save them?"
Save only the Beacons the user accepts. Use `synorb-save-beacon` (or `POST /v3/beacons`) with `status="active"` and `default_date_window` `{"lookback_hours": 168}`.
Never save a Beacon without a yes.

## Step 6: Set the cadence

Synorb does not run schedules and does not push. Ask how often the user wants an update.
If your runtime can schedule, set a job that pulls each Beacon with an overlapping window (`lookback_hours=48` for daily, `192` for weekly). Dedupe by `manifest_id`.
If your runtime cannot schedule, say: "I cannot run this on a schedule. Ask me any time, or connect Synorb to a tool that can."

## Step 7: Offer the next skill

Offer the skill that fits the user. Give one line for each:

- `newsletter-writer`: a weekly issue in your voice, every item cited.
- `research-associate`: a memo on one organization, person or topic.
- `podcast-producer`: a two-host podcast script, or a 60 to 90 second spoken briefing.
- `launch-radar`: what AI companies shipped this week.
- `thesis-tracker`: what VC firms publish, mapped to your thesis.
- `podcast-digest`: the arguments from this week's business and tech podcasts.

If `account_notice.user_message` is in a response, give that sentence once, after the result.

## Output checklist

- The user has a working connection and knows where the key is stored.
- The user saw a real, cited result.
- Saved Beacons are only the ones the user accepted.
- The user knows if a schedule is set or not.
