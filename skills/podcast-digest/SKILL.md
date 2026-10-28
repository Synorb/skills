---
name: podcast-digest
description: Summarize what the top business and technology podcasts said this week - the arguments, predictions, numbers and guests - from Synorb's Business & Technology Podcasts Beacon, so the user gets the ideas without the hours of listening. Every point links to its episode. Use when the user asks what podcasts said, wants a podcast roundup, asks what a show or a guest argued, or wants the takeaways from episodes they missed. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.2"
  homepage: https://synorb.com/skills/podcast-digest
---

# Podcast digest

You turn this week's episodes into the arguments worth knowing, each linked to its episode.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). If a visual helps explain a comparison or argument, read [references/visuals.md](references/visuals.md); a companion is optional show-note material, not a replacement for the digest.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the actual speakers and arguments, listener usefulness and any disagreement supported by sources. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/podcast-digest`.

## Step 2: Set the scope

1. Default scope: the Business & Technology Podcasts starter Beacon (`tag="starter"`).
2. If the user names shows or hosts, keep the Beacon and rank those shows first. If a named show is not in the Beacon, say so.
3. Window: 7 days (`lookback_hours=168`).
4. Use the current request and relevant available memory, project context and prior feedback to identify the user's interests, purpose, expertise and listening priorities. Do not ask again for known context; ask only when an unresolved choice materially changes the digest.

## Step 3: Gather

Count the chosen Beacon and window first (free); note effective dates and allowance. Inspect the live schema before narrowing. Use only supported focus fields; never invent filters or alter saved Beacon scope. Pull bounded pages, or diversify by date if needed to check named shows or priorities, within allowance. Disclose what you inspected; do not claim exhaustive coverage.

## Step 4: Pick episodes

Rank episodes by how useful their Claims are to this user: a clear argument, a prediction, a number, a named guest.
Skip episodes that are off-topic for the user, even when the Beacon returned them.

## Step 5: Write the digest

Choose only as many episodes as the user's listening purpose needs; four to six is a ceiling when coverage supports it, not a target. For each:

- **Show and episode title**, with the date and the episode link.
- **The argument** in a concise account built from the Claims and supporting quotes.
- **Predictions** as predictions: "the guest expects", "the host predicts". Never as facts.
- **One quote** if a supporting quote is short and strong. Quote it exactly.

Name a speaker only when a Claim, a quote or the episode title names that person. Otherwise say "a guest" or "the hosts".
Explain each episode's distinctive argument and why it merits listening for this user. Do not turn available internal project or evaluation context into the digest unless requested. Add cross-show threads only when evidence supports a useful connection; link episodes and label your synthesis as your reading. Include material counterarguments and uncertainty. Compare with the prior digest when state is available, and explain substantive updates instead of repeating items unchanged.
Call speakers' positions a disagreement only when the supplied arguments conflict. Otherwise describe a possible tension or an open question.
Before claiming a conflict, identify the two propositions that cannot both hold under the same conditions.
If both can hold, describe different emphases. If excerpts lack the needed detail, say direct disagreement is not established.

## Step 6: Set the schedule

This first digest is the setup run. Agree the schedule and where the digest goes. The default is every Sunday evening (`lookback_hours=192`).
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later digest covers only episodes you have not reported. For a spoken version, the `podcast-producer` skill writes one.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the digest.
