# Contributing

Open an issue or a pull request on
[the repository](https://github.com/Haibread/skills). The short version:
install the tooling with mise, add your skill as a directory at the repository
root, and get `task lint` green.

## Development setup

Install [mise](https://mise.jdx.dev/installing-mise.html), which installs
every other tool this repository needs — the versions are pinned in
[`mise.toml`](mise.toml), so nothing else is installed by hand.

```sh
mise trust
```

```sh
mise install
```

```sh
task setup
```

`task --list` then shows the available commands, and `task lint` proves the
setup is good: it runs the whole gate and must pass from a fresh clone.

See [README.md](README.md#getting-started) for installing the skills into a
client.

## Running the tests

There is no test suite: the repository holds skill content, not code. What
stands in for one is the structural and content validation of every skill,
which runs as a pre-commit hook and therefore through `task lint`:

```sh
task lint
```

```sh
pre-commit run skill-validator --all-files
```

A new or changed skill is expected to pass that check with no errors and no
warnings before the pull request is opened. The validator resolves the links a
`SKILL.md` contains, so it needs network access.

## Pre-commit hooks

`task setup` installs the hooks, and they must pass before anything is pushed.
The hook list is in [`.pre-commit-config.yaml`](.pre-commit-config.yaml).

Run the whole repository:

```sh
task lint
```

Re-run a single hook while iterating:

```sh
pre-commit run <hook-id> --all-files
```

The ones whose failure needs explaining:

| Hook | What it checks | How to fix |
| --- | --- | --- |
| `skill-validator` | each skill against the Agent Skills specification, plus link resolution and content quality | fix what the report names; it prints the file and the rule |
| `yamllint` | YAML style — block style only, no leading `---` | rewrite the offending lines; it does not autofix |
| `actionlint` | the GitHub Actions workflows | fix the expression or key it names |
| `no-co-authors` | the commit message carries no co-author or attribution trailer | rewrite the message |

`trailing-whitespace`, `end-of-file-fixer` and `mise-fmt` fix the files
themselves — re-stage and commit again.

`--no-verify` and `SKIP=` are not the fix. A red hook is a real finding:
correct the content, or change the hook's configuration in the same pull
request and say why. The same hooks run in CI, so skipping them locally only
moves the failure somewhere slower.

## Continuous integration

| Workflow | Purpose | Reproduce locally |
| --- | --- | --- |
| [`quality.yaml`](.github/workflows/quality.yaml) | the quality gate | `task lint` |
| [`scorecard.yaml`](.github/workflows/scorecard.yaml) | OpenSSF Scorecard supply-chain grading | — |

`quality` is the only blocking check, and `task lint` reproduces it in full.
`scorecard` never runs on a pull request: it grades the repository's
supply-chain practices and publishes the result read by the README badge, so
it is informational and has no local equivalent. Neither workflow needs a
secret.

## Submitting a change

- Branch off `main`, named after the change.
- Commit subjects are imperative, lowercase and short — `git log --oneline` is
  the reference.
- One skill per pull request, with green CI.
- Update [`README.md`](README.md) and this file in the same pull request when
  the change affects them.
