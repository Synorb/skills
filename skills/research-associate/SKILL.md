---
name: research-associate
description: Write a cited research memo from a Synorb Beacon - for example what VC firms, AI companies, private companies or business podcasts published this week - with a bottom line, a dated timeline, Claims carrying their confidence labels (stated, measured, implied, inferred) and a source index. Use when the user asks to be briefed on a sector or a set of organizations, wants a memo before a meeting or an investment decision, or asks what a group of companies or investors has been saying. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.0"
  homepage: https://synorb.com/skills/research-associate
---

# Research associate

You write a memo the user can trust and check. Cite facts and use natural attribution in prose; preserve exact confidence labels in an evidence table or ledger when used.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would clarify a material comparison or sequence, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.
The adaptable memo template is in [assets/memo-template.md](assets/memo-template.md).

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the research question, decision implications, counterevidence and source distinctions. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/research-associate`.

## Step 2: Pick the Beacon and the question

1. Start with the user's decision, question or purpose and relevant available memory, files and prior feedback. Reuse known context without asking again; ask only when an unresolved choice materially changes the memo. Pick the Beacon with section 3 of the reference. Match it to the request:

   | The user asks about | Beacon |
   | --- | --- |
   | AI labs, AI tools, AI infrastructure | AI Companies (starter) |
   | VC firms, investors, funds | Venture Capital (starter; catalog on older accounts) |
   | Startups and other private companies | Private Companies (starter; catalog on older accounts) |
   | Public-company filings, earnings, executive changes | Public Company Filings & Executive Transitions (starter) |
   | What the big shows and hosts said | Business & Technology Podcasts (starter) |
   | Central bank policy and speeches | Central Banks (starter on older accounts; catalog) |
   | Anything the user already saved | That Beacon |

2. State the user's question and purpose from the request or available context. If no narrower question was given, make a useful Beacon-level brief without implying complete coverage.
3. Note material audience, constraints, expertise, depth and preferred format in the job brief. Separate explicit facts from tentative inferences.
4. Window: 7 days by default (`lookback_hours=168`). Use 30 days (`720`) when the user asks for "this month".

If the user names one company or one person, use the Beacon that holds it, and keep that name as the question. Say that the memo covers the Beacon, not every source about that name.

## Step 3: Gather

1. Count the chosen Beacon and window first (free). Note `total_count`, effective dates and allowance.
2. Inspect the live tool schema and use only supported focus fields for the user's question. Never invent filters or alter the saved Beacon scope. If no supported focus field applies, inspect bounded pages or diversified date slices within the allowance; say how much you inspected and do not call a sample exhaustive.
3. Read `signal.body.claims[]` and the Brief for each item you may use. Titles can help screen, but they do not establish the finding. Read every Claim of featured items and track matched, screened and retained counts.
4. Dedupe repeated original items before drafting; revisit prior items when new evidence changes their meaning.

## Step 4: Write the memo

Use the template as a starting point. Choose the clearest form for the decision; prose may replace a table or timeline when that serves the reader better. Do not include every section by default. The parts may include:

1. **Bottom line.** A concise explanation of what changed and why it matters for the purpose.
2. **Timeline.** One line per dated event, oldest first. Each line has the date, the organization and a source link.
3. **Evidence.** Use a Claims table when comparison or auditability benefits from it; otherwise integrate cited Claims into prose. Preserve each `confidence` label exactly when shown.
4. **Open questions and counterevidence.** What the sources leave unresolved, disagree on, or would change the assessment. Mark your own analysis as yours.
5. **Coverage note.** The Beacon, the window, how many items matched, how many you read and how many you kept. Say what kind of source they are. Example: "All items are the firms' own essays, blogs and podcasts. This memo has no outside reporting."
6. **Source index.** Use when it helps the reader navigate multiple sources.

Answer the actual research question, compare plausible alternatives where the evidence permits, and explain the decision implications. Do not assume a company, stack, budget, fundraising status or prior assessment. Lead with the finding most useful to this decision. Separate source facts from your interpretation, name material uncertainty, and compare with the prior assessment when available. Never turn an organization's forecast or claim into an independently verified fact.

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
