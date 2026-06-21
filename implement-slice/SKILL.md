---
name: implement-slice
description: Implement exactly one approved slice. Use after slice-plan when the user asks to execute a specific slice.
---

# implement-slice

Implement one slice.

Short. Direct. No theater.
No bonus work.
No assumptions as facts.

## Use when

Use this skill when user asks to:
- implement a slice
- execute Slice N
- work on one planned chunk
- continue from `slice-plan`
- make one bounded change before review

Use after `slice-plan`.

Do not use for:
- unclear tasks
- unresolved design
- multiple slices at once
- broad refactors
- repo-wide cleanup
- speculative improvement

## Prime directive

One slice. No bonus work.

Implement only the requested slice.
Keep repo usable.
Run the narrowest useful check.
Report evidence.
Stop.

Small verified change > large clever change.

## Truth

Never convert assumption into fact.

Use facts from:
- approved slice
- approved plan
- user request
- repo files
- tests
- docs
- configs
- error output
- previous command output

If unknown:
- inspect if possible
- otherwise mark as `Unknown`

Do not invent files, APIs, commands, env vars, config fields, dependencies, or project structure.

## Pre-check

Before editing, confirm the slice is executable.

The slice must have:
- one clear goal
- explicit non-goals
- files or areas to inspect
- acceptance criteria
- verification path
- risk level
- AFK/HITL mode

If the requested slice is `HITL`, check why.

Stop and ask confirmation before editing when:
- destructive change is possible
- public contract may change
- behavior change is ambiguous
- security risk exists
- migration is involved
- required decision is unresolved

If ambiguity changes implementation:
- ask one clear question before editing

If safe default exists:
- state the assumption
- continue

## Lock implementation facts

Before editing, lock repo-specific facts.

Find exact:
- existing env names
- existing commands
- existing config fields
- files to edit
- tests or checks to run
- external syntax, if used

Do not implement with generic placeholders when repo-specific facts exist.

Bad:
- use `MODEL_NAME`
- run `npm test`
- edit config file
- add timeout setting

Good:
- use existing `MODEL_ID`
- run `./scripts/smoke-e2e.sh <offer-id> --destroy`
- edit `scripts/create-instance.sh`
- add `VLLM_MAX_MODEL_LEN`

External syntax stays `Unknown` until verified.

Examples:
- CLI flag syntax
- YAML schema
- GitHub Actions field
- Docker Compose option
- tool-specific config key

If exact facts cannot be found:
- mark them `Unknown`
- do not pretend
- ask only if the unknown changes implementation

## Scope control

Stay inside the slice.

Allowed:
- files needed for this slice
- tests/checks needed for this slice
- minimal docs update if acceptance criteria require it

Not allowed:
- next slice
- unrelated cleanup
- broad reformat
- dependency upgrades
- architecture scaffolding
- opportunistic refactor
- new abstraction without current need
- changing public behavior outside the slice

If you find adjacent issue:
- report it under `Not done`
- do not fix it unless it blocks this slice

## Implementation rules

Before editing:
1. restate slice goal
2. lock implementation facts
3. inspect nearest existing pattern
4. choose smallest safe change

While editing:
1. change the minimum files
2. preserve existing style
3. avoid unrelated formatting
4. keep behavior narrow
5. keep rollback easy

After editing:
1. run exact slice verification
2. run narrower check first if full check is expensive
3. rerun failed command after fix
4. stop after slice is done

Do not continue into the next slice.

## Verification rules

Run the exact verification from the slice when possible.

If exact command is known:
- run it
- report pass/fail
- include exact failure summary if failed

If command is unknown:
- write `Command: Unknown`
- write `Must verify: <specific expected behavior>`

If verification cannot run:
- say why
- do not claim success
- provide manual check or next exact command

Good:
- `pytest tests/test_auth.py::test_expired_token_rejected` — passed
- `ruff check src/auth.py` — failed: unused import
- `./scripts/smoke-e2e.sh 34025117 --destroy` — not run: requires paid instance

Bad:
- tests pass
- lint ok
- should work
- verified manually

## Safety

Never hide:
- secret leaks
- auth/permission changes
- unsafe shell/path handling
- destructive commands
- data loss risk
- broad formatting churn
- public contract changes
- high-probability near-term breakage

For destructive or irreversible changes:
- stop
- ask confirmation

For risky but reversible changes:
- warn clearly
- keep patch small
- include rollback

Never print full secrets.
Redact secret values.

## Output format: before editing

If a pre-edit summary is useful, use this structure.

# Slice Execution Plan

## Slice

<Slice title / number>

## Goal

<One concrete goal>

## Risk

<low | medium | high> — <one-line reason if medium or high>

## Locked facts

- Env: `<exact env name>` or `Unknown`
- Commands: `<exact command>` or `Unknown`
- Config fields: `<exact field>` or `Unknown`
- Files: `<exact file>` or `Unknown`
- External syntax: `<verified syntax>` or `Unknown`

## Assumptions

- <Assumption>

Omit this section if there are no assumptions.

## Will change

- `<file>` — <change>

## Will not change

- <Non-goal>

## Verification

- `<exact command>` — <expected result>

## Needs confirmation

- <Reason>

Omit this section if no confirmation is needed.

## Output format: implementation report

After implementing, return only this structure.

# Slice Implementation Report

## Slice

<Slice title / number>

## Changed

- `<file>` — <what changed>

## Not changed

- <Relevant non-goal preserved>
- <Adjacent issue found but not fixed>

## Verification

- `<command>` — passed | failed | not run
- <failure summary if failed>

## Not checked

- <What was not checked and why>

## Risks / follow-up

- <Risk or follow-up>

## Quality bar

Good implementation:
- completes exactly one slice
- uses exact repo facts
- edits minimal files
- preserves existing style
- runs exact verification when possible
- reports unknowns honestly
- stops after done

Bad implementation:
- starts next slice
- uses placeholder env names
- invents commands
- changes unrelated files
- broad-reformats repo
- adds abstraction without current need
- claims success without checks
- hides risky behavior changes
