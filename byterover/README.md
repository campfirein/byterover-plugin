# ByteRover plugin

Use ByteRover to search authorized enterprise documents, read ingested content, and upload complete files from an
AI agent.

Distribution channel: development.

## Install with an agent

Paste this prompt into Claude Code, Codex, Cursor, or Grok Bot:

```text
Install and connect the development distribution of ByteRover from:
https://github.com/campfirein/byterover-plugin

Inspect the repository, detect the current host, use its native installation path, complete every step you can, and verify the connection.
Do not overwrite existing configuration. Stop only when browser sign-in or one host restart requires me.
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
