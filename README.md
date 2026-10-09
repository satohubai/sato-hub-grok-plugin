# Sato Hub for Grok

Build any crypto agent, from inside Grok Build.

This plugin connects Grok Build to **Sato Hub**, the agent builder hub for
crypto: a daily-rebuilt map of what onchain agents are built from (frameworks,
MCP servers, wallets, x402 and stablecoin payment rails, ERC-8004 identity,
agent skills), with dated evidence on every record.

Ask Grok things like:

- "What do I need to build a trading agent on Base?"
- "Check `npx -y @coinbase/agentkit-model-context-protocol` before I install it."
- "Which x402 services can my agent pay for on Base?"
- "Is this repo maintained and open source?"

Grok answers from Sato Hub's records and cites each one's page on satohub.ai,
so you can check the current state yourself.

## What's inside

| Component | Path | What it does |
|---|---|---|
| MCP server | [`.mcp.json`](.mcp.json) | Sato Hub's hosted server, `https://satohub.ai/api/mcp` (Streamable HTTP) |
| Skill | [`skills/sato-hub/`](skills/sato-hub/SKILL.md) | How to query Sato Hub and the rules to carry into answers |

No hooks, no commands, no agents, no install scripts.

## Install

From the xAI plugin marketplace in Grok Build, or connect the server alone:

```sh
grok mcp add --transport http satohub https://satohub.ai/api/mcp
```

## Network and credentials

- **Endpoints:** `https://satohub.ai/api/mcp` (MCP). The skill's optional
  `scripts/query.sh` calls the same endpoint and keyless GET pages on
  `https://satohub.ai`.
- **Credentials:** none. No API key, no account, no OAuth.
- **What is sent:** the arguments of each tool call, plus one header,
  `x-sato-source: grok-build`, so Sato Hub can tell a call came through this
  plugin. Nothing is read from your machine.
- **Funds:** nothing in this plugin signs, holds a key, deploys, relays or
  moves funds. Most tools only read; the few that change Sato Hub's own
  records (for example, submitting a project) say so in their tool
  annotations. A route answer is calldata you would read and sign yourself.

## How to read the answers

- The **Sato Score** (0–100) measures how open, active and verifiable a project
  is. It is not a safety, quality or returns grade.
- **Sato Check** and **Preflight** describe what was read and run, with dates.
  They are not audits or safety ratings. `unknown` means Sato Hub holds no
  record, not that anything is wrong.
- `verification_status` separates self-reported from verified.

Docs: https://satohub.ai/mcp

## License

MIT. Catalog data returned by the server is CC-BY-4.0, attribution
"data by satohub.ai".
