# ByteRover plugin marketplace

The ByteRover plugin gives your coding agent grounded company context from your ByteRover Company
Brain: accepted facts about the company, product, team and decisions, read at the moment your agent
needs them.

## Install

Claude Code:

```bash
claude plugin marketplace add campfirein/byterover-plugin
```

Then install the plugin:

```
/plugin install byterover@byterover
```

Cowork: open Customize, then Plugins, then Add marketplace, and enter
`campfirein/byterover-plugin`. Click Save plugin on the card to finish.

Other agents read the same directory through the [Agent Plugins](https://agent-plugins.org)
format. Point your client's plugin setup at the `byterover/` directory of this repository, and
follow that client's own install instructions.

Restart the session, or run `/reload-plugins`, before the skill loads.

## What you get

Two things, and they work together:

- **The `byterover-company-brain` skill.** It tells your agent when to reach for the Brain and how
  to report what came back - to answer from returned objects only, and to say that context is
  missing rather than guess.
- **The `byterover-brain` MCP server.** `brain__query` reads accepted context. `brain__learn`
  proposes a new statement, which stays pending until someone reviews it in ByteRover.

So you can ask your agent "what did we decide about billing retries?" or "who owns the ingest
pipeline?" and get an answer sourced from the Brain instead of from the repository or a guess. Ask
it to remember something and it files a proposal - it never writes accepted knowledge on its own.

## Requirements

A ByteRover account. The plugin connects to `https://dev-mcp.byterover.dev/mcp` and opens a browser
for sign-in and consent on first use. There is nothing to install or launch locally, and no
particular operating system is required.

The remote MCP surface is read-only while its final tool contract is being defined.

## What is here

- `.claude-plugin/marketplace.json`: the marketplace catalog. Authored by hand.
- `byterover/`: the plugin itself. **Generated.** It is built from `apps/plugin` in the ByteRover
  repository and published here by a release job. Do not edit it: the next release overwrites the
  whole directory.

## Updates

Run `/plugin marketplace update` to pick up a new version. A host only offers an update when the
version in the manifest changes, so every release carries one - including a release that only
changes the Company Brain skill your agent follows.
