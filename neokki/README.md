# Neokki

[Neokki](https://neokki.app) keeps flashcards as text: a deck is a `.neodeck`
file, and its cards are HTML that can run JavaScript. This plugin connects the
agent to your Neokki account through Neokki's MCP at `https://neokki.app/mcp`,
which signs you in on neokki.app the first time it is used.

The MCP is a JavaScript REPL over your decks. Each Neokki operation is an async
function: `list_decks`, `read_deck`, `check_deck`, `create_deck`, `save_deck`,
`delete_deck`, `study`, `answer`, `list_schedulers` and `pick_scheduler`. An
agent can write a deck from your notes, check it, rework many cards at once, or
study with you card by card while Neokki schedules each card.

Claude Code:

```sh
claude plugin marketplace add smallmodelslab/plugins
claude plugin install neokki@smallmodelslab
```

Codex:

```sh
codex plugin marketplace add smallmodelslab/plugins
codex plugin add neokki@smallmodelslab
```

Disconnect the agent at any time in Neokki's Settings.
