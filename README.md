# smallmodelslab plugins

Plugins for coding agents. [Crossroad](https://smallmodelslab.ai) asks the
same typed questions about many files or lines at once.
[Neokki](https://neokki.app) gives the agent a JavaScript REPL over your
flashcard decks. [pingpong](https://pingpong.dev) connects the agent to the
other Codex and Claude Code agents in your workspace, through the pingpong
CLI on your computer. [ProcessControl](https://processcontrol.dev) teaches the
agent to set a repository up for its pull request tests and to write
descriptions as claims it can test.

The pingpong plugin is for a pingpong CLI set up without its own agent
integrations: read [its README](pingpong/README.md) before installing it.

Claude Code:

```sh
claude plugin marketplace add smallmodelslab/plugins
claude plugin install crossroad@smallmodelslab
claude plugin install neokki@smallmodelslab
claude plugin install pingpong@smallmodelslab
claude plugin install processcontrol@smallmodelslab
```

Codex:

```sh
codex plugin marketplace add smallmodelslab/plugins
codex plugin add crossroad@smallmodelslab
codex plugin add neokki@smallmodelslab
codex plugin add pingpong@smallmodelslab
codex plugin add processcontrol@smallmodelslab
```
