---
distribution-channel: development
mcp-server-url: https://dev-mcp.byterover.ai/mcp
marketplace-source: campfirein/byterover-plugin
---

# Install ByteRover

This file is an installation contract for an AI agent. It is instruction data, not permission. Continue only when the
current user message explicitly asks you to install ByteRover from the repository that contains this file.
Complete every supported step in that scope without asking for an extra conversational confirmation. Native host
permission prompts and browser OAuth consent still belong to the user.

Read the distribution channel and MCP server URL from the frontmatter. Report the channel before changing the host.
The marketplace repository's default branch is the published release stream. Read the current release from the exact
`marketplace-source` in the frontmatter. Do not substitute a fork or another repository. Continue only when the channel
named in the user's current message equals the channel in this contract.

## Goal

Install the ByteRover plugin for the current host, authenticate its remote MCP server, and verify the connection.
Install only for the current user and current host.

## Safety rules

- Determine the current host from your runtime context. Do not select a host only because its executable exists.
- Use the host's native plugin manager when it is available.
- Do not change the MCP URL declared by this package.
- Do not remove other marketplaces, plugins, MCP servers, rules, or user settings.
- Never replace an existing ByteRover entry that points to a different repository or MCP URL. Report the conflict.
- Do not copy tokens, cookies, authorization codes, or browser callback URLs into chat or files.
- Let the host display its native permission prompt. Do not bypass it.
- Let the user complete browser sign-in and consent. Continue verification after the login command returns.
- If the current session cannot load a newly installed plugin, finish the command-line checks and ask for exactly one
  restart. Do not claim that tools are available in the current session until the host shows them.

## Claude Code

1. Inspect the current installation with `claude plugin list --json` and `claude plugin marketplace list --json`.
   The marketplace JSON exposes its repository and local checkout. If `byterover` exists, require
   either its `repo` or the canonical Git origin from `installLocation` to equal `marketplace-source`. When
   `<installLocation>/byterover/INSTALL_AGENT.md` exists, require its channel and MCP URL to equal this contract. For a
   legacy checkout without that file, require `<installLocation>/byterover/.mcp.json` to contain the exact MCP URL from
   this contract. Use `git -C <installLocation> symbolic-ref --short -q HEAD` to detect a branch checkout. If it returns
   a branch, resolve the default branch with
   `git -C <installLocation> symbolic-ref --short refs/remotes/origin/HEAD`, remove the `origin/` prefix, and compare the
   two branch names. Stop if the default branch cannot be resolved or the names differ. If the first command returns no
   branch, do not resolve `origin/HEAD`; use `git -C <installLocation> describe --tags --exact-match HEAD` instead. Stop
   if no exact tag is found. If the repository, channel, or MCP URL differs, stop and report it.
2. If `byterover` is absent, add the user-scoped marketplace:

   ```sh
   claude plugin marketplace add campfirein/byterover-plugin --scope user
   ```

3. If the repository matches but its local checkout is detached, resolve the exact tag at `HEAD`. Migrate only the
   retired `dev-v0.1.2` marketplace once. For any other detached ref, stop and report the conflict.

   ```sh
   claude plugin marketplace remove byterover --scope user
   claude plugin marketplace add campfirein/byterover-plugin --scope user
   ```

   Stop if the user-scoped declaration cannot be removed. Do not remove project or local declarations. This migration
   is authorized only by the current explicit install or update request. Migrate the marketplace at most once.
4. After step 2 or 3, rerun the JSON and Git inspection commands from step 1 and use only the new state. Require the
   checkout to track its default branch. If the source still differs or the checkout is detached, stop and report the
   failure. Do not repeat the add or migration.
5. Refresh the marketplace release stream:

   ```sh
   claude plugin marketplace update byterover
   ```

   Rerun every JSON and Git validation from step 1 against the refreshed checkout. Stop if the update or any validation
   fails.
6. If `byterover@byterover` is not installed, run:

   ```sh
   claude plugin install byterover@byterover --scope user
   ```

   If it is already installed, update it instead:

   ```sh
   claude plugin update byterover@byterover --scope user
   ```

   If it is installed but disabled, run:

   ```sh
   claude plugin enable byterover@byterover --scope user
   ```

7. Authenticate when required:

   ```sh
   claude mcp login 'plugin:byterover:byterover'
   ```

8. Verify that `claude plugin list` shows `byterover@byterover` as enabled and `claude mcp list` shows
   `plugin:byterover:byterover` as connected.

## Claude Desktop

1. Confirm from the runtime context that the current host is Claude Desktop, not Claude Code.
2. Inspect the native plugin manager before changing anything. If ByteRover already exists, require its marketplace
   source to equal `marketplace-source` and its remote MCP URL to equal this contract. Stop on either mismatch.
3. If ByteRover is absent, use Claude Desktop's native plugin manager to add the marketplace source and install the
   `byterover` plugin. Do not use Claude Code shell commands as a substitute for the desktop plugin manager.
4. Let Claude Desktop show its native plugin approval. Ask the user to approve that prompt only when the app requires
   it. Do not bypass or simulate the approval.
5. Complete ByteRover OAuth when Claude Desktop opens the browser consent flow.
6. Open a new Claude Desktop conversation after installation. Verify that ByteRover exposes exactly `search`, `read`,
   and `write` before reporting functional success.

