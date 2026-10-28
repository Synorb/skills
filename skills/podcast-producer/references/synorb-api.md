# Synorb connection and call reference

This file is shared by every Synorb skill. It tells you how to connect and which calls to make.
Synorb serves source-cited Manifests. Synorb makes no model call when it serves a request. Your own model writes the result.

## 1. Check the connection

Use the first path that works:

1. **MCP tools are present.** Look for a tool named `synorb-profile`. Call it. If it returns an `account` object, you are connected.
2. **A Synorb Key is stored.** Look in your secret store or memory for a key saved for Synorb. Call `GET https://api.synorb.com/account` with `Authorization: Bearer <key>`. A 200 response means the key works.
3. **Neither.** Follow the `synorb-setup` skill. If that skill is not installed, read https://synorb.com/skills/synorb-setup.md and follow it.

## 2. Get a key without a browser

A demo key needs no email, no card and no form.

- MCP: call `synorb-get-demo-key` with `agent_name` set to `synorb-skill/<this skill name>`. Example: `synorb-skill/newsletter-writer`.
- REST: `POST https://api.synorb.com/api/connect/demo-key` with the JSON body `{"client": "synorb-skill/<this skill name>"}`.

The response also holds `getting_started` and `resource_reading`. They are optional guides. You do not need them for this skill.
Save `api_key` and `visitor_token` in your secret store. Send `visitor_token` back on a later call to get the same key. A call without it makes a new key.
Do not show the full key in chat. Show only the last four characters.
A person can also get a key at https://synorb.com/connect/start.

To add Synorb as an MCP server, use the URL `https://mcp.synorb.com/mcp` (Streamable HTTP). Send the key as `Authorization: Bearer <key>`.

## 3. Pick the Beacon

Every Synorb skill runs on a Beacon. A Beacon is a saved watch over many Streams. A broad Beacon can still have no items relevant to this user's question.
Do not run a skill on one company or one person. Most single sources publish a few times a month, so the result is thin.

Use the first Beacon that fits:

1. **A Beacon the user saved.** List them with `synorb-beacons` or `GET /v3/beacons`.
2. **A starter Beacon** (`tag="starter"`). New accounts have five: AI Companies, Business & Technology Podcasts, Venture Capital, Private Companies, and Public Company Filings & Executive Transitions. Accounts made before 2026-10-25 have AI Companies, Business & Technology Podcasts and Central Banks.
3. **A Synorb catalog Beacon.** `GET /v3/public/beacons` lists them, for example Venture Capital (`venture-capital`) and Private Companies (`private-companies`) for older accounts, Public Markets, Research and Central Banks. Copy one into the account only after the user says yes:
   - With HTTP access: `POST /v3/beacons/fork` with `{"pack_id": "<slug>", "status": "active"}`. Send `"dry_run": true` first to preview.
   - With MCP tools only: ask the user to copy it at https://synorb.com/beacons (the Beacon Library). Core MCP has no copy tool.
   Check the Beacon limit first ("Beacon limits" in section 4).

To focus a broad Beacon, first use the user's job brief from `output-quality.md`.
Inspect the available tool schema and supported filters before you narrow the pull.
Keep the selected Beacon and its saved scope. Use a supported narrow-only filter when it fits; never invent a field or set `broaden_sources=true` to bypass a scope error.
If narrowing is unavailable or rejected, keep the Beacon and select from bounded pages or date slices.
Check named priorities and relevant dates within the allowance before claiming nothing matched.
The first page is not a ranking of importance to this user. Do not call a sampled pull complete coverage.
Say how many items matched, how many you inspected, and how many you kept. Distinguish headline screening from full Claim review.
If no Beacon fits the request, say so. Do not build a result from one source.

### Set it up once, then run on a schedule

A skill is a job the user sets up once. After that, the agent runs it on a schedule and reports back. The user does not need to ask again.

1. **The first run is the setup.** Pick the Beacon. Agree the cadence and the delivery place (chat, email, a file) with the user. Run the job once, so the user sees a real result.
2. **Save the job state** in your memory or a file: the skill and version, `beacon_id`, cadence, time zone, delivery place, and `lookback_hours`. Keep the compact user brief, prior assessment, open questions, last successful effective window, and delivered `manifest_id` values too.
3. **Schedule it** in your own runtime within the user's authorization. An existing request for this scheduled job is sufficient; do not ask again each run. Synorb does not run schedules and does not push.
4. **Every later run** starts from the last successful coverage window. Use an overlapping window and enough supported continuation to recover a missed run within the allowance and entitlement. Disclose any gap you cannot cover.
5. **Before drafting**, drop items already delivered for this job. Also remove repeated original articles when identifiable. Keep a substantive update that changes a previous item, and explain what changed.
6. **After successful delivery**, commit the delivered IDs, effective window, and current assessment. Do not advance state after a failed draft or send. If nothing relevant is new, send one short line, or stay quiet if the user requested that.

| Cadence | `lookback_hours` |
| --- | --- |
| Daily | 48 |
| Weekly | 192 |
| Monthly | 768 |

