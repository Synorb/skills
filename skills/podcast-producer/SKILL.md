---
name: podcast-producer
description: Produce an agentic podcast from any Synorb Beacon - a two-host script with voice stage directions, or a 60 to 90 second spoken briefing - for the user's own text-to-speech tool or voice agent to read. Every segment is grounded in cited Claims from AI companies, VC firms, private companies and business podcasts. Use when the user asks for a podcast episode, an audio briefing, a script for TTS, a morning voice update, or something to listen to. Set it up once; the agent then runs it on a schedule and reports only what is new.
license: MIT
metadata:
  author: synorb
  version: "1.5.4"
  homepage: https://synorb.com/skills/podcast-producer
---

# Podcast producer

Create one finished script for the intended listener, unless the user explicitly asks for variants. Give it a source-grounded story, tension and takeaway that reward listening; use the listener’s actual interests to select and interpret evidence, without inventing private facts.
You write the script. The voice comes from the user's own voice agent or text-to-speech tool. Say so when you deliver.
Read [references/synorb-api.md](references/synorb-api.md) for every call and rule. Before choosing coverage or writing, read [references/output-quality.md](references/output-quality.md). Read [references/voice-directions.md](references/voice-directions.md) only when stage directions are useful. If a visual would clarify a comparison, read [references/visuals.md](references/visuals.md); use a companion visual only when it helps and the host can create and verify it.

Before delivering, the calling agent must complete the same-invocation draft → critique → revise → verify procedure in [references/output-quality.md](references/output-quality.md), checking the requested script or briefing, listener tone, spoken pacing and source fidelity. Deliver only the final result.

## Step 1: Check the connection

Follow section 1 of the reference. If there is no connection, follow `synorb-setup` with the skill name `synorb-skill/podcast-producer`.

## Step 2: Pick the format

Use the current request and relevant available context to fit the listener, purpose, expertise, constraints, tone, and length. Do not repeat questions answered in memory or project context. Ask only when an unresolved choice changes the script materially. Choose the format that fits:

| Format | Length | Use |
| --- | --- | --- |
| **Episode** | Usually 4 to 10 minutes | Two hosts and a few segments, adjusted to the evidence and requested length. |
| **Spoken briefing** | 60 to 90 seconds, about 150 to 220 words | One voice, about three items by default. For voice agents and morning updates. |

A shorter episode is fine when the data is thin. Do not add filler to reach a length.

Default to the episode. Use the spoken briefing when the user mentions a voice agent, a smart speaker, a commute or "short".

## Step 3: Gather

1. Scope: the user's active Beacons that fit the request. If there are none, use the AI Companies starter Beacon as a fallback and say what it covers.
2. Window: 7 days for an episode (`lookback_hours=168`), the last two days for a spoken briefing (`lookback_hours=72`, because windows round to whole days).
3. Count the chosen Beacon and window first (free); check dates and allowance. Inspect the live schema and use only supported focus fields; never invent filters or change saved scope. If needed, diversify bounded pages or date slices within allowance. Disclose material coverage limits when needed; do not claim exhaustive coverage.
4. Pick items that fit this listener and are easy to say aloud. Skip off-topic items, how-to guides and items that require a visual to understand when a spoken explanation would not work.
5. Use `presentation_items[].supporting_quotes` to check each line a host says.

## Step 4: Write the episode

Two hosts:

- **Host A (lead)** sets up each story and keeps time.
- **Host B (analyst)** adds the "so what" and asks the obvious question.

Use this as a flexible default structure; adjust segment count and order to the evidence and listener's purpose:

Choose a compelling, evidence-backed through-line for this listener. Build a spoken story with concrete detail, a real tension or question, and natural transitions; each segment should advance it toward a substantive payoff rather than merely repeat the prompt as a question. Avoid repetitive generic advice and audit narration. Attribute naturally aloud, keep material qualifications near the claim once, and put routine coverage and operational diagnostics in the show notes or a separate receipt. Keep internal project or evaluation context out unless the requested episode is about it.

1. Cold open: one line that hooks on the best item.
2. Intro: date and what is coming; include a show name only if the user supplied or established one. Otherwise keep it unbranded. Host A and Host B are usable roles; suggest names separately only if requested. A descriptive episode title is fine. Keep the intro to 20 seconds.
3. Segments: one per item. The lead states what happened with the figure. The analyst explains why it matters. Name the source aloud ("Higgsfield said on its blog...").
4. Wrap: resolve the story or leave the listener with its supported implication, then sign off.

Write numbers the way a person says them: "one billion dollars", not "$1B". Spell out abbreviations on first use.
Each segment ends with a source line in brackets. It is for the show notes, not for reading aloud.

## Step 5: Write the spoken briefing

One voice, usually 60 to 90 seconds. Choose only the items this listener needs; use fewer for thin evidence or a narrower request. Give each enough setup and detail to make the point clear, then direct listeners to the source notes. No stage directions except pauses.
Check the spoken text against the requested time and language. If the listener asks for no acronyms, use plain words throughout.
Keep URLs, evidence tables and coverage detail in show notes, outside the spoken script.

## Step 6: Add voice directions

Use the tags in the voice-directions reference only when the requested delivery benefits from them. Keep the voice tool separate from the script; do not claim to generate audio unless an available tool actually does so.
If the user names a TTS service, check its own markup rules before you add tags. If you are not sure, give plain text plus the directions in brackets.

## Step 7: Deliver

Give, in this order:

1. The script.
2. Show notes: one line per item with its source link.
3. An estimated run time (150 words is about one minute), when useful.

Estimate from spoken words only. Check that the script fits the requested duration before delivery.

This first script is the setup run.

## Step 8: Set the schedule

Agree the schedule and where the script goes. The defaults: an episode every Friday (`lookback_hours=192`), or a spoken briefing every weekday morning (`lookback_hours=72`).
Then follow "Set it up once, then run on a schedule" in section 3 of the reference. Each later script covers only what is new since the last one.
If `account_notice.user_message` is in a response, give that sentence once, after the script.

## Rules for this skill

- The hosts say only what the Claims support. Banter is fine. New facts are not.
- Say who the source is. Organization Streams are the organization's own publications, so say "Anthropic announced", not "reports say".
- Keep confidence in the words: "the company says", "the data shows", "they suggest".
- Keep sourced facts distinct from host interpretation. Include material disagreement or uncertainty in plain speech, and make clear what changed from the previous script when prior state is available.
- Read the script aloud in the refinement pass: does its story have a listener-specific payoff and sound like speech, with source details easy to find in the notes?