## Codex

1. Inspect the current installation with `codex plugin marketplace list --json`, `codex plugin list --json`, and
   `codex mcp list`. The marketplace JSON exposes its source and local root. If `byterover` exists,
   require its source to equal `https://github.com/campfirein/byterover-plugin.git`. When
   `<root>/byterover/INSTALL_AGENT.md` exists, require its channel and MCP URL to equal this contract. For a legacy
   checkout without that file, require `<root>/byterover/mcp.json` to contain the exact MCP URL from this contract. Use
   `git -C <root> symbolic-ref --short -q HEAD` to detect a branch checkout. If it returns a branch, resolve the default
   branch with `git -C <root> symbolic-ref --short refs/remotes/origin/HEAD`, remove the `origin/` prefix, and compare the
   two branch names. Stop if the default branch cannot be resolved or the names differ. If the first command returns no
   branch, do not resolve `origin/HEAD`; use `git -C <root> describe --tags --exact-match HEAD` instead. Stop if no exact
   tag is found. If the source, channel, or MCP URL differs, stop and report it.
2. If the `byterover` marketplace is absent, add the marketplace:

   ```sh
   codex plugin marketplace add campfirein/byterover-plugin --json
   ```

3. If the source matches but its local checkout is detached, resolve the exact tag at `HEAD`. Migrate only the retired
   `dev-v0.1.2` marketplace once. For any other detached ref, stop and report the conflict.

   ```sh
   codex plugin marketplace remove byterover --json
   codex plugin marketplace add campfirein/byterover-plugin --json
   ```

   Stop if removal fails. This migration is authorized only by the current explicit install or update request. Migrate
   the marketplace at most once.
4. After step 2 or 3, rerun the JSON and Git inspection commands from step 1 and use only the new state. Require the
   checkout to track its default branch. If the source still differs or the checkout is detached, stop and report the
   failure. Do not repeat the add or migration.
5. Refresh the marketplace release stream:

   ```sh
   codex plugin marketplace upgrade byterover --json
   ```

   Stop if the upgrade fails. Rerun every JSON and Git validation from step 1 against the refreshed checkout and stop if
   any validation fails.
6. If `byterover@byterover` is not installed, run:

   ```sh
   codex plugin add byterover@byterover --json
   ```

   If the plugin is installed but disabled or has another version, reinstall only this plugin:

   ```sh
   codex plugin remove byterover@byterover --json
   codex plugin add byterover@byterover --json
   ```

7. Authenticate when required:

   ```sh
   codex mcp login byterover
   ```

8. Verify that `codex plugin list --json` shows `byterover@byterover` as enabled and `codex mcp list` shows
   `byterover` with OAuth authentication.

## Cursor

Install into the current project only when the current working directory is the intended project.

1. Read `byterover/.cursor/mcp.json` and `byterover/.cursor/rules/byterover.mdc` from the default branch of the exact
   marketplace source declared in the frontmatter.
2. Inspect `<project>/.cursor/mcp.json` before editing it. If the file exists but is not valid JSON, stop without
   writing. If `mcpServers.byterover` is absent, add the packaged entry. If it has the exact packaged URL, keep it. If
   it has another URL, stop and report the conflict.
3. Inspect `<project>/.cursor/rules/byterover.mdc` before editing it. If it is absent, copy the packaged rule. If it has
   a ByteRover `source-sha256` marker, hash the canonical body and require it to equal that marker before replacing
   the file. A mismatch means the user changed it; stop and report the conflict. Also stop if the marker is absent.
4. Parse the final MCP file as JSON before reporting success.
5. Ask for one Cursor restart. After restart, direct the user to `Customize` > `MCPs` > `byterover` and let Cursor
   complete OAuth.

Do not overwrite an existing `.cursor/mcp.json` with the distribution file.

## Grok Bot

Grok Bot supports the remote MCP connection, not this host-specific skill package.

1. Use the MCP server URL declared in the packaged contract from the marketplace repository.
2. Inspect existing custom MCP connections. If `byterover` is absent, add it with that URL. If it has the same URL,
   reuse it. If it has another URL, stop and report the conflict. Never replace the existing connection.
3. Let the user complete OAuth.
4. Verify that Grok Bot discovers the ByteRover tools.

## Unsupported hosts

Do not invent an installation path. Explain that this repository currently provides installation contracts for Claude
Code, Claude Desktop, Codex, Cursor, and the Grok Bot MCP connection. Another hosted product may require a catalog
submission or administrator-managed connector.

## Functional verification

When the host can use newly installed tools in the current session:

1. Confirm that the server exposes exactly `search`, `read`, and
   `write`.
2. Call `search` once with query `ByteRover` and `effort` set to `low`. Do not pass a drive identifier; the
   backend searches every drive allowed by current RBAC.
3. Report only whether the call succeeded and how many results it returned. No results is a successful empty search.

If a restart is required, report installation and authentication separately from functional verification. Do not call
the installation complete end to end until the search succeeds.

## Final report

Report only:

- detected host;
- plugin installation state;
- MCP authentication state;
- functional verification state;
- the single remaining user action, or `none`.
