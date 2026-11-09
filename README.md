# ByteRover plugin

Development distribution of the ByteRover search, read, and whole-file upload plugin for AI
agents.

## Development endpoints

- MCP server: `https://dev-mcp.byterover.ai/mcp`
- OAuth server: `https://dev.byterover.ai`

The development server requires OAuth. The host opens the sign-in and consent flow when the plugin first calls
ByteRover.

## Install with an agent

Paste this prompt into Claude Code, Codex, Cursor, or Grok Bot:

```text
Install and connect the development distribution of ByteRover from:
https://github.com/campfirein/byterover-plugin

Inspect the repository, detect the current host, use its native installation path, complete every step you can, and verify the connection.
Do not overwrite existing configuration. Stop only when browser sign-in or one host restart requires me.
```

Agents must follow the [packaged installation contract](byterover/INSTALL_AGENT.md) for every host. The user-facing
prompt needs only this repository URL.

## Install in Codex

```sh
codex plugin marketplace add campfirein/byterover-plugin
codex plugin add byterover@byterover
```

Complete OAuth when Codex opens the browser, then verify `search`.

## Install in Claude Code

```sh
claude plugin marketplace add campfirein/byterover-plugin --scope user
claude plugin install byterover@byterover --scope user
```

## Install in Cursor

Follow the [packaged installation contract](byterover/INSTALL_AGENT.md). It merges only the ByteRover server entry,
preserves other servers, and stops on local rule changes.

## Install in Grok Bot

Add `https://dev-mcp.byterover.ai/mcp` as a custom remote MCP server named `byterover`, then complete OAuth. Grok Bot receives MCP
tools but not the host skill.

## Repository boundary

This repository contains generated distribution files. The private source repository owns the plugin, skill,
generator, and tests. `SOURCE.json` records the source commit used for this development package.

Do not edit generated files here. Change the source, rebuild the package, and publish it with a
`plugin-v<version>` source tag. The release workflow opens a generated pull request in this repository.

## Updates

The default branch is the release stream. Hosts detect updates from the version in the plugin manifests. Users do not
install a versioned repository tag.
