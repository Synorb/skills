---
name: thesis-tracker
description: Track what venture capital firms and their partners publish - investment theses, market maps, new funds, portfolio news and podcast arguments - from the firms' own essays, blogs and podcasts via Synorb's Venture Capital Beacon, and map it to the user's own thesis with citations. Use when the user asks what VCs are saying, what a16z, Sequoia or another firm published, where investors are leaning, or how VC views match their own thesis or pitch. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.8"
  homepage: https://synorb.com/skills/thesis-tracker
---

# Thesis tracker

Update the user’s actual business or investment thesis against a prior assessment of that same thesis when available: say what changed, what did not, and a specific observable condition that would move the assessment. Select and interpret evidence for the user’s decision and priorities, without inventing a thesis, prior assessment or private facts. Explain competing positions and their implications for the user’s decision. When no thesis is requested, summarize the firms’ positions instead.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would clarify positions or changes over time, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.

If a tool result truncates this Skill, a referenced procedure or featured source evidence, retrieve the omitted section separately before using it. Read the complete refinement procedure before drafting.

After gathering, return to the reader-payoff check in references/output-quality.md before drafting; assess that payoff before the source and delivery checks during refinement.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the supplied thesis, attributed positions, counterevidence and any supported change in assessment. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/thesis-tracker`.

## Step 2: Set the scope

1. **The Venture Capital Beacon.** It covers VC firms' own essays, announcements and podcasts. New accounts have it as a starter (`tag="starter"`): use it. An account made before 2026-10-25 may not have it. Then copy the catalog Beacon (section 3 of the reference):
   - With HTTP access: `POST /v3/beacons/fork` with `{"pack_id": "venture-capital", "dry_run": true}` to preview, then the same call with `"status": "active"` and without `dry_run` after a yes.
   - With MCP tools only: ask the user to copy "Venture Capital" at https://synorb.com/beacons, then list Beacons again.
   Check the Beacon limit first (see the reference).
2. **Named firms.** If the user names firms, keep the Venture Capital Beacon and rank those firms first. If a named firm is not in the Beacon, say so.
3. **The user's thesis and decision.** Use the request and relevant available memory, deck, memo or prior assessment of the same thesis. Do not ask again for an available thesis. Ask only when the user wants a comparison and the missing thesis materially changes it. Skip this if the user only wants a summary.
4. Window: 30 days (`lookback_hours=720`). Firms post less often than companies.

## Step 3: Gather

Count the chosen Beacon and window first (free); note effective dates and allowance. Inspect the live schema before narrowing. Use only supported focus fields; never invent filters or alter saved Beacon scope. Pull bounded pages, or diversify date slices if needed to cover named firms or priorities, within allowance. Disclose material coverage limits when needed; do not describe a sample as complete coverage.
The Venture Capital recipe is broad. Expect off-topic items (climate funds, accelerator portfolio news) and skip them for a focused question.

## Step 4: Extract positions

For each item, note:

- **Who:** the firm, and the partner or guest if a Claim, a quote or the title names them.
- **Position:** the claim the firm makes about a market, a technology or a company. Keep the confidence label.
- **Action:** a new fund, an investment, a program, an application deadline.

A podcast Claim often does not name the speaker. Say "on the firm's podcast" when no one is named.

## Step 5: Write the tracker

Lead with what matters to the user's decision. For a supplied thesis, distinguish evidence that supports it from counterevidence and explain any warranted update; do not invent the thesis or a prior assessment. Use sections that fit the evidence; theme groups or tables are optional when prose is clearer. Do not force a fixed number of themes.

1. **Position changes.** New funds, programs, deadlines, or meaningful changes in a firm's stated position, with dates and links.
2. **Agreement and disagreement.** Show which firms said what and where evidence conflicts. Treat repeated reporting of one original publication as one source.
3. **Thesis comparison** (only when the user wants it and the thesis is available). Identify supporting evidence, counterevidence, missing evidence, and what would change the assessment. Label your interpretation.
4. **Sources.** Include a source index when useful to navigate the evidence.

Say plainly that these are the firms' own publications, not outside reporting.
Compare the current picture with an actual prior assessment of the same thesis when available; identify the specific new evidence and how far it moves the assessment, or explain why it does not. Give a meaningful observable condition that would strengthen or weaken the belief. A proposed study may be relevant, but must not replace the update or become a generic testing plan. Do not invent a thesis score or claim that source silence disproves it.
If effective query dates are unavailable, show the observed item dates and say query coverage is unknown.
Dates on individual publications do not establish complete coverage of the month. When tracking a thesis, check before delivery that the update and belief-changing condition are specific to this thesis and decision, not interchangeable with an unrelated one.

## Step 6: Set the schedule

This first tracker is the setup run. Agree the schedule and where the tracker goes. The default is the first day of each month (`lookback_hours=768`).
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later tracker covers only what the firms published since the last one, and says how the picture moved.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the tracker.
