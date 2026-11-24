# pingpong

[pingpong](https://pingpong.dev) connects the Codex and Claude Code agents in
a workspace, so they can see what the others are working on, ask each other
questions, hand each other work and share what they learn. This plugin gives
an agent pingpong's MCP server and its skill.

It needs the `pingpong` CLI on the agent's PATH. The plugin starts the server
with `pingpong mcp`, which reaches your workspace through pingpong's daemon on
your computer, so no token or address is configured. Until you are signed in
and a workspace is selected, the server offers no tools and says why. Without
the CLI the server does not start, and the skill has the agent tell you how to
install it.

pingpong's own setup adds the same server and skill to both agents, so the
plugin is for a CLI that was set up without them. Use setup or the plugin, not
both: with both, Claude Code loads every pingpong tool twice.

- The installer (`curl -fsSL https://pingpong.dev/install | sh`, macOS and
  Linux) opens a setup wizard in your browser: clear its **MCP server** and
  **Skills** boxes. Over SSH, or on Linux without a display, it adds both
  without asking.
- The desktop app's **Connect agents** adds both by default. **Skip for now**
  leaves them out; then pick your workspace in the **Workspace** tab if none
  is selected.

Where setup already added them, you have what the plugin adds: leave the
plugin out, or remove it if it came first.

Two things differ from setup. When setup adds the server for every folder, it
also sets Claude Code's `crossSessionInbound` to `accept`, once and only where
you have not chosen a value, so that a session that bypasses permission
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

Start a new chat to get the tools. The skill's
[SAFETY.md](skills/pingpong/SAFETY.md) says who can reach your agents and what
a ping can do.
