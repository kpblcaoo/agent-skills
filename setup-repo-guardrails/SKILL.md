---
name: setup-repo-guardrails
description: Inspect a repository and propose or add minimal quality/security feedback loops for AI-assisted development. Use for linters, tests, type-checks, secret scans, dependency audits, and basic repo blockers.
---

# setup-repo-guardrails

Set up minimal repo guardrails.

Short. Direct. No theater.
No fake maturity.
No assumptions as facts.
No giant checklist.

## Use when

Use this skill when user asks to:
- add repo guardrails
- set up linters
- set up type-checks
- set up tests
- add security checks
- add secret scanning
- add dependency audit
- prepare repo for AI-assisted coding
- add basic blockers before agent work

Do not use for:
- full DevSecOps redesign
- production hardening
- compliance program
- CI platform migration
- speculative security architecture
- tiny obvious edits

## Prime directive

Create fast feedback loops.
Block obvious bad changes.
Do not simulate enterprise maturity.

Small useful guardrail > perfect quality platform.

Guardrails must serve current repo pain:
- catch broken code
- catch unsafe code
- catch leaked secrets
- catch dependency risk
- make agent work reviewable

## Truth

Never convert assumption into fact.

Use facts from:
- repo files
- existing commands
- package manager files
- lockfiles
- CI configs
- test configs
- README/docs
- previous command output
- user request

If unknown:
- inspect if possible
- otherwise mark as `Unknown`

Do not invent stack, commands, tools, package managers, CI, or project layout.

## Operating mode

Default mode: proposal first.

Implement changes only when:
- user explicitly asked to edit files now
- user approved the proposal
- change is tiny, local, and clearly requested

Always propose first before:
- adding dependencies
- changing lockfiles
- adding hooks
- changing CI
- changing formatting rules
- running broad auto-format
- deleting files
- changing security policy

## Discovery

Inspect before recommending.

Look for:
- language and framework
- package manager
- lockfiles
- existing test runner
- existing lint/type-check tools
- existing build command
- existing CI jobs
- existing pre-commit/hooks
- existing Makefile/Justfile/Taskfile/scripts
- existing security tools
- README commands

Prefer existing tools.
If a tool already exists, extend or wire it before adding a new one.
Do not replace working tooling without clear reason.

## Guardrails to consider

Consider only relevant guardrails.

Core:
- format check
- lint
- type-check
- unit tests
- build or smoke command

Security:
- secret scan
- dependency audit
- basic SAST / semantic security lint
- unsafe shell/path handling checks where relevant

Repo blockers:
- single `check` command
- pre-commit hook
- pre-push hook
- CI job
- required local command before agent changes

Do not add all of them by default.

## Selection rules

Start with the smallest useful set.

Prefer 2-5 guardrails per pass.

First pass:
- cover highest-value missing feedback loops
- prefer existing tools and commands
- avoid broad repo churn

Later passes:
- require a new proposal
- should be based on actual pain from first pass
- should not add tools just because they were skipped earlier

Choose guardrails that are:
- fast
- deterministic
- local
- easy to run
- easy to explain
- already close to repo conventions

Avoid guardrails that are:
- slow
- noisy
- hard to configure
- dependent on external services
- likely to block unrelated work
- not supported by current stack
- added only because they sound mature

## Tool choice

Use existing ecosystem defaults when possible.

Examples:
- Python: `ruff`, `pytest`, `mypy`, `bandit`, `pip-audit`
- TypeScript/JavaScript: existing package scripts, `eslint`, `tsc`, test runner, package audit
- Go: `go test`, `go vet`, `gofmt`, `staticcheck`
- Rust: `cargo test`, `cargo fmt --check`, `cargo clippy`
- .NET: `dotnet test`, `dotnet build`, existing analyzers
- Java: existing Gradle/Maven tasks, existing test/lint plugins
- Generic: `gitleaks` or equivalent secret scan

These are hints, not facts.
Inspect repo first.

Add optional or non-default tools only when:
- already used in repo
- clearly justified by current pain
- approved by user

## Dependency rule

Do not add new dependencies casually.

Before adding a dependency, state:
- why existing tooling is insufficient
- exact package/tool
- exact config/file changes
- expected command
- rollback path

Prefer dev dependencies over runtime dependencies.
Prefer pinned versions when practical.
Do not add unpinned curl/bash installers.

## Command rule

Every guardrail needs a command.

Good:
- `npm run lint` — lint must pass
- `pytest tests/test_auth.py` — focused tests must pass
- `ruff check .` — no lint errors
- `gitleaks detect --source .` — no secrets found

Bad:
- run tests
- check lint
- scan security
- make sure it works

If command is unknown:
- write `Command: Unknown`
- write `Must verify: <specific expected behavior>`

## Safety

Never hide:
- secret leaks
- auth/permission changes
- unsafe shell/path handling
- destructive commands
- data loss risk
- broad formatting churn
- noisy false-positive risk
- high-probability near-term breakage

For destructive or irreversible changes:
- stop
- ask confirmation

For risky but reversible changes:
- warn clearly
- keep patch small
- include rollback

When running secret scans:
- never print full secrets
- redact secret values
- report file/path and finding type only when possible
- do not run secret scans over external/home directories unless requested

## Implementation rules

When implementing:

1. change smallest useful set
2. keep config minimal
3. preserve existing style
4. avoid unrelated cleanup
5. avoid broad reformat
6. add one `check` command that runs existing tools if none exists
7. run focused verification

Prefer adding:
- one `check` command
- one config file
- one CI/pre-commit hook only if requested or approved

Do not:
- migrate package managers
- rewrite test structure
- add large frameworks
- add policy docs unless requested
- add security theater
- make unrelated dependency updates

## Output format: proposal

When proposing, return only this structure.

# Repo Guardrails Proposal

## Current facts

- <Detected stack/tooling fact>
- <Existing command/config fact>

## Assumptions

- <Assumption>

Omit this section if there are no assumptions.

## Current gaps

- <Concrete missing feedback loop>
- <Concrete missing feedback loop>

## Recommended pass

1. <Guardrail>
   - Why: <current pain/risk>
   - Command: `<exact command>` or `Unknown`
   - Files: `<path>` or `Unknown`
   - Risk: low | medium | high

2. <Guardrail>

## Not included

- <Guardrail intentionally skipped and why>

## Requires confirmation

- <Change requiring confirmation>

Omit this section if nothing requires confirmation.

## Verification

- `<exact command>` — <expected result>

## Risks

- <Risk and mitigation>

## Open questions

- <Question>

Omit this section if there are no open questions.

## Output format: implementation report

After implementing, return only this structure.

# Repo Guardrails Report

## Changed

- `<file>` — <what changed>

## Added commands

- `<command>` — <what it checks>

## Verification

- `<command>` — passed | failed | not run
- <failure summary if failed>

## Not checked

- <What was not checked and why>

## Risks / follow-up

- <Risk or follow-up>

## Quality bar

Good guardrails:
- catch real mistakes
- are cheap to run
- have exact commands
- match current stack
- extend existing tooling first
- are understandable
- help agent work safely
- avoid noisy fake maturity

Bad guardrails:
- install tools blindly
- add slow checks first
- create broad CI churn
- reformat the whole repo
- add security tools with no consumer
- block work with noisy false positives
- pretend unknown commands exist
