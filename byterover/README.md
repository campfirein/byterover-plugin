# ByteRover plugin

Use ByteRover to search authorized enterprise documents, read ingested content, and upload complete files from an
AI agent.

Distribution channel: development.

## Install with an agent

Paste this prompt into Claude Code, Claude Desktop, Codex, or Cursor:

```text
Install and connect the development distribution of ByteRover from:
https://github.com/campfirein/byterover-plugin

Inspect the repository, detect the current host, use its native installation path, complete every step you can, and verify the connection.
Start ByteRover MCP OAuth automatically only if the current host and its permission policy allow that action. Do not bypass, change, or work around the permission policy.
When browser OAuth opens, I will complete sign-in and consent myself; do not complete them for me. Wait for me to finish, then resume and verify the ByteRover MCP connection.
After installation and OAuth, restart the host or open a new conversation if the current conversation does not reload newly connected tools. In the new conversation, explicitly ask the host to use ByteRover and verify a real ByteRover tool call.
If the host blocks, denies, or does not support automatic MCP OAuth, report the exact blocked action and provide the exact host-specific manual step to start it. If you cannot determine that step for this host, say so instead of guessing.
Do not overwrite existing configuration.
```

The repository README is the public installation entry point. Agents must follow the
[packaged installation contract](INSTALL_AGENT.md) for every host. Native permission prompts and OAuth consent remain
under user control. The package never asks an agent to download or run a repository-provided executable.

## Native installation

Claude Code users may also run:

```text
claude plugin marketplace add campfirein/byterover-plugin --scope user
claude plugin install byterover@byterover --scope user
```

Codex users may also run:

```sh
codex plugin marketplace add campfirein/byterover-plugin
codex plugin add byterover@byterover
```

## ChatGPT and Dot

Open ChatGPT Plugins, choose Add > Add custom MCP server, and enter `https://dev-mcp.byterover.ai/mcp`. Complete OAuth, create
ByteRover as a plugin backed by that remote MCP server, then enable ByteRover for the Dot. Do not upload the desktop
plugin ZIP. Start a new Dot conversation after enabling the plugin, then explicitly ask it to use ByteRover.

## Grok Bot

Open Grok Connectors, add a Custom connector with `https://dev-mcp.byterover.ai/mcp`, and complete OAuth. Grok receives the remote
MCP tools but does not install the ByteRover skill package. Open a new conversation after connection and explicitly
ask that conversation to use ByteRover. Do not repeat OAuth unless the connector settings report an authentication
error.
