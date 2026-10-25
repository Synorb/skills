---
name: podcast-producer
description: Produce an agentic podcast from the user's Synorb Beacons or Streams - a two-host script with voice stage directions ready for text-to-speech or a voice agent, or a 60 to 90 second spoken briefing. Every segment is grounded in cited Claims from AI companies, VC firms, private companies and business podcasts. Use when the user asks for a podcast episode, an audio briefing, a script for TTS, a morning voice update, or something to listen to.
license: MIT
metadata:
  author: synorb
  version: "1.0.0"
  homepage: https://synorb.com/skills/podcast-producer
---

# Podcast producer

You turn this week's cited items into a script people want to hear.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule.
Stage directions are in [references/voice-directions.md](references/voice-directions.md).

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/podcast-producer`.

## Step 2: Pick the format

Ask, or infer from the request:

| Format | Length | Use |
| --- | --- | --- |
| **Episode** | 4 to 10 minutes, about 600 to 1,400 words | Two hosts, three to five segments. |
| **Spoken briefing** | 60 to 90 seconds, about 150 to 220 words | One voice, three items. For voice agents and morning updates. |

A shorter episode is fine when the data is thin. Do not add filler to reach a length.

Default to the episode. Use the spoken briefing when the user mentions a voice agent, a smart speaker, a commute or "short".

## Step 3: Gather

1. Scope: the user's active Beacons. If there are none, use the AI Companies starter Beacon.
2. Window: 7 days for an episode (`lookback_hours=168`), the last two days for a spoken briefing (`lookback_hours=72`, because windows round to whole days).
3. Count first (free). Then pull one page.
4. Pick items that fit the show's topic and are easy to say aloud: a number, a name, a clear change. Skip off-topic items, how-to guides and items that need a table to make sense.
5. Use `presentation_items[].supporting_quotes` to check each line a host says.

## Step 4: Write the episode

Two hosts:

- **Host A (lead)** sets up each story and keeps time.
- **Host B (analyst)** adds the "so what" and asks the obvious question.

Structure:

1. Cold open: one line that hooks on the best item.
2. Intro: show name, date, what is coming. Keep it to 20 seconds.
3. Segments: one per item. The lead states what happened with the figure. The analyst explains why it matters. Name the source aloud ("Higgsfield said on its blog...").
4. Wrap: one sentence per segment, then a sign-off.

Write numbers the way a person says them: "one billion dollars", not "$1B". Spell out abbreviations on first use.
Each segment ends with a source line in brackets. It is for the show notes, not for reading aloud.

## Step 5: Write the spoken briefing

One voice. Three items. For each item: one sentence of setup and two sentences of detail. Close with "Sources are in the show notes."
No stage directions except pauses.

## Step 6: Add voice directions

Use the tags in the voice-directions reference. Use them sparingly: one or two per segment.
If the user names a TTS service, check its own markup rules before you add tags. If you are not sure, give plain text plus the directions in brackets.

## Step 7: Deliver

Give, in this order:

1. The script.
2. Show notes: one line per item with its source link.
3. An estimate of the run time (150 words is about one minute).

Offer to make it a weekly show. Set a schedule only on a yes, and only if your runtime can.
If `account_notice.user_message` is in a response, give that sentence once, after the script.

## Rules for this skill

- The hosts say only what the Claims support. Banter is fine. New facts are not.
- Say who the source is. Organization Streams are the organization's own publications, so say "Anthropic announced", not "reports say".
- Keep confidence in the words: "the company says", "the data shows", "they suggest".
