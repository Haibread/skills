# Security policy

## Reporting a vulnerability

Report it through GitHub's private vulnerability reporting:
[open a draft advisory](https://github.com/Haibread/skills/security/advisories/new).
The report is visible only to the maintainers and to you, so the fix can be
prepared before anything is public.

Never report a vulnerability through a public issue, pull request or
discussion: described in public, it is disclosed before it is fixed.

A useful report holds:

- the skill and the revision it affects;
- the steps to reproduce it, with the client and agent you ran;
- the impact as you see it.

## Supported versions

This repository cuts no releases. The default branch is the only supported
version.

## Scope

A skill is instructions an agent reads and acts on, so what counts here is
content that makes an agent do something its reader did not ask for:

- a `SKILL.md` or a bundled reference whose instructions exfiltrate data,
  reach a network location, or weaken a protection the client applies;
- a bundled script that is unsafe to run, or that does more than the skill
  describes;
- text crafted to be read as an instruction by an agent while looking inert to
  a human reviewer;
- a link or dependency in a skill pointing at a resource that is not what the
  skill says it is.

Out of scope:

- a vulnerability in an agent client, in a tool a skill invokes, or in another
  dependency: report it to that project, which is where the fix lives;
- a finding that needs an already-compromised host or account;
- a skill doing exactly what it documents, where the objection is to the
  documented behaviour — that is a bug report or a design discussion, so open
  an issue;
- scanner output with no path to exploitation.

## What happens next

1. The report is acknowledged in the draft advisory.
2. The impact and the affected skills are assessed.
3. A fix is prepared in the advisory's private fork.
4. The fix lands on the default branch.
5. The advisory is published, with a CVE requested through GitHub when the
   impact warrants one, and you are credited unless you prefer otherwise.

Reports are handled on a best-effort basis: this is a personal repository with
no response-time commitment.
