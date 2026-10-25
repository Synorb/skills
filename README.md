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
- **Research Associate**: `Read https://synorb.com/skills/research-associate.md and follow it to write me a research memo on [a company, a person or a topic].`
- **Podcast Producer**: `Read https://synorb.com/skills/podcast-producer.md and follow it to make this week's episode of my podcast.`

## Skills

| Skill | What it does | See it |
| --- | --- | --- |
| [`synorb-setup`](skills/synorb-setup/SKILL.md) | Connect Synorb in a minute, see a first cited briefing, and save the watches you care about. | [sample](samples/synorb-setup/2026-10-25-seed-investor-setup.md) · [page](https://synorb.com/skills/synorb-setup) |
| [`newsletter-writer`](skills/newsletter-writer/SKILL.md) | A weekly issue in your own voice, every item cited to its publisher. | [sample](samples/newsletter-writer/2026-10-25-the-agent-economy.md) · [page](https://synorb.com/skills/newsletter-writer) |
| [`research-associate`](skills/research-associate/SKILL.md) | A cited memo on an organization, person or topic, with a timeline and confidence-labelled Claims. | [sample](samples/research-associate/2026-10-25-andreessen-horowitz-memo.md) · [page](https://synorb.com/skills/research-associate) |
| [`podcast-producer`](skills/podcast-producer/SKILL.md) | A two-host podcast script with voice directions, or a 60 to 90 second spoken briefing, from this week's cited items. | [sample](samples/podcast-producer/2026-10-25-signal-hour-episode.md) · [page](https://synorb.com/skills/podcast-producer) |

Every skill starts by checking the Synorb connection. With none, it follows `synorb-setup`, which gets a free demo key with no email or card.

## By agent type

| Agent type | How to install |
| --- | --- |
| Personal Agents | Copy the phrase and paste it into your agent. The agent reads the hosted skill page and follows it. |
| Chat Assistants | Download the skill as a ZIP and upload it where your assistant takes skills. Or paste the phrase into a chat. |
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

- `.claude-plugin/marketplace.json`: a Claude Code plugin marketplace. `claude plugin marketplace add Synorb/skills`, then `claude plugin install synorb@synorb-skills`.
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
