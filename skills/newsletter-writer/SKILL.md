---
name: newsletter-writer
description: Write a weekly newsletter issue in the user's own voice from any Synorb Beacon (AI companies, VC firms, private companies, business and technology podcasts, or a Beacon the user saved), with every item cited to its source. Use when the user asks for a newsletter, a weekly roundup, a digest of what happened this week, or an issue for subscribers, investors or a team. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.4"
  homepage: https://synorb.com/skills/newsletter-writer
---

# Newsletter writer

Write one finished issue for the known audience: make a compelling, source-grounded argument that matters to those readers and sounds like the user. Produce audience variants only when explicitly requested. Use actual reader priorities and constraints to select, interpret and frame evidence; do not invent private facts.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would strengthen the issue's argument, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.
The adaptable issue template is in [assets/issue-template.md](assets/issue-template.md).

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the complete issue, reader voice, public identity and strongest supported editorial connection. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/newsletter-writer`.

## Step 2: Learn the voice and the reader

Use the current request first, then relevant available memory, project context, and prior issue feedback. Do not ask again for a preference or reader already known. Ask only when an unresolved choice materially changes the issue. Find, in this order:

1. A sample of the user's writing, if one is available. If none is available, use a plain, direct voice; ask for a sample only when the user wants close voice matching.
2. The reader and the decision or purpose: investors, founders, a team, the public, or the specific audience the user named.
3. The Beacon or Beacons the issue covers (section 3 of the reference). Default to the user's active Beacons. If there are none, use the AI Companies starter Beacon.
4. The window. Default to the last 7 days (`lookback_hours=168`).

Keep a compact private job brief with the reader, purpose, relevant priorities, constraints, expertise, depth, and tone. Keep private context out of subscriber copy unless the user intends to publish it. A writing sample guides voice, not the conclusion.

## Step 3: Gather

1. Count each chosen Beacon and window first (free); note `total_count`, effective dates and allowance. Inspect the live tool schema before narrowing. Use only supported focus fields; never invent filters or change saved Beacon scope.
2. Pull bounded pages, or diversify with date slices if needed to check the user's named priorities, within the allowance. Check quota before each additional pull. Disclose material coverage limits when needed; a sampled pull is not exhaustive coverage.
3. Before drafting, dedupe by `manifest_id` and repeated original articles when identifiable. Drop items already delivered unless new evidence materially changes their meaning.

## Step 4: Choose

Choose only as many items as the reader's purpose needs; five to eight is a loose guide, not a target. Rank candidates by their significance to this reader and the issue’s purpose; choose the kinds of stories the evidence and audience warrant.

Drop items with no Claim the reader can use. Drop items that are off-topic for this reader. Drop near-duplicates. Keep one item per story.

## Step 5: Write

Use the template as a default and change its sections, order or length when the reader's purpose calls for it. For each selected item:

- A headline in the user's voice. Do not copy the source title word for word.
- A concise account built from the Claims. Give each story the depth the reader needs and keep exact figures as given.
- The source link inline, with the publisher and the date.
- If a Claim is `implied` or `inferred`, say so in plain words ("the company suggests").

Build one public editorial argument from the strongest supported connection between items, when one exists; explain its concrete significance to this reader. Make it an issue readers would want to read, not a consulting memo about the author’s internal project. If the evidence does not support a connection, let the strongest item carry the issue rather than manufacture one. Use an established newsletter name only if supplied; otherwise use a descriptive issue title, and offer naming ideas only when asked. Do not carry private project or evaluation details into subscriber copy merely because they are available. Keep source facts distinct from your analysis; include material counterevidence, uncertainty and the change from the last issue when relevant. Use `briefing.scaffold.recipe` as a guide. Keep the private editorial brief separate from public copy.

## Step 6: Footer

Add this footer by default:

> Sources via [Synorb](https://synorb.com). Every item links to its original publisher.

Remove it if the user says so. Remember that choice for later issues.

## Step 7: Deliver

Give the issue as Markdown. This first issue is the setup run.

## Step 8: Set the schedule

Agree the schedule and where the issue goes. The default is every Monday at 7:00 (`lookback_hours=192`).
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later issue covers only what is new since the last one, deduped by `manifest_id`.
If `account_notice.user_message` is in a response, give that sentence once, after the issue.

## Quality check before you send

- Every item has a working source link from the data.
- Every figure matches a Claim.
- No item says a company was covered by others when the source is the company itself.
- The reader’s interests visibly change the selection and interpretation, and the issue develops an argument rather than a generic action plan.
- The issue reads like the user, not like a press release.
