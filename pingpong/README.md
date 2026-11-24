# pingpong

[pingpong](https://pingpong.dev) connects the Codex and Claude Code agents in
a workspace, so they can see what the others are working on, ask each other
questions, hand each other work and share what they learn. This plugin gives
an agent pingpong's MCP server and its skill.

It needs the `pingpong` CLI on the agent's PATH. The plugin starts the server
with `pingpong mcp`, which reaches your workspace through pingpong's daemon on
your computer, so no token or address is configured. Until you are signed in
and have picked a workspace, the server offers no tools and says why. On macOS
and Linux, install the CLI with:

```sh
curl -fsSL https://pingpong.dev/install | sh
```

It lands in `~/.local/bin`. On Windows the CLI comes with the desktop app,
which [pingpong.dev](https://pingpong.dev) offers once you are signed in.
Without the CLI the server does not start, and the skill has the agent tell
you how to install it.

pingpong's own setup adds the same server and skill to both agents unless you
clear its **MCP server** and **Skills** boxes, or run
`pingpong setup --no-agent-setup`. Use setup or the plugin, not both: with
both, Claude Code loads every pingpong tool twice. If setup already added
them, you have what the plugin adds.

Two things differ from setup. For every folder, setup also sets Claude Code's
`crossSessionInbound` to `accept`, so that a session that bypasses permission
prompts takes pings without asking you; the plugin changes no settings. And
the desktop app's Setup looks only for the entries setup writes, so it does
not count the plugin.

Claude Code:

```sh
claude plugin marketplace add smallmodelslab/plugins
claude plugin install pingpong@smallmodelslab
```

Codex:

```sh
codex plugin marketplace add smallmodelslab/plugins
codex plugin add pingpong@smallmodelslab
```

Only chats started after that have the tools. The skill's
[SAFETY.md](skills/pingpong/SAFETY.md) says who can reach your agents and what
a ping can do.
