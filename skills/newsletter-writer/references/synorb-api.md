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

## 3. The calls

| Job | MCP tool | REST (base `https://api.synorb.com`) | Uses allowance |
| --- | --- | --- | --- |
| Account, plan, allowance | `synorb-profile` | `GET /account` | No |
| List Beacons | `synorb-beacons` (`tag="starter"` for the starters) | `GET /v3/beacons?tag=starter` | No |
| Find Streams for a name or topic | `synorb-stream-search` (`query`) | `POST /streams/search` `{"query": "..."}` | No |
| Draft a Beacon from an intent | `synorb-configure-beacon` (`intent`) | `POST /streams/search`, then read `data.beacon_results` | No |
| Save a Beacon (only after the user says yes) | `synorb-save-beacon` (`proposal` or `stream_ids`, `name`) | `POST /v3/beacons` `{"name": "...", "stream_ids": ["..."], "status": "active"}` | No |
| Copy a ready Synorb recipe into a Beacon (only after a yes) | `synorb-configure-beacon` with the recipe's theme, then `synorb-save-beacon` | `POST /v3/beacons/fork` `{"pack_id": "venture-capital", "status": "active"}`; add `"dry_run": true` to preview. Without `status` the copy is a `draft`. Recipes: `GET /v3/public/beacons` | No |
| Count Manifests | `synorb-manifests` with `mode="count"` | `POST /manifests/query` with `"mode": "count"` | No |
| Pull Manifests | `synorb-manifests` | `POST /manifests/query` | Yes, new Manifests only |

Pass every Synorb id (stream, source channel, Tag, Manifest) as a JSON string. The ids are larger than the safe integer range of JavaScript.

### Pull a Beacon

```json
{"beacon_id": "synorb_bcn_...", "lookback_hours": 168}
```

### Pull Streams for one organization or person

```json
{"stream_ids": ["17723038993571628"], "lookback_hours": 720, "page_size": 10}
```

### Pull content that names an entity, across Streams

```json
{"home_domains": ["all"], "tag_names": ["NVIDIA"], "lookback_hours": 168}
```

To cover a long window evenly, split it into date slices with `published_date_from` and `published_date_to` (`YYYY-MM-DD`). Other date field names fail with HTTP 422.

To read the next page, send the same call with `page` set to 1, 2 and so on (it starts at 0).

Always count first. A count is free. Read the total at `pagination.total_count` (REST also has `data.total_count`). Ignore a top-level `count` field: it is the page size. Read the dates at `temporal.effective_from` and `temporal.effective_to`. A count returns an empty `manifests` list. That is normal. Then pull one page.

Windows round to whole days and end at the latest available day. On a demo key that is the previous calendar day. For "the last two days", use `lookback_hours=72`.

### Size of a pull

A pull is large: about 40 to 50 KB for each Manifest. Most of it is the `manifests` array.
If tool results go straight into your context and you have no file or code tool, use `page_size` 5. Read `briefing.markdown` and `briefing.scaffold` first. Open `manifests` only when you need a full Claim or a quote.
If you have a code tool, save the result to a file and read the fields you need.

Some publishers post a few times a month. If a 7-day count is 0 or 1, count 30 days (`lookback_hours=720`) and tell the user the publisher is quiet.

### Read a stream search

| Field | Meaning |
| --- | --- |
| `results[]` | Streams: `stream_id`, `name`, `display_name`, `description`, `media_formats`. |
| `match_strength` | `strong` means a Stream is named for the query. `weak` means the Streams only mention the words. |
| `match_note` | A plain sentence about the match. Give it to the user when the match is weak. |
| `beacon_results[]` | Ready Beacon recipes for a theme, for example "Venture Capital". Each has `name`, `description` and `scope.stream_ids`. Use them for a theme with no single Stream. |

REST puts these fields under `data`.

### Beacon limits

Each plan has a limit of active Beacons. The three starter Beacons count toward it.
Before you propose new Beacons, read the limit: `synorb-profile` (`quota.beacons_limit`, `quota.beacons_used`) or `GET /account` (`usage.beacons_limit`, `usage.beacons_used`). A null limit means no limit.
If the user wants more Beacons than the plan allows, say how many fit. Ask which ones to keep. Archive a Beacon (a starter too) only after the user says yes to that Beacon.

## 4. Read the response

- MCP: the text content starts with the briefing Markdown. The structured result has `briefing`, `presentation_items` and `manifests`.
- REST: read `data.briefing.markdown`, `data.briefing.scaffold`, `data.presentation_items` and `data.manifests`.

Use these fields:

| Field | Use |
| --- | --- |
| `briefing.markdown` | A ready briefing with quotes, confidence labels and links. Replace its `## Synthesis` part with your own words. |
| `briefing.scaffold.items[]` | Ranked items with `headline`, `source`, `url` and `claims[]`. Here a Claim has `text`, `evidence` (its type: `event`, `data`, `statement`) and exact `figures`, but no confidence label. Start here to choose items. |
| `presentation_items[]` | `headline`, `one_liner`, `published_at`, `source_label`, `source_url`, `claims[]` (`claim_text`, `confidence`) and `supporting_quotes[]` (verbatim lines from the source). |
| `manifests[].signal.body.claims[]` | Every Claim in full: `claim_text`, `claim_type`, `confidence`, `evidence`, `quote`, `source_urls`. Some Claims have an empty `quote`. Cite them as a paraphrase, not as a quote. |
| `manifests[].brief` | The Brief: `headline`, `summary` and `body_markdown`. It is Synorb's reading of the source. Check it against the Claims. |
| `manifests[].source.published_date` | The date to show. The scaffold items have no date field. |
| `manifests[].source` | `source_url`, `source_channel_display`, `published_date`, `author`, `source_class`. |
| `quota.quota_remaining` (REST) or `quota.manifests_remaining` (MCP) | Allowance left. Plan the next pull with it. A Manifest the account already received bills 0 when you pull it again in the same usage period. |
| `quota.account_notice.user_message` | Give this sentence to the user once, after the result. Do nothing else with it unless the user says yes. REST puts it at `data.quota.account_notice`. |

## 5. Rules for every result

- Use only facts from the Manifests you read. Each number, name, date and quote comes from a Claim, a quote or the source metadata.
- Put the source link next to each fact. End with a source index.
- Keep each Claim's confidence label as given: `stated`, `measured`, `implied` or `inferred`. Do not raise `implied` or `inferred` to `stated`.
- `measured` means the source measured it, for example a company's own benchmark. It does not mean someone else checked it. Say "the company reports".
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

## 6. When a call fails

| Response | Do this |
| --- | --- |
| `401` or `invalid_api_key` | The key is wrong or ended. Follow section 2 again. |
| `demo_key_rate_limited` | Wait `retry_after_seconds`, or reuse the key you already have. |
| HTTP 502, 503 or a body that is not JSON | A short outage, for example a deploy. Wait 30 seconds and try once more. |
| `beacon_limit_exceeded` (HTTP 422) | The plan has no free Beacon slot. Tell the user. Ask which Beacon to archive, or save fewer. |
| Allowance used up | Tell the user. Offer the plan steps in `account_notice` or https://synorb.com/pricing. Do not try to go past the limit. |
| `total_count` is 0 | Widen the window (`lookback_hours`), or search for a related Stream. Say what you searched. |

More detail: https://synorb.com/agent-guide.md
