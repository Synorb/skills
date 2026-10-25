# Synorb Skills

Agent Skills for [Synorb](https://synorb.com). Set a skill up once: your agent runs it on your Synorb Beacons on a schedule and reports back, every fact with its source. A Monday newsletter in your voice, a weekly research memo, a podcast episode, a launch radar.

Synorb follows AI companies, VC firms, private companies and business and technology podcasts, plus SEC filings and central banks. Each item is the publisher's own post, episode or filing, structured into Claims with confidence labels and a source link. Synorb makes no model call when it serves a request. Your own model writes the result.

## Install

```bash
npx skills add Synorb/skills
```

One skill:

```bash
npx skills add Synorb/skills --skill newsletter-writer
```

No terminal? Paste a phrase into any agent that can read a link:

- **Synorb Setup**: `Read https://synorb.com/skills/synorb-setup.md and follow it to connect Synorb for me.`
- **Newsletter Writer**: `Read https://synorb.com/skills/newsletter-writer.md and follow it to set up my weekly newsletter.`
- **Research Associate**: `Read https://synorb.com/skills/research-associate.md and follow it to set up a weekly memo on what VC firms publish.`
- **Podcast Producer**: `Read https://synorb.com/skills/podcast-producer.md and follow it to set up my weekly podcast episode.`
- **Launch Radar**: `Read https://synorb.com/skills/launch-radar.md and follow it to set up a weekly radar of what AI companies ship.`
- **Thesis Tracker**: `Read https://synorb.com/skills/thesis-tracker.md and follow it to set up a monthly tracker of what VC firms say about my space.`
- **Podcast Digest**: `Read https://synorb.com/skills/podcast-digest.md and follow it to set up my weekly podcast digest.`

## Skills

| Skill | What it does | See it |
| --- | --- | --- |
| [`synorb-setup`](skills/synorb-setup/SKILL.md) | Connect Synorb once, see a first cited briefing, and set up the Beacons your skills run on. | [sample](samples/synorb-setup/2026-10-25-seed-investor-setup.md) · [page](https://synorb.com/skills/synorb-setup) |
| [`newsletter-writer`](skills/newsletter-writer/SKILL.md) | Set it up once. Every Monday your agent writes a new issue in your voice, every item cited. | [sample](samples/newsletter-writer/2026-10-25-the-agent-economy.md) · [page](https://synorb.com/skills/newsletter-writer) |
| [`research-associate`](skills/research-associate/SKILL.md) | Set it up once. Every week your agent sends a cited memo from any Beacon, with a timeline and open questions. | [sample](samples/research-associate/2026-10-25-vc-firms-this-week-memo.md) · [page](https://synorb.com/skills/research-associate) |
| [`podcast-producer`](skills/podcast-producer/SKILL.md) | Set it up once. Every week your agent writes a two-host episode script, or a short spoken briefing every morning. | [sample](samples/podcast-producer/2026-10-25-signal-hour-episode.md) · [page](https://synorb.com/skills/podcast-producer) |
| [`launch-radar`](skills/launch-radar/SKILL.md) | Set it up once. Every week your agent reports what AI companies shipped, from their own announcements. | [sample](samples/launch-radar/2026-10-25-ai-launch-radar.md) · [page](https://synorb.com/skills/launch-radar) |
| [`thesis-tracker`](skills/thesis-tracker/SKILL.md) | Set it up once. Every month your agent reports what VC firms published, mapped to your thesis. | [sample](samples/thesis-tracker/2026-10-25-vc-thesis-tracker.md) · [page](https://synorb.com/skills/thesis-tracker) |
| [`podcast-digest`](skills/podcast-digest/SKILL.md) | Set it up once. Every week your agent sends the arguments from the top business and tech podcasts. | [sample](samples/podcast-digest/2026-10-25-weekly-podcast-digest.md) · [page](https://synorb.com/skills/podcast-digest) |

Every skill starts by checking the Synorb connection. With none, it follows `synorb-setup`, which gets a free demo key with no email or card. The first run is the setup; later runs report only what is new.

## By agent type

| Agent type | How to install |
| --- | --- |
| Personal Agents | Copy the phrase and paste it into your agent. The agent reads the hosted skill page and follows it. |
| Chat Assistants | Upload the skill as a ZIP where your assistant takes skills. One-click directory listings are coming; ours are in review. Or paste the phrase into a chat. |
| Coding Agents | Install from the public repo with one command. The skills land in your agent's skills folder. |
| Horizontal Agents | Import a workflow template. It calls the Synorb REST API and hands the result to your model step. |
| Computer Agents | Download the skill folder and put it in the folder where your agent reads skills. |
| Voice Agents | Use the voice pack. It has a system prompt and the Synorb MCP settings. |

- Workflow recipe: [`packs/workflow-recipe.md`](packs/workflow-recipe.md)
- Voice pack: [`packs/voice-pack/`](packs/voice-pack/)
- Gallery and per-skill install pages: https://synorb.com/skills
- Machine-readable catalog: https://synorb.com/skills.json

### Plugin manifests

This repo also carries manifests for agents that install plugins from a repository. They follow each tool's published format. Synorb has not yet tested every one of them; the `npx skills` path above is tested.

- `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`: a Claude Code plugin marketplace with one plugin. `claude plugin marketplace add Synorb/skills`, then `claude plugin install synorb@synorb-skills`.
- `plugin.json`: a portable agent plugin (Codex and other hosts that read root `plugin.json` with `skills/`).
- `gemini-extension.json`: a Gemini CLI extension. `gemini extensions install https://github.com/Synorb/skills`.

## What is inside a skill

Plain Markdown: `SKILL.md`, `references/synorb-api.md` (the Synorb calls and rules, the same in every skill) and optional `assets/` templates. No scripts, no binaries. Read every file before you install it.

## Samples

`samples/` holds real output. Each file shows the request, the result as delivered, and every Synorb call the agent made, from a live test against production Synorb.

## Links

- Synorb: https://synorb.com
- Agent guide: https://synorb.com/agent-guide.md
- MCP server: `https://mcp.synorb.com/mcp`
- Free key: https://synorb.com/connect/start

## License

MIT. See [LICENSE](LICENSE).
