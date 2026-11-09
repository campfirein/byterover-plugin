# ByteRover plugin

Development distribution of the ByteRover search, read, and whole-file upload plugin for AI
agents.

## Development endpoints

- MCP server: `https://dev-mcp.byterover.ai/mcp`
- OAuth server: `https://dev.byterover.ai`

The development server requires OAuth. The host opens the sign-in and consent flow when the plugin first calls
ByteRover.

## Install with an agent

Paste this prompt into Claude Code, Claude Desktop, Codex, Cursor, or Grok Bot:

```text
Install and connect the development distribution of ByteRover from:
https://github.com/campfirein/byterover-plugin

Inspect the repository, detect the current host, use its native installation path, complete every step you can, and verify the connection.
Start ByteRover MCP OAuth automatically only if the current host and its permission policy allow that action. Do not bypass, change, or work around the permission policy.
When browser OAuth opens, I will complete sign-in and consent myself; do not complete them for me. Wait for me to finish, then resume and verify the ByteRover MCP connection.
If the host blocks, denies, or does not support automatic MCP OAuth, report the exact blocked action and provide the exact host-specific manual step to start it. If you cannot determine that step for this host, say so instead of guessing.
Do not overwrite existing configuration.
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

## Install in Claude Desktop

Paste the installation prompt above into Claude Desktop. Let its native plugin manager add ByteRover, approve the
plugin when the app asks, and complete OAuth. The prompt does not bypass native approval or consent.

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
