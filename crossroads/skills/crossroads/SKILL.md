---
name: crossroads
description: Ask the same typed questions about many inputs at once with the crossroads command, such as routing tickets, labelling files, scoring urgency or checking each line of a list. Use when one set of questions should be answered for every file or line, with an option from a list, a yes or no or a number on a scale, each with its probabilities.
---

# Crossroads

`crossroads run` asks every question about each input and prints one JSON
line per input, in order.

## Install and sign in

If `crossroads version` fails, install it (macOS on Apple silicon, Linux):

```sh
curl -fsSL https://smallmodelslab.ai/install.sh | sh
```

It lands in `~/.local/bin` and updates itself.

If a run says it is not signed in, start `crossroads login` in the
background. It prints a link: give it to the person and wait for the command
to finish, which it does once they approve (up to 30 minutes). The key is
kept in `~/.smlabs.toml`; never print it. Crossroads is in early access: if
they have no account, follow "Request access" in
https://smallmodelslab.ai/agents.md first.

## Run

Questions come before the inputs. Each is `NAME=INSTRUCTION`:

```sh
crossroads run \
  --choice "team=Which team should handle this request?" --options billing,engineering,sales \
  --bool "needs_reply=Does this message need a reply?" \
  --score "urgency=How urgent is this request?" --range 1,5 \
  tickets/*.txt
```

```json
{"input":"tickets/1.txt","answers":{"needs_reply":{"value":true,"probability":0.94},"team":{"choice":"billing","probabilities":{"billing":0.91,"engineering":0.06,"sales":0.03}},"urgency":{"score":3.48,"probabilities":{"1":0.02,"2":0.08,"3":0.41,"4":0.38,"5":0.11}}}}
{"input":"tickets/2.txt","error":{"code":"invalid_request","message":"…"}}
```

- A yes or no answers `{"value", "probability"}`, the probability of yes; a
  choice `{"choice", "probabilities"}`, one per option; a score
  `{"score", "probabilities"}`, the expected level and one per level.
- Inputs are files, one input each. With no files, each non-empty line of
  standard input is one input, labelled `stdin:<line>`; `-` reads all of
  standard input as one.
- Up to 16 questions; each input up to 48,000 characters. Choices take 2 to
  32 options, comma-separated.
- The command exits non-zero when any input failed; the others still print.
- Running the same inputs and questions again replays the saved answers
  without another charge. Usage costs $0.04 per million input tokens.
