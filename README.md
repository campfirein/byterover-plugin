# ByteRover plugin marketplace

The ByteRover plugin gives your coding agent grounded company context from your Grove Company Brain.

## Install

Claude Code:

```bash
claude plugin marketplace add campfirein/grove-plugin
```

Then install the plugin:

```
/plugin install grove@byterover
```

`grove` is the plugin's id, and it does not change with the name on the card: a host keys an
install by that string, so renaming it would read as a different plugin and leave the one you have
installed sitting there.

Other agents read the same directory through the [Agent Plugins](https://agent-plugins.org)
format. Point your client's plugin setup at the `grove/` directory of this repository, and follow
that client's own install instructions.

## What is here

- `.claude-plugin/marketplace.json`: the marketplace catalog. Authored by hand.
- `grove/`: the plugin itself. **Generated.** It is built from `apps/plugin` in the Grove
  repository and published here by a release job. Do not edit it: the next release overwrites the
  whole directory.

## Updates

Run `/plugin marketplace update` to pick up a new version. A host only offers an update when the
version in the manifest changes, so every release carries one - including a release that only
changes the Company Brain skill your agent follows.
