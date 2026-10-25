# Synorb Skills

Agent Skills that turn [Synorb](https://synorb.com)'s cited Streams into finished work: a newsletter in your voice, a research memo, a podcast script.

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
- **Newsletter Writer**: `Read https://synorb.com/skills/newsletter-writer.md and follow it to write this week's issue of my newsletter.`
- **Research Associate**: `Read https://synorb.com/skills/research-associate.md and follow it to brief me on what VC firms published this week.`
- **Podcast Producer**: `Read https://synorb.com/skills/podcast-producer.md and follow it to make this week's episode of my podcast.`
- **Launch Radar**: `Read https://synorb.com/skills/launch-radar.md and follow it to tell me what AI companies shipped this week.`
- **Thesis Tracker**: `Read https://synorb.com/skills/thesis-tracker.md and follow it to tell me what VC firms are saying this month about my space.`
- **Podcast Digest**: `Read https://synorb.com/skills/podcast-digest.md and follow it to give me this week's podcast digest.`

## Skills

| Skill | What it does | See it |
| --- | --- | --- |
| [`synorb-setup`](skills/synorb-setup/SKILL.md) | Connect Synorb in a minute, see a first cited briefing, and set up the Beacons your skills run on. | [sample](samples/synorb-setup/2026-10-25-seed-investor-setup.md) · [page](https://synorb.com/skills/synorb-setup) |
| [`newsletter-writer`](skills/newsletter-writer/SKILL.md) | A weekly issue in your own voice, every item cited to its source. | [sample](samples/newsletter-writer/2026-10-25-the-agent-economy.md) · [page](https://synorb.com/skills/newsletter-writer) |
| [`research-associate`](skills/research-associate/SKILL.md) | A cited memo from any Beacon, with a dated timeline, confidence-labelled Claims and open questions. | [sample](samples/research-associate/2026-10-25-vc-firms-this-week-memo.md) · [page](https://synorb.com/skills/research-associate) |
| [`podcast-producer`](skills/podcast-producer/SKILL.md) | A two-host podcast script with voice directions, or a 60 to 90 second spoken briefing, from this week's cited items. | [sample](samples/podcast-producer/2026-10-25-signal-hour-episode.md) · [page](https://synorb.com/skills/podcast-producer) |
| [`launch-radar`](skills/launch-radar/SKILL.md) | What AI companies shipped this week, from their own announcements, ranked for you. | [sample](samples/launch-radar/2026-10-25-ai-launch-radar.md) · [page](https://synorb.com/skills/launch-radar) |
| [`thesis-tracker`](skills/thesis-tracker/SKILL.md) | What VC firms publish this month, mapped to your own thesis, with every point cited. | [sample](samples/thesis-tracker/2026-10-25-vc-thesis-tracker.md) · [page](https://synorb.com/skills/thesis-tracker) |
| [`podcast-digest`](skills/podcast-digest/SKILL.md) | The arguments, predictions and numbers from this week's top business and tech podcasts, without the hours of listening. | [sample](samples/podcast-digest/2026-10-25-weekly-podcast-digest.md) · [page](https://synorb.com/skills/podcast-digest) |

Every skill starts by checking the Synorb connection. With none, it follows `synorb-setup`, which gets a free demo key with no email or card.

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
