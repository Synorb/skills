# Sample: synorb-setup, seed-stage investor

- Skill: synorb-setup (v1.0.0)
- Date: 2026-10-25
- Tested live against production Synorb over REST, demo key (ends c36f)

## User request

> I'm a seed-stage investor. I care about AI agent startups, Sequoia, and Andreessen Horowitz. Set me up with Synorb.

## Conversation

**Agent:** I am connecting Synorb and getting a free demo key. This takes a minute.

**Agent:** You are connected. I saved a free 72-hour demo key (ends in c36f) and its visitor token in a local file in my working folder (skilltest/setup/key.txt and vt.txt). It has 25 Manifests and expires Oct 28. I can add Synorb as an MCP server (https://mcp.synorb.com/mcp) if you want that. Say yes and I will.

You already told me what you care about, so here is a first result from the AI Companies starter Beacon (864 items this week, I pulled 5):

1. Higgsfield extended its Series B with new money from TCV and NVIDIA, reaching a $1B ARR run rate 18 months after launch. 2026-10-23. [Higgsfield Blog](https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia)
2. Legora raised $550M at an $8.8B valuation for its agentic legal operating system. 2026-10-23. [Legora Blog](https://legora.com/blog/scaling-fast-built-to-last)
3. Tempus AI and Bristol Myers Squibb signed a multi-year deal through 2031 for drug discovery. 2026-10-23. [Tempus IR](https://investors.tempus.com/news-releases/news-release-details/tempus-expands-strategic-collaboration-bristol-myers-squibb-0)
4. Wayve, Stellantis and NVIDIA will deploy autonomous vehicles in France. 2026-10-23. [Wayve Press](https://wayve.ai/press/wayve-stellantis-nvidia-collaborate-on-deployment-across-france)
5. The U.S. Navy picked Applied Intuition to field its AI perception system, starting with five destroyers. 2026-10-22. [Applied Intuition](https://www.appliedintuition.com/press-releases/navy-selects-applied-intuition-field-ai-perception)

These come from the companies' own publications, via Synorb. (One-liners are Synorb's summaries.)

**Agent:** Here are the Beacons I suggest. Shall I save them?

1. **Sequoia Capital**: Sequoia's own stream plus the Crucible Moments podcast (7 items in 30 days, so a weekly window is often quiet).
2. **Andreessen Horowitz**: the a16z stream plus Martin Casado's a16z author stream (54 items in 30 days).
3. **AI Agent Startups**: Synorb has no stream named for that theme (the search says "No stream is named for 'AI agent startups'"). The nearest match is the companies' own streams: Sierra, Decagon, Harvey, LangChain and Parloa (24 items in the last 7 days). These carry each company's own publications, not outside coverage.

**User:** yes, save all of them

**Agent:** Saved two of three:
- Sequoia Capital (synorb_bcn_gR6XxB72Uc5DhAa5lw-0gQ), 1 item this week
- Andreessen Horowitz (synorb_bcn_PQpoLf5gk1uQBFb3uYRhjQ), 11 items this week

The third did not save. The demo plan allows 5 active Beacons, and the 3 starters use 3 of them: "You are using all 5 active Beacons your plan includes. Disable or archive an active Beacon to make room." I did not archive anything. I can archive a starter (for example Central Banks) to make room for AI Agent Startups, or you can connect an email to move to the free Starter plan. Which do you prefer?

**Agent:** How often do you want an update?

**User:** weekly on Mondays

**Agent:** I cannot run this on a schedule. Ask me any time, or connect Synorb to a tool that can. When you ask on a Monday I will pull each Beacon with a 192-hour window and skip anything I showed you before, using the Manifest id.

Also, your demo key has 20 of 25 Manifests left and ends Oct 28. To keep your updates running after that, I can connect it to your email (free, no card, same key and Beacons, 100 Manifests a month). Want me to?

Next I can write you a weekly issue in your voice (`newsletter-writer`), a memo on one firm or company (`research-associate`), or a short spoken briefing (`podcast-producer`).

## Calls made

Base: https://api.synorb.com. All but the first use `Authorization: Bearer <key ending c36f>`.

1. `POST /api/connect/demo-key` body `{"client":"synorb-skill/synorb-setup"}` -> 200. plan `agent_demo`, manifest_quota 25, expires 2026-10-28, returns `api_key` and `visitor_token` (ends b5cc).
2. `GET /account` -> 200. manifests_limit 25, beacons_limit 5, beacons_used 3.
3. `GET /v3/beacons?tag=starter` -> 200. 3 starters: Central Banks, AI Companies (synorb_bcn_buuPMDhqsFzZF8gFI955wg), Business & Technology Podcasts.
4. `POST /manifests/query` `{"beacon_id":"synorb_bcn_buuPMDhqsFzZF8gFI955wg","lookback_hours":168,"mode":"count"}` -> 200. total_count 864, quota_charged false, remaining 25.
5. `POST /manifests/query` `{"beacon_id":"synorb_bcn_buuPMDhqsFzZF8gFI955wg","lookback_hours":168,"page_size":5}` -> 200. 5 manifests billed, quota_remaining 20.
6. `POST /streams/search` `{"query":"AI agent startups"}` -> 200. total_count 1101, match_strength weak, no stream named for the theme.
7. `POST /streams/search` `{"query":"Sequoia"}` -> 200. strong; stream `sequoia` 17723038993548157, `crucible-moments-podcast` 17744947063057448.
8. `POST /streams/search` `{"query":"Andreessen Horowitz"}` -> 200. strong; `andreessen-horowitz` 17723038993571529, `martin-casado` 17723038993578220.
9. `POST /manifests/query` mode count, Sequoia stream, 720h -> total_count 7. a16z stream, 720h -> 54. Five agent-company streams, 168h -> 24. All free, remaining 20.
10. `POST /v3/beacons` Sequoia Capital, stream_ids [17723038993548157, 17744947063057448], status active, lookback 168 -> 201, beacon_id synorb_bcn_gR6XxB72Uc5DhAa5lw-0gQ.
11. `POST /v3/beacons` Andreessen Horowitz, stream_ids [17723038993571529, 17723038993578220] -> 201, beacon_id synorb_bcn_PQpoLf5gk1uQBFb3uYRhjQ.
12. `POST /v3/beacons` AI Agent Startups, 5 stream_ids -> 422 `beacon_limit_exceeded` (message quoted above).
13. `GET /v3/beacons` -> 200. 5 active (allowance limit 5, active_count 5).
14. `POST /manifests/query` mode count for the two new Beacons, 168h -> Sequoia 1, a16z 11. Quota remaining 20.
