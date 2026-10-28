---
name: synorb-setup
description: Connect an agent to Synorb (cited news and context from AI companies, VC firms, private companies, business and technology podcasts, SEC filings and central banks) and pick or save the Beacons that every other Synorb skill runs on. Use when the user wants to connect Synorb, get a Synorb Key, see the starter Beacons, add a Beacon such as Venture Capital or Private Companies, or says "I care about X, Y and Z, keep me posted". Other Synorb skills route here when they find no connection or no Beacon.
license: MIT
metadata:
  author: synorb
  version: "1.5.4"
  homepage: https://synorb.com/skills/synorb-setup
---

# Synorb setup

The first result should answer a question or illuminate a decision the user actually cares about, with a relevant next action. Connect the user and set up the Beacons their skills will run on. Use the user’s stated priorities and constraints to choose and interpret evidence, not merely to label the audience; do not invent private facts.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or form, read [references/output-quality.md](references/output-quality.md). If a comparison or relationship would be clearer visually, read [references/visuals.md](references/visuals.md) and create a real visual only when supported.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the connection and first cited result, Beacon fit and actual setup state. Deliver only the final result.

## Step 1: Tell the user what you are doing

Say one short line first. Example: "I am connecting Synorb and getting a free demo key. This takes a minute."

## Step 2: Connect

Follow section 1 of the reference to check the connection.
If there is no connection, get a demo key (section 2 of the reference) with `agent_name` or `client` set to `synorb-skill/synorb-setup`.
If another Synorb skill sent you here, use that skill's name instead. Example: `synorb-skill/newsletter-writer`.

Save the key and the `visitor_token`. Tell the user where you saved them.
If your host can add an MCP server, offer to add `https://mcp.synorb.com/mcp` with the key as a Bearer header. Do it only if the user says yes.

A demo key is free and short-lived, with a small allowance. To keep it, the user binds an email and moves to the free plan. The response's `quota.account_notice` says how. Do not promise any volume beyond the allowance the response shows.

## Step 3: Show a first result fast

1. List the starter Beacons (`tag="starter"`). New accounts have five: AI Companies, Business & Technology Podcasts, Venture Capital, Private Companies, and Public Company Filings & Executive Transitions. Older accounts have AI Companies, Business & Technology Podcasts and Central Banks.
2. Start with the user's current purpose, relevant available context and prior feedback. Use them to choose the starter Beacon that best fits the user's actual decision or interest; AI Companies is the fallback when nothing else fits.
3. Count the chosen Beacon for 168 hours (free), note its effective dates and the allowance, then pull a bounded first page with `page_size` 5. Check the live tool schema before narrowing; use only supported focus fields and never alter saved Beacon scope. If relevant coverage needs more, use bounded pages or date slices within allowance. Disclose material coverage limits when needed; do not present the sample as exhaustive.
4. Write a short, useful first briefing of the items that best fit the user's interest or decision, with concrete takeaways from the sources. Do not make available internal evaluation context the subject unless the user asks. Keep it brief when coverage is thin; each item needs its date and source link. Lead with the result that makes the Beacon's relevance clear, and give a next action specific to the finding and user’s purpose when warranted. Do not substitute a generic demonstration or testing plan for the result.
5. End with one line accurately describing the sources in the selected Beacon, for example, that the items come from the firms' own publications, via Synorb.

## Step 4: Set up the Beacons the user needs

Every Synorb skill runs on a Beacon (section 3 of the reference). Use what you already know from the request, available memory, past conversations, and projects.

Map interests from the user's current request and relevant available memory or project context. Distinguish explicit interests from tentative inferences; do not ask again for context already available. If the user's interests are unknown and the choice changes setup materially, ask once what they follow. Map each interest in this order:

1. **A starter Beacon** that already covers it (see step 1 for the list on this account).
2. **A Synorb catalog Beacon** from `GET /v3/public/beacons`. Common ones: Public Markets, Research, Central Banks, and Venture Capital or Private Companies when the account has no starter for them. Read each one's `description` and `counts.streams`.
3. **A new Beacon the user saves**, only when no starter or catalog Beacon fits. Build it from many Streams on one theme (`synorb-configure-beacon` with the intent, or `POST /streams/search` and its `beacon_results`). Count it for 30 days first. If the count is low, say the Beacon would be thin and suggest a broader one.

Do not make a Beacon for one company or one person. One source publishes a few times a month, so the Beacon comes back thin. Put the name inside a broader Beacon instead, and say which Beacon holds it.

Read the Beacon limit before you propose anything ("Beacon limits" in section 4). Starters count toward it.
Draft one to three Beacons. Give each a name and a one-line reason. Then ask once: "Here are the Beacons I suggest. Shall I add them?"
Add only the ones the user accepts:

- Catalog Beacon: `POST /v3/beacons/fork` with `{"pack_id": "<slug>", "status": "active"}`. With MCP tools only, ask the user to copy it at https://synorb.com/beacons.
- New Beacon: `synorb-save-beacon` (or `POST /v3/beacons`) with `status="active"` and `default_date_window` `{"lookback_hours": 168}`.

Never add a Beacon without a yes. If the user wants a Beacon that Synorb does not have, say so plainly and name the closest one.

## Step 5: Set the cadence

Every skill is set up once and then runs on its own schedule. Ask how often the user wants each update.
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Pull each Beacon with an overlapping window (`lookback_hours=48` for daily, `192` for weekly). Dedupe by `manifest_id`, so each run reports only what is new.
If your runtime cannot schedule, say: "I cannot run this on a schedule. Connect Synorb to a tool that can, or use the workflow recipe."

## Step 6: Offer the next skill

Offer the skill that fits the user, with the Beacon it will use:

- `newsletter-writer`: a weekly issue in your voice, from any Beacon.
- `research-associate`: a cited memo from any Beacon.
- `podcast-producer`: a two-host podcast script, or a 60 to 90 second spoken briefing, from any Beacon.
- `launch-radar`: what AI companies shipped this week (AI Companies).
- `thesis-tracker`: what VC firms publish, mapped to your thesis (Venture Capital).
- `podcast-digest`: the arguments from this week's shows (Business & Technology Podcasts).

If `quota.account_notice.user_message` is in a response, give that sentence once, after the result.

## Output checklist

- State whether the connection works and where the key is stored; do not claim setup succeeded if it did not.
- The user saw a real, cited result.
- Every skill the user wants has a Beacon to run on, and the user accepted each one added.
- The user knows if a schedule is set or not.
- The first result is useful on its own for the user’s purpose; its next action follows from the finding, and its coverage limit is concise.
- On later setup-related runs, use relevant saved setup state to explain meaningful coverage changes.
