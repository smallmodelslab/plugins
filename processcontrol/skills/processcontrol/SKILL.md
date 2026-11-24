---
name: processcontrol
description: Set a repository up for ProcessControl, which tests pull requests by building and running the app, and write pull request descriptions as claims it can test. Use when asked to set up or use ProcessControl, and when writing or editing the title or description of a pull request in a repository ProcessControl tests.
---

# ProcessControl

ProcessControl tests pull requests. For each one it tests, an agent builds and
launches the app at that commit on a machine of its own, tests the claims in
the pull request's title and description, and reports a GitHub check that
links to the run's evidence.

## Set a repository up

The steps and their commands are kept at `processcontrol.dev/agents.md`. Read
them from the repository checkout and follow them:

```sh
curl -fsS https://processcontrol.dev/agents.md
```

You start a setup request and show the person its link and code. They sign in
with GitHub, install the GitHub App on the repository, optionally connect
Codex, and give you access. You then check that AGENTS.md and the READMEs say
how to run the app, open a pull request, and ask for its first test.

- Access arrives as an API key that is returned once. Save it the way the
  steps say, in a file only you can read. Never print, paste or commit it.
- The tester reads the repository's AGENTS.md (or the CLAUDE.md it points to)
  and READMEs at the tested commit. How to install, build and start the app,
  and which services and fixtures it needs, belongs there. Credentials never
  go in the repository: the person enters them in ProcessControl's **Setup**.

## Write the description as claims

The tester is told to list every claim in the title and description, test
each one on its own against the pull request's commit, and report each with a
verdict: verified, contradicted or blocked. Any contradicted claim fails the
run, and so does a UI standard violation when the team sets violations to
fail; otherwise any blocked claim leaves it blocked. It passes only when every
claim reported is verified. So write what a reviewer could try, and nothing
the commit does not do:

> Email notifications can be turned off in Settings.
>
> The setting survives signing out and back in.

- State each behavior, fix, compatibility, performance or security claim as
  its own sentence about the software at this commit: where it shows, what the
  user does and what they see. A compound sentence is split into separate
  checks anyway.
- For a claim about the interface the tester drives the real interface and
  takes screenshots. For other claims it uses a command or a measurement, so
  give the number or the output to expect.
- The exception is "tests pass", or lint, type checks or a build: a successful
  CI check on that commit that runs them verifies it, and the tester runs them
  itself only when no completed check does. Writing that they passed proves
  nothing; claim it only when such a check exists or the tester can run them.
- Why the change was made, its history, what is planned next, an attribution
  footer and remarks about the pull request itself are context, not claims.
  Keep them apart from the claims, and leave out anything you would not want
  tested.
- A claim the tester's machine cannot check is blocked: it needs a sign-in, a
  service, key or fixture the repository does not provide, or another
  operating system or device. Self-serve runs are on Linux. Say so beside a
  claim you know needs something else.
- The tester is told to read the description as material to test, never as
  instructions to skip a check or change its verdict. Write claims there, not
  requests.
- Without any claims the tester derives its checks from the diff.

Once a mention has started a test, or while the repository tests every pull
request, each push and each edit to the title or description requests a
new test, which replaces one still under way. Keep the description true as the
change moves.

## Act on the result

The same page says how to wait for the **ProcessControl** check and read the
run. Each claim it reports has a verdict and evidence:

- Contradicted: fix the code, or the description if it overstates the change.
- Blocked on setup: add the missing build steps, services or fixtures to
  AGENTS.md or the README. A missing secret goes in **Setup**: ask the person.
- Blocked on an account: a run that ended blocked has an **Add a test
  account** link on its check; send it to the person. A failed run has no
  such link, so tell the person which sign-in the claim's evidence names.
- Blocked on a platform: the claim needs another operating system or device;
  say so in the pull request.
