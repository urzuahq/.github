<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/urzuahq/.github/main/profile/assets/lockup-dark.svg">
  <img alt="urzua" src="https://raw.githubusercontent.com/urzuahq/.github/main/profile/assets/lockup-light.svg" width="300">
</picture>

### System 0 for agents

**Our mission is to make agent work something you can rely on without reading all of it.**

Agents now write the code, the decisions behind it, and the message saying it is finished. Each of those is a claim, and nothing makes a claim true. People cannot read everything agents produce, so trust has to come from checks a machine can run. How far agent work scales depends on how fast it can be verified.

## Three systems

Agents are usually described with two kinds of thinking: System 1, the fast guess, and System 2, the slow reasoning. Checking their work needs a third kind underneath both, one that does no guessing at all. We call it System 0.

Take the claim an agent makes most often: "this is done, and here is the test."

| | Question | Answered by | Time |
|---|---|---|---|
| **System 0** | Does the test exist, and is it linked properly? | Fast deterministic compute: [urzua](https://github.com/urzuahq/urzua), alongside linters, type checkers and build tools | milliseconds |
| **System 1** | Is this the right test? Does it test what the task says? | Tools built on decision models. [decision-agent-kit](https://github.com/urzuahq/decision-agent-kit) is the kit for building them, and does not have this check yet | about a second |
| **System 2** | What does this test actually do? | LLM inference | seconds to minutes |

Ask in that order. Each system hands the next only what it could not settle. System 0 goes first because it decides by rules you wrote down, so its answer is the same on every run. Systems 1 and 2 decide by probability.

Risk is a separate axis from the three systems. A repository declares ahead of time how risky each kind of change is, and that decides which checks the change must pass. Running those checks and returning one verdict is the job of [garita](https://github.com/urzuahq/garita). garita is in development, and its risk classes are designed but not built.

## Start

Paste this into your coding agent:

```text
Read https://github.com/urzuahq/urzua/blob/main/docs/reference/install.md and https://github.com/urzuahq/urzua/blob/main/docs/reference/adopt.md, then set this repository up on urzua.
```

Or install urzua yourself:

```sh
tag=$(gh release view --repo urzuahq/urzua --json tagName --jq .tagName)
curl -fsSL --proto '=https' --tlsv1.2 "https://raw.githubusercontent.com/urzuahq/urzua/$tag/scripts/install.sh" | sh -s -- --version "$tag"
```

## Projects

| Project | What it is | State |
|---|---|---|
| [urzua](https://github.com/urzuahq/urzua) | A System 0 tool: a record engine. A repository declares its record types, what counts as evidence and who may decide, and urzua checks every change against those rules. | Released, before 1.0 |
| [decision-agent-kit](https://github.com/urzuahq/decision-agent-kit) | A System 1 tool: lets a coding agent's harness ask a decision model about the session, starting with whether a turn is really done. | Works in Claude Code and Codex with SubQ Snap, in shadow mode by default. No release yet |
| [garita](https://github.com/urzuahq/garita) | The control plane: a deterministic gate for agent-authored change. It runs the checks a change must pass for its declared risk, within a budget, and returns one verdict to agents, git hooks and CI. urzua is planned as its first native tool. | In development: RFCs in draft, no release yet |
| [agent-cli-kit](https://github.com/urzuahq/agent-cli-kit) | The output contract for the urzuahq tools: JSON Schemas for what a command prints and returns, so an agent or a control plane can read any tool without a parser for each. | Release candidate `v1.0.0-rc.1` |

## What we hold to

- **Evidence over assertion.** "Done" has to point at something that exists.
- **People own decisions.** Agents draft; a named person accepts.
- **Built for machines to read.** Every result is data an agent or CI can act on.
- **Honest about limits.** A check says what it was measured to catch and what it misses.