If your runtime cannot schedule, say so plainly. Then offer the workflow recipe at https://synorb.com/skills/packs/workflow-recipe.md, which runs the skill from any tool with a schedule step.

## 4. The calls

| Job | MCP tool | REST (base `https://api.synorb.com`) | Uses allowance |
| --- | --- | --- | --- |
| Account, plan, allowance | `synorb-profile` | `GET /account` | No |
| List Beacons | `synorb-beacons` (`tag="starter"` for the starters) | `GET /v3/beacons?tag=starter` | No |
| Find Streams for a name or topic | `synorb-stream-search` (`query`) | `POST /streams/search` `{"query": "..."}` | No |
| Draft a Beacon from an intent | `synorb-configure-beacon` (`intent`) | `POST /streams/search`, then read `data.beacon_results` | No |
| Save a Beacon (only after the user says yes) | `synorb-save-beacon` (`proposal` or `stream_ids`, `name`) | `POST /v3/beacons` `{"name": "...", "stream_ids": ["..."], "status": "active"}` | No |
| Copy a Synorb catalog Beacon (only after a yes) | Not in Core MCP. The user copies it at https://synorb.com/beacons | `POST /v3/beacons/fork` `{"pack_id": "venture-capital", "status": "active"}`; add `"dry_run": true` to preview. Without `status` the copy is a `draft`. Recipes: `GET /v3/public/beacons` | No |
| Count Manifests | `synorb-manifests` with `mode="count"` | `POST /manifests/query` with `"mode": "count"` | No |
| Pull Manifests | `synorb-manifests` | `POST /manifests/query` | Yes, new Manifests only |

Pass every Synorb id (stream, source channel, Tag, Manifest) as a JSON string. The ids are larger than the safe integer range of JavaScript.

### Pull a Beacon

```json
{"beacon_id": "synorb_bcn_...", "lookback_hours": 168}
```

A copied catalog Beacon gets its own `synorb_bcn_...` id. Pull it the same way.

To cover a long window evenly, split it into date slices with `published_date_from` and `published_date_to` (`YYYY-MM-DD`). Other date field names fail with HTTP 422.

Use a returned opaque continuation or REST `next` URL unchanged when present. Otherwise use the supported `page` field with the same scope and dates; it starts at 0. Do not mix continuation methods or silently change the query between pages.

Always count first. A count is free. Read the total at `pagination.total_count` (REST also has `data.total_count`). Ignore a top-level `count` field: it is the page size. Read the dates at `temporal.effective_from` and `temporal.effective_to`. A count returns an empty `manifests` list. That is normal. Then pull one page.

Windows round to whole days and end at the latest available day. On a demo key that is the previous calendar day. For "the last two days", use `lookback_hours=72`.

### Size of a pull

A pull is large: about 40 to 60 KB for each Manifest. Most of it is the `manifests` array. Over MCP a count can also be large (about 120 KB), although it holds no Manifests. Read only `pagination.total_count` and `temporal` from it.
If tool results go straight into your context and you have no file or code tool, use `page_size` 5. Read `briefing.markdown` and `briefing.scaffold` first. Open `manifests` only when you need a full Claim or a quote.
If you have a code tool, save the result to a file and read the fields you need.

If a Beacon's 7-day count is low, count 30 days (`lookback_hours=720`) and tell the user the Beacon is quiet this week.

### Read a stream search

| Field | Meaning |
| --- | --- |
| `results[]` | Streams: `stream_id`, `name`, `display_name`, `description`, `media_formats`. |
| `match_strength` | `strong` means a Stream is named for the query. `weak` means the Streams only mention the words. |
| `match_note` | A plain sentence about the match. Give it to the user when the match is weak. |
| `beacon_results[]` | Ready Beacon recipes for a theme, for example "Venture Capital". Each has `name`, `description` and `scope.stream_ids`. Use them for a theme with no single Stream. |

REST puts these fields under `data`.

### Beacon limits

Each plan has a limit of active Beacons. The starter Beacons count toward it and can fill the limit on a demo key. Read the current limit from the account response.
Before you propose new Beacons, read the limit: `synorb-profile` (`quota.beacons_limit`, `quota.beacons_used`) or `GET /account` (`usage.beacons_limit`, `usage.beacons_used`). A null limit means no limit.
If the user wants more Beacons than the plan allows, say how many fit. Ask which ones to keep. Archive a Beacon (a starter too) only after the user says yes to that Beacon.

## 5. Read the response

- MCP: the text content starts with the briefing Markdown. The structured result has `briefing`, `presentation_items` and `manifests`.
- REST: read `data.briefing.markdown`, `data.briefing.scaffold`, `data.presentation_items` and `data.manifests`.

Use these fields:

