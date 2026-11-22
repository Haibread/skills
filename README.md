# skills

Personal [Agent Skills](https://agentskills.io), usable by any Agent Skills
compatible client.

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/Haibread/skills/badge)](https://scorecard.dev/viewer/?uri=github.com/Haibread/skills)

## Description

A skill is a directory holding a `SKILL.md` — `name` and `description` in its
frontmatter, instructions in its body — plus whatever scripts, references or
templates those instructions need. An agent reads every skill's name and
description at startup and loads the rest only when a task matches, so a
catalogue costs little context until one of its skills is actually relevant.

This repository is that catalogue: **each skill is a directory at the
repository root**, and nothing else lives there bar this repository's own
documentation and tooling. The format is the open
[Agent Skills specification](https://agentskills.io/specification), so the same
directory works in Claude Code, Cursor, Codex, Copilot, OpenCode and the other
clients that implement it.

It is not a skill authoring tool and not a registry: it holds the skills
themselves.

## Getting started

### Prerequisites

- `git`
- an Agent Skills compatible client

### Installation

Clone the repository:

```sh
git clone https://github.com/Haibread/skills.git
```

Copy the skill directories you want into the skills directory your client
reads — `~/.claude/skills` for Claude Code, `~/.agents/skills` for the
cross-client convention most other clients scan:

```sh
cp -R skills/<skill> ~/.agents/skills/
```

Project-scoped skills go in `.claude/skills/` or `.agents/skills/` inside the
project instead of under `$HOME`.

An Agent Skills manager can also be pointed at this repository, so an update
pulls the current revision and prunes what was removed. Follow the manager's
own documentation for that; the layout above is all it needs.

### Usage

A client discovers the installed skills at startup and activates one when a
task matches its `description`. Nothing is invoked by hand: ask for the work,
and the agent loads the skill that covers it. Each `SKILL.md` states the
conditions it triggers on and the ones it stays out of.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — see [LICENSE](LICENSE).
