---
name: podcast-digest
description: Summarize what the top business and technology podcasts said this week - the arguments, predictions, numbers and guests - from Synorb's Business & Technology Podcasts Beacon, so the user gets the ideas without the hours of listening. Every point links to its episode. Use when the user asks what podcasts said, wants a podcast roundup, asks what a show or a guest argued, or wants the takeaways from episodes they missed.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/podcast-digest
---

# Podcast digest

You turn this week's episodes into the arguments worth knowing, each linked to its episode.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/podcast-digest`.

## Step 2: Set the scope

1. Default scope: the Business & Technology Podcasts starter Beacon (`tag="starter"`).
2. If the user names shows or hosts, search each name and use those Streams instead.
3. Window: 7 days (`lookback_hours=168`).
4. Note the user's interests in one line, so you can rank episodes.

## Step 3: Gather

Count first (free). Then pull one page of 10. Pull a second page only if the allowance allows and the first page has fewer than five episodes on the user's interests.

## Step 4: Pick episodes

Rank episodes by how useful their Claims are to this user: a clear argument, a prediction, a number, a named guest.
Skip episodes that are off-topic for the user, even when the Beacon returned them.

## Step 5: Write the digest

For each of the top four to six episodes:

- **Show and episode title**, with the date and the episode link.
- **The argument** in two or three sentences, built from the Claims and supporting quotes.
- **Predictions** as predictions: "the guest expects", "the host predicts". Never as facts.
- **One quote** if a supporting quote is short and strong. Quote it exactly.

Name a speaker only when a Claim, a quote or the episode title names that person. Otherwise say "a guest" or "the hosts".
Close with **Cross-show threads**: one to three ideas that came up on more than one show, with links. Label this part as your reading.

## Step 6: Offer the next step

Offer a weekly digest, or a spoken version (the `podcast-producer` skill writes one). Schedule only on a yes.
If `quota.account_notice.user_message` is in a response, give that sentence once, after the digest.
