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
| **System 0** | Does the test exist, and is it linked properly? | Deterministic checks: [urzua](https://github.com/urzuahq/urzua) | milliseconds |
| **System 1** | Is this the right test? Does it test what the task says? | A probability from a decision model | about a second |
| **System 2** | What does this test actually do? | Reasoning by an LLM | seconds to minutes |

Ask in that order. Each system hands the next only what it could not settle. System 0 goes first because its answer is the same on every run.

## Start

Paste this into your coding agent:

```text
Read https://github.com/urzuahq/urzua/blob/main/docs/reference/install.md and https://github.com/urzuahq/urzua/blob/main/docs/reference/adopt.md, then set this repository up on urzua.
```

Or install it yourself:

```sh
tag=$(gh release view --repo urzuahq/urzua --json tagName --jq .tagName)
curl -fsSL --proto '=https' --tlsv1.2 "https://raw.githubusercontent.com/urzuahq/urzua/$tag/scripts/install.sh" | sh -s -- --version "$tag"
```

## Projects

| Project | What it checks | When |
|---|---|---|
| [urzua](https://github.com/urzuahq/urzua) | What the records say: this was decided, this is done, this is the evidence. A record engine configured entirely by the repository that uses it. Decision-model checks are on the way for the questions a rule cannot settle. | Every commit and pull request |
| [decision-agent-kit](https://github.com/urzuahq/decision-agent-kit) | What the agent says in the session: it works, it is finished. Scored by a decision model. | The end of every turn |

## What we hold to

- **Evidence over assertion.** "Done" has to point at something that exists.
- **People own decisions.** Agents draft; a named person accepts.
- **Built for machines to read.** Every result is data an agent or CI can act on.
- **Honest about limits.** A check says what it was measured to catch and what it misses.