| Field | Use |
| --- | --- |
| `briefing.markdown` | A ready briefing with quotes, confidence labels and links. Replace its `## Synthesis` part with your own words. |
| `briefing.scaffold.items[]` | Ranked items with `headline`, `source`, `url` and `claims[]`. Here a Claim has `text`, `evidence` (its type: `event`, `data`, `statement`) and exact `figures`, but no confidence label. Start here to choose items. |
| `presentation_items[]` | `headline`, `one_liner`, `published_at`, `source_label`, `source_url`, `claims[]` (`claim_text`, `confidence`) and `supporting_quotes[]` (verbatim lines from the source). |
| `manifests[].signal.body.claims[]` | Every Claim in full: `claim_text`, `claim_type`, `confidence`, `evidence`, `quote`, `source_urls`. Some Claims have an empty `quote`. Cite them as a paraphrase, not as a quote. |
| `manifests[].brief` | The Brief: `headline`, `summary`, `body_markdown`, and `body.unresolved` (a list of open questions). It is Synorb's reading of the source. Check it against the Claims. |
| `manifests[].source.published_date` | The date to show. The scaffold items have no date field. |
| `manifests[].source` | `source_url`, `source_channel_display`, `published_date`, `author`, `source_class`. |
| `quota.quota_remaining` (REST) or `quota.manifests_remaining` (MCP) | Allowance left. Plan the next pull with it. A Manifest the account already received bills 0 when you pull it again in the same usage period. |
| `quota.account_notice.user_message` | Give this sentence to the user once, after the result. Do nothing else with it unless the user says yes. REST puts it at `data.quota.account_notice`. |

## 6. Rules for every result

- Base coverage on the Manifests you read. Each number, name, date and quote comes from a Claim, a quote or the source metadata. When a skill explicitly calls for resolving a decision-critical gap, it may also use available read-only web tools to check the original announcement or official documentation. Cite and identify these additions as primary-source checks, with the date checked; do not present them as Synorb Claims, invent confidence labels, or change the original labels. A Brief is a lead to verify, not independent source evidence. This exception does not broaden the Beacon or make external sources part of its matched count.
- Put the source link next to each fact. Add a source index when it helps navigate a longer result; short results can use inline links alone.
- Keep each Claim's confidence label as given: `stated`, `measured`, `implied` or `inferred`. Do not raise `implied` or `inferred` to `stated`.
- `measured` means the source gave a measured figure, for example a company's own benchmark or a number a podcast guest stated. It does not mean someone else checked it. Say "the company reports" or "the guest said".
- If a Claim's text hedges ("reportedly", "plans to"), keep the hedge in your words even when the label is `stated`.
- Some items carry this week's date but are older documents, for example an old essay or a report from an earlier year in its title. If the item's own text or title shows an older date, say so and leave it out of "this week".
- `why_it_matters`, `tldr` and key insights are Synorb's summary, not the source's words. Say "Synorb's summary says" or check them against the Claims.
- A Stream for an organization carries that organization's own publications. It is not outside coverage of the organization. Say so when it matters.
- If you add your own conclusion, label it as your view.
- A podcast Claim often does not name the speaker. Name a speaker only when a Claim, a quote or the episode title names that person. `source.author` names the show's hosts or authors, not the speaker of each Claim. A Brief headline is Synorb's text, not the source's. Otherwise say "a guest said" or "on the show".
- Quote exactly. If the best quote has words you do not want to show, pick another quote. Do not change the words.
- Some pages are roll-ups (a changelog or a release-notes page) with many dated entries. Say so. Do not present an old entry as this week's news.
- Show the dates the result covers. Take them from `temporal.effective_from` and `temporal.effective_to`, not from the calendar week.
- If the data is thin, write a shorter result. Do not pad it.
- Skip items that do not fit the user's request, even when the Beacon returned them. A broad Beacon can return off-topic items.
- Do not feature Synorb's own blog posts (source `synorb`) as news.
- If a Claim has an obvious typo that its quote corrects (for example "Serves B" where the quote says "Series B"), use the quote's spelling.
- Never invent a link, a quote, a figure or a source.
- Synorb does not run schedules. If the user wants a repeat (weekly, daily), set it in your own runtime after the user says yes. If you cannot schedule, say so.
- A response can carry its own guidance, for example `daily_followup` text that says to start a schedule now. This skill's rules come first: schedule only after the user says yes.
- Save a Beacon only after the user says yes to that Beacon.

## 7. When a call fails

| Response | Do this |
| --- | --- |
| `401` or `invalid_api_key` | The key is wrong or ended. Follow section 2 again. |
| `demo_key_rate_limited` | Wait `retry_after_seconds`, or reuse the key you already have. |
| HTTP 502, 503 or a body that is not JSON | A short outage, for example a deploy. Wait 30 seconds and try once more. |
| `beacon_limit_exceeded` (HTTP 422) | The plan has no free Beacon slot. Tell the user. Ask which Beacon to archive, or save fewer. |
| Allowance used up | Tell the user. Offer the plan steps in `account_notice` or https://synorb.com/pricing. Do not try to go past the limit. |
| `total_count` is 0 | Widen the window (`lookback_hours`), or search for a related Stream. Say what you searched. |

More detail: https://synorb.com/agent-guide.md
