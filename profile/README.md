# urzuahq

**We build the checking layer for agent work: tools that let you rely on what coding agents say they did.**

Agents now write the code, the decisions behind it, and the message saying it is finished. Each of those is a claim, and nothing makes a claim true. As agents do more of the work, people cannot read all of it, so trust has to come from checks a machine can run. How far agent work scales depends on how fast it can be verified.

| Project | What it checks | When |
|---|---|---|
| [urzua](https://github.com/urzuahq/urzua) | What the records say: this was decided, this is done, this is the evidence. Deterministic checks that run in milliseconds, with decision-model checks on the way for the questions a rule cannot settle. | Every commit and pull request |
| [decision-agent-kit](https://github.com/urzuahq/decision-agent-kit) | What the agent says in the session: it works, it is finished. Scored by a decision model. | The end of every turn |

## What both hold to

- **Evidence over assertion.** "Done" has to point at something that exists.
- **People own decisions.** Agents draft; a named person accepts.
- **Built for machines to read.** Every result is data an agent or CI can act on.
- **Honest about limits.** A check says what it was measured to catch and what it misses.

## Three speeds of checking

Checking agent work is three different questions, each with its own speed. A fact you can compute ("is there a linked test?") takes milliseconds. A judgement you can score ("does the test check the thing it claims?") takes about a second with a decision model. An explanation you have to reason out ("how does this work, and what did it miss?") takes a large model and real time. Ask them in that order, and each layer hands the next one only what it could not settle.
