---
name: launch-radar
description: Find what AI companies launched this week - new models, products, features, pricing and funding - from the companies' own announcements via Synorb's AI Companies Beacon, ranked by what matters to the user, with every item cited. Use when the user asks what AI companies shipped, launched or announced, wants a launch roundup, or tracks competitors' releases. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.6"
  homepage: https://synorb.com/skills/launch-radar
---

# Launch radar

Give this user a clear fit judgment on relevant releases, as the request and evidence permit: adoption, a targeted test, deferral or another supported conclusion. Rank company announcements by actual fit, access and economics for the user’s stated decision and constraints; do not infer private facts or force a recommendation where evidence is insufficient.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual would explain a material comparison, read [references/visuals.md](references/visuals.md) and create and verify it when tools permit.

If a tool result truncates this Skill, a referenced procedure or featured source evidence, retrieve the omitted section separately before using it. Read the complete refinement procedure before drafting.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), including the decision-critical evidence checks below, current availability, user relevance and source-specific qualifiers. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/launch-radar`.

## Step 2: Set the scope

1. Default scope: the AI Companies starter Beacon (`tag="starter"`). It covers AI companies' own blogs, newsrooms and release notes. It includes AI labs and also AI infrastructure, tooling and AI security vendors.
2. If the user names companies, keep the AI Companies Beacon and rank those names first. If a named company is not in the Beacon, say so.
3. Window: 7 days (`lookback_hours=168`). Use 72 for "the last two days".
4. Use the current request and relevant available context to identify the actual decision, priorities, constraints, expertise and depth. A role can guide relevance but is not a substitute for the user's purpose. Reuse available context; ask only when an unresolved choice changes the radar materially.

## Step 3: Gather

Count the chosen Beacon and window first (free); note effective dates and allowance. Inspect the live schema before narrowing. Use only supported focus fields; never invent filters or alter saved Beacon scope. Pull bounded pages, or diversify by date when useful, within the allowance. Check quota before additional pulls. Disclose material coverage limits when needed; do not claim exhaustive coverage.

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

### Resolve decision-critical gaps before writing

For shortlisted launches, resolve a missing fact when it could change the ranking or
the user's next action: for example the access route, release stage, price, license
or compatibility. A short Claim list is not the boundary of the available evidence.

1. Read the full retained Claims and supporting quotes, then the complete Brief.
   Treat the Brief's takeaways and unresolved questions as leads, not new source
   facts; check whether the evidence already answers them.
2. If the answer is still missing or conflicting, use available read-only web tools
   to open the original announcement and, when needed, its official product docs,
   pricing, release notes or model card. Search within the publisher's official
   sites to locate the exact product/version if a link fails or is ambiguous.
   Do this yourself before assigning a publicly answerable check to the user.
3. Record the source URL, date checked, exact product/version, supported answer and
   any relevant plan, region or rollout qualifier. Keep web-verified additions
   visibly distinct from Synorb Claims; never assign them a Synorb confidence label
   or silently rewrite the original Claim. Prefer current official terms for a
   current-access decision, explaining a material change since the announcement.
4. Reassess the recommendation and any table or visual with the resolved facts.
   Public API availability, an enterprise admin toggle, and future open weights are
   separate access routes; one does not determine the others. Published availability
   does not prove this user's account, credits or permissions are configured.

Keep this investigation proportional: at most two targeted lookup rounds within
the existing refinement budget, focused on facts that change the decision. A round
may inspect the relevant official pages for the shortlisted products. Stop when
the material question is answered, the tools or allowance prevent further checks,
or those rounds are exhausted. Do not sign up, buy, log in, change accounts or make
a paid test call to establish access. If the fact remains unresolved, state what
was checked and the specific remaining limitation briefly; make the recommendation
conditional or choose an actionable alternative. Do not repeat a resolved question
as a caveat or use a search snippet alone as verified evidence.

### Check the actual pricing route

A product site, membership plan and developer API can have different billing
pages. A localized price card is not evidence that other public API prices are
unknown. When region or currency affects the decision, follow the publisher's
official links or search its official international or regional developer platform
for the exact model/version and access route before deferring that question.
Include this check within the targeted lookup rounds above.

If the user's region is unspecified, do not infer it from a time zone, name or
language. Report the relevant published route with its currency, billing units
and qualifiers; private eligibility remains a separate question. Prefer published
rates in the same currency for a comparison when available. Do not invent an
exchange rate or treat a domestic rate as an international quote. Public list
prices can be compared without pretending to know the user's negotiated terms
or total workload cost.

## Step 5: Write the radar

Lead with the release most relevant to the user's decision. Prioritize concrete fit, access and what changed, supported by each announcement; give a fit judgment and specific reason when the user’s decision and evidence permit. Explain material tradeoffs and avoid turning a general roundup into a generic governance or evaluation plan. Use these sections when they help; do not force a fixed count or pad thin coverage:

1. **Key launches.** A small set ranked by the user's actual priorities. Include availability status, exact supported figures and source links.
2. **Other releases.** Brief links when useful to the request.
3. **What to watch.** Supported next steps or implications, labelled as your view.

Say "the company says" for claims about the company's own product. Preserve exact Claim confidence in evidence records; natural attribution in prose must retain the original certainty and hedges. A company Stream carries its own posts: do not represent these as independent reviews, and avoid repeating that qualification after every item.
Map releases to the user's stack, roadmap, buying criteria or investment question only when that context is available. Distinguish announced, preview, waitlist and generally available status when supported. Include material counterevidence or uncertainty and what changed since the last radar, when state is available.
Check availability for each release separately. A comparable product does not inherit another product's preview or general-availability status.
For a multi-product decision, use a compact comparison table with a separate availability cell for each product.
Use the status supported by that product's own sources after the checks above.
Write "not established after checking [sources]" only for a material unresolved status;
do not call a fact unknown merely because it is absent from the selected Claims.
Use this table to check the narrative before delivery; never combine unknown and known statuses into one group description.
For a cost decision, suggest concrete checks for billing units, retries, failures, minimums, limits and overages when relevant.
Resolve material public terms before delivery. Reserve questions for facts that
remain unavailable or require the user's private account or intended workload.
Any workload calculation needs supported inputs and clear assumptions.

### Compare what is actually comparable

Keep the product family, exact variant and billing route together. Before a
family-wide economic or capability judgment, check the relevant standard and
specialized offerings in the evidence. A premium variant's rate or extra billable
work does not establish the economics of every route. The ranking can stay the
same when supported; make its actual basis and scope precise.

Use a comparable priced subset when it explains the decision. A protocol,
unpriced release or differently billed product need not appear in the same
numeric chart. Before rejecting a useful price visual for mixed currencies,
complete the public pricing-route checks above; use the supported common units
and route, and identify omissions. Do not turn token-price bars into a quality
ranking or an estimate of the user's bill. Choose prose or a table when a chart
still adds no useful explanation.

Before delivery, check that each recommendation follows from this user’s priorities and the product’s own resolved access and economic terms, and that a different priority could change the ranking. Once public terms are verified, give their answers directly. Keep residual private
eligibility or workload unknowns in one concise place where they affect the next
action. Do not repeat the same caution in the lead, comparison and closing, or
present a resolved public question as still open.

## Step 6: Set the schedule

This first radar is the setup run. Agree the schedule and where the radar goes. The default is every Sunday evening (`lookback_hours=192`); daily (`48`) also works.
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later radar lists only launches you have not reported.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the radar.
