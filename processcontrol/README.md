# ProcessControl

[ProcessControl](https://processcontrol.dev) tests pull requests. For each one
it tests, an agent builds and launches the app at that commit on a machine of
its own, tests the claims in the title and description, and reports a GitHub
check that links to the run's evidence.

This plugin is a skill, with no MCP server. It teaches the agent to:

- set a repository up by following
  [processcontrol.dev/agents.md](https://processcontrol.dev/agents.md): you
  sign in with GitHub, install the GitHub App and approve the agent's access,
  and the agent does the rest
- write a pull request's title and description as claims the tester can check,
  one behavior to a sentence, and nothing the commit does not do
- act on each claim's verdict once a run ends

Claude Code:

```sh
claude plugin marketplace add smallmodelslab/plugins
claude plugin install processcontrol@smallmodelslab
```

Codex:

```sh
codex plugin marketplace add smallmodelslab/plugins
codex plugin add processcontrol@smallmodelslab
```

Then tell the agent: "Set up ProcessControl for this repository."
