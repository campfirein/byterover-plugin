# Grove plugin marketplace

The Grove plugin gives your coding agent grounded company context from your Grove Company Brain.

## Install

Claude Code:

```bash
claude plugin marketplace add campfirein/grove-plugin
```

Then install the plugin:

```
/plugin install grove@byterover
```

Other agents read the same directory through the [Agent Plugins](https://agent-plugins.org)
format. Point your client's plugin setup at the `grove/` directory of this repository, and follow
that client's own install instructions.

## What is here

- `.claude-plugin/marketplace.json`: the marketplace catalog. Authored by hand.
- `grove/`: the plugin itself. **Generated.** It is built from `apps/plugin` in the Grove
  repository and published here by a release job. Do not edit it: the next release overwrites the
  whole directory.

## Updates

Run `/plugin marketplace update` to pick up a new version. The plugin version tracks the Company
Brain skill it carries, so a new version means the guidance your agent follows has changed.
