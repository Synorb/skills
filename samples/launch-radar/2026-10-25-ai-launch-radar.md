# Sample: launch-radar

- Skill: `launch-radar` v1.0.0
- Date: 2026-10-25
- Tested live against production Synorb over MCP
- Beacon: AI Companies starter Beacon (`synorb_bcn_iiadZvETkMnI32Vevse9Og`), `lookback_hours=168`, effective window 2026-10-19 to 2026-10-25

## User request

"What did AI companies ship this week? I'm a founder building developer tools for AI agents, so tell me what matters for me."

## Launch radar

**AI launch radar, 2026-10-19 to 2026-10-25.** Scope: the AI Companies Beacon, which carries each company's own announcements, so everything below is "the company says". This is a sample: I read 20 of 860 matching Manifests (two pages of 10). Your angle, as I read it: a founder building developer tools for AI agents.

### Top three for you

1. **Daytona raised $60M for an "agent cloud" (2026-10-20).** The company says it raised a $60M Series B at a $1B valuation, led by FirstMark Growth, for total funding of $91M. It says revenue has grown about 25x since January, with average month-over-month net revenue retention of about 135%. It says it is the only provider with Linux, Windows, macOS and GPU sandboxes on one platform, and that Writer provisioned 300,000 sandboxes in one month on it. All of these are stated by Daytona about itself. Why it matters to you (my view): sandboxed execution for agents is attracting money, and a vendor now claims one platform across four operating-system types. [Source](https://www.daytona.io/dotfiles/daytona-raises-60m-series-b-to-build-the-agent-cloud)
2. **Mistral released Voxtral 3, a voice agent SDK plus speech models (2026-10-20).** Mistral says the SDK is built on LiveKit and the models support 50+ languages. It says they are available through its EU-hosted API or for self-deployment. Listed prices (measured label): Voxtral Mini Transcribe 3 (batch) $0.0035 per minute, and Voxtral Mini TTS 3 $13 per 1 million characters. Mistral says Voxtral Small Transcribe 3 beats Whisper, Scribe v2 and Gemini 3.5 Transcribe on multilingual transcription; that comparison is Mistral's own claim, not an independent test. Why it matters to you (my view): if your tools serve voice agents, there is a new SDK and a price point to compare. [Source](https://mistral.ai/news/voxtral-3)
3. **SentinelOne launched Singularity Agentic Detection and Response, in early access (2026-10-21).** The company says it gives an inventory of agents and MCP servers across endpoints, SaaS and cloud, and covers Microsoft Copilot Studio, OpenAI ChatGPT workspace agents, Anthropic Claude managed agents and Salesforce Agentforce. It says it blocks prompt injection and tool poisoning before an action runs, and can stop one agent mid-action. Why it matters to you (my view): a large security vendor now treats agents and MCP servers as something to inventory and police, which is a likely buyer question for any agent tooling. [Source](https://investors.sentinelone.com/press-releases/news-details/2026/SentinelOne-Launches-Singularity-Agentic-Detection-and-Response-to-Stop-Rogue-and-Malicious-AI-Agents-at-Machine-Speed/default.aspx)

### Also shipped

- **Fireworks AI, 2026-10-20: Muse Spark Open, Meta's open-weights model, on US serverless.** Fireworks says it is an 816B-parameter mixture-of-experts model with 42B active parameters and a 1M-token context window, with zero data retention by default. Fireworks reports (measured label) 84.3% on SWE-bench Verified and 82.9% on Terminal-Bench 2.1, and 53.3% on Rogo's Big Finance Bench, which it says is ahead of Claude Opus 5.5. These are the vendor's reports. [Link](https://fireworks.ai/blog/meta-muse-spark-open)
- **Anthropic, page dated 2026-10-22: "Product Updates and Feature Releases (2025-2026)".** This is a cumulative page, so the individual launches are not dated in the Claims. Anthropic says it is donating Agent Skills to the Agentic AI Foundation, and that more than 70 agent platforms, including ChatGPT, Cursor, GitHub Copilot and VS Code, have integrated Agent Skills since December 2025. It also lists a compute partnership with SpaceX, and Claude for Healthcare, Claude for Small Business, Claude Science and an Economic Index connector. [Link](https://www.anthropic.com/news/product)
- **Hightouch, 2026-10-22:** announced enterprise-grade message delivery in its agentic marketing platform (email, SMS, push, in-app, WhatsApp). It says Medium moved its sending in under a month. [Link](https://hightouch.com/blog/lifecycle-studio-customer-engagement)
- **Legora, 2026-10-23:** raised a $550M Series E at an $8.8B post-money valuation, led by Atreides Management. It says it is building an agentic operating system, aOS, and uses consumption-based pricing. [Link](https://legora.com/blog/scaling-fast-built-to-last)
- **Higgsfield, 2026-10-23:** extended its Series B with TCV and NVIDIA. It reports crossing $1 billion annualized revenue run rate in September (measured label), and says it is expanding to NVIDIA Vera Rubin. [Link](https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia)
- **Wayve, 2026-10-23:** collaboration with Stellantis and NVIDIA on autonomous vehicle deployment in France. It also says it signed a production agreement with Mercedes-Benz. [Link](https://wayve.ai/press/wayve-stellantis-nvidia-collaborate-on-deployment-across-france)
- **Applied Intuition, 2026-10-22:** says the U.S. Navy awarded it a production contract, starting with five Arleigh Burke-class destroyers. [Link](https://www.appliedintuition.com/press-releases/navy-selects-applied-intuition-field-ai-perception)
- **Tempus AI, 2026-10-23:** multi-year data-licensing and platform agreement with Bristol Myers Squibb, with licensing through 2031. [Link](https://investors.tempus.com/news-releases/news-release-details/tempus-expands-strategic-collaboration-bristol-myers-squibb-0)

Left out as not launches: an OpenAI Engineering storage write-up (2026-10-21), PHP security posts from Sourcegraph, Dynatrace and Securonix, a SAS survey report, IBM earnings items, and a Writer essay.

### What to watch (my view, not the sources')

Agent infrastructure is where the money and launches cluster this week: sandboxes (Daytona), voice SDKs (Mistral) and agent security (SentinelOne). Agent Skills adoption claimed by Anthropic is also relevant if you ship tooling that agents load. All figures are the companies' own and are not independently verified.

### Source index

| Item | Publisher | Published | Link |
| --- | --- | --- | --- |
| Daytona Raises $60M Series B to Build the Agent Cloud | Daytona | 2026-10-20 | https://www.daytona.io/dotfiles/daytona-raises-60m-series-b-to-build-the-agent-cloud |
| Voxtral 3: Voice Agent SDK & Speech Models in 50+ Languages | Mistral AI | 2026-10-20 | https://mistral.ai/news/voxtral-3 |
| SentinelOne Launches Singularity Agentic Detection and Response | SentinelOne | 2026-10-21 | https://investors.sentinelone.com/press-releases/news-details/2026/SentinelOne-Launches-Singularity-Agentic-Detection-and-Response-to-Stop-Rogue-and-Malicious-AI-Agents-at-Machine-Speed/default.aspx |
| Muse Spark Open on Fireworks | Fireworks AI | 2026-10-20 | https://fireworks.ai/blog/meta-muse-spark-open |
| Product Updates and Feature Releases (2025-2026) | Anthropic | 2026-10-22 | https://www.anthropic.com/news/product |
| Hightouch Launches Enterprise-Message Delivery Capabilities | Hightouch | 2026-10-22 | https://hightouch.com/blog/lifecycle-studio-customer-engagement |
| Scaling fast, built to last | Legora | 2026-10-23 | https://legora.com/blog/scaling-fast-built-to-last |
| Higgsfield Extends Series B With New Investment From TCV and NVIDIA | Higgsfield | 2026-10-23 | https://higgsfield.ai/blog/higgsfield-series-b-extension-tcv-nvidia |
| Wayve, Stellantis, and NVIDIA Collaborate ... Across France | Wayve | 2026-10-23 | https://wayve.ai/press/wayve-stellantis-nvidia-collaborate-on-deployment-across-france |
| U.S. Navy Selects Applied Intuition to Field AI Perception | Applied Intuition | 2026-10-22 | https://www.appliedintuition.com/press-releases/navy-selects-applied-intuition-field-ai-perception |
| Tempus Expands Strategic Collaboration with Bristol Myers Squibb | Tempus AI | 2026-10-23 | https://investors.tempus.com/news-releases/news-release-details/tempus-expands-strategic-collaboration-bristol-myers-squibb-0 |

## Message after the radar

Want a weekly radar like this? I can't schedule anything in this runtime, so you would need to ask me again each week, or set a weekly job in a runtime that can. No Beacon was saved. The response carried no account notice.

## Calls made

| Tool | Key args | total_count | Manifests returned |
| --- | --- | --- | --- |
| `synorb-profile` | none | n/a | 0 (plan internal, 33 Beacons used, no limit) |
| `synorb-beacons` | `tag="starter"` | 3 Beacons | 0 |
| `synorb-manifests` | `beacon_id=synorb_bcn_iiadZvETkMnI32Vevse9Og`, `lookback_hours=168`, `mode="count"` | 860 | 0 |
| `synorb-manifests` | same Beacon, `lookback_hours=168`, `page_size=10`, page 0 | 860 | 10 |
| `synorb-manifests` | same, page 1 | 860 | 10 |
