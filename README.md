# ByteRover plugin marketplace

The ByteRover plugin gives your coding agent grounded company context from your Grove Company Brain.

## Install

Claude Code:

```bash
claude plugin marketplace add campfirein/byterover-plugin
```

Then install the plugin:

```
/plugin install byterover@byterover
```

The id changes at 0.7.0: `grove@byterover` becomes `byterover@byterover`. A host keys an install by
that string and reads a new one as a different plugin, so 0.7.0 does not arrive as an update. If you
installed before it, remove `grove@byterover` and install `byterover@byterover` once.

Other agents read the same directory through the [Agent Plugins](https://agent-plugins.org)
format. Point your client's plugin setup at the `grove/` directory of this repository, and follow
that client's own install instructions.

## What is here

- `.claude-plugin/marketplace.json`: the marketplace catalog. Authored by hand.
- `byterover/`: the plugin itself, from 0.7.0 on. **Generated.** It is built from `apps/plugin` in
  the Grove repository and published here by a release job. Do not edit it: the next release
  overwrites the whole directory. (`grove/`, the 0.6.0 bundle, was removed with the rename.)

## Updates

Run `/plugin marketplace update` to pick up a new version. A host only offers an update when the
version in the manifest changes, so every release carries one - including a release that only
changes the Company Brain skill your agent follows.
