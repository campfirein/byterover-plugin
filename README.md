# ByteRover plugin marketplace

The ByteRover plugin gives your coding agent grounded company context from your Grove Company Brain.

## Install

Claude Code:

```bash
claude plugin marketplace add campfirein/byterover-plugin
```

Then install the plugin:

```
/plugin install grove@byterover
```

The id changes at 0.7.0: `grove@byterover` becomes `byterover@byterover`. A host keys an install by
that string and reads a new one as a different plugin, so 0.7.0 does not arrive as an update. If you
installed before it, remove `grove@byterover` and install `byterover@byterover` once.

Other agents read the same directory through the [Agent Plugins](https://agent-plugins.org)
format. Point your client's plugin setup at the `grove/` directory of this repository, and follow
that client's own install instructions.

## What is here

- `.claude-plugin/marketplace.json`: the marketplace catalog. Authored by hand.
- `grove/`: the plugin, up to 0.6.0. **Generated**, and on its way out - 0.7.0 publishes
  `byterover/` instead, and this directory is deleted with the catalog row that points at it.
- `byterover/`: the plugin from 0.7.0 on. **Generated.** It is built from `apps/plugin` in the Grove
  repository and published here by a release job. Do not edit it: the next release overwrites the
  whole directory.

## Updates

Run `/plugin marketplace update` to pick up a new version. A host only offers an update when the
version in the manifest changes, so every release carries one - including a release that only
changes the Company Brain skill your agent follows.
