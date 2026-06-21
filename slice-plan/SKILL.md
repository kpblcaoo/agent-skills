---
name: slice-plan
description: Split an approved implementation plan into small, ordered, verifiable implementation slices. Use after make-plan and before coding.
---

# slice-plan

Split a plan into implementation slices.

Short. Direct. No theater.
No issue tracker.
No fake maturity.
No assumptions as facts.

## Use when

Use this skill when user asks to:
- slice a plan
- split work into chunks
- prepare implementation slices
- make execution steps from a plan
- turn a plan into agent-sized tasks

Use after `make-plan`.

Do not use for:
- unclear tasks
- unresolved design
- tiny obvious edits
- creating GitHub issues

## Prime directive

Make work executable.
Make work reviewable.
Make work stoppable.

Small verified slice > large impressive phase.

Each slice must reduce uncertainty or deliver working behavior.

## Truth

Never convert assumption into fact.

Use facts from:
- approved plan
- user request
- current discussion
- repo files
- tests
- docs
- configs
- error output

If unknown:
- inspect if possible
- otherwise mark as `Unknown`

Do not invent files, commands, APIs, dependencies, or project structure.

## Pre-check

Before slicing, check the plan.

Do not slice if the plan lacks:
- clear goal
- non-goals
- concrete decisions
- verification path

If unresolved decisions affect slice order or implementation:
- stop
- ask one clear question

If safe default exists:
- state the assumption
- continue

Before slicing, lock implementation facts:
- exact existing env names
- exact existing commands
- exact existing config fields
- exact files to edit
- external syntax marked `Unknown` until verified

Do not slice with generic placeholder env names, commands, config keys, or file paths when repo-specific facts exist.

## Slice rules

A slice is a small unit of implementation.

A good slice:
- has one goal
- has clear boundary
- can be reviewed alone
- can be verified alone
- leaves repo in a usable state
- avoids speculative architecture

A bad slice:
- says "refactor module"
- says "add tests"
- says "implement feature"
- touches many unrelated concepts
- creates abstraction before behavior
- cannot be verified until many later slices

Prefer vertical slices.

Bad:
- create interfaces
- implement services
- add tests
- wire UI

Good:
- add one failing test for expired token behavior
- implement expired token rejection
- wire rejection into existing auth path
- update docs for token expiry behavior

## Size

Prefer 3-7 slices.

More than 7 slices is allowed only when complexity is real.

If there are more than 10 slices:
- merge adjacent low-risk mechanical slices
- split into a separate sub-plan only if there are multiple independent goals
- otherwise simplify the plan

Split a slice if it has:
- multiple goals
- multiple risky files
- multiple unrelated checks
- unclear review boundary
- hidden design decision

## Ordering

Order slices by dependency.

Prefer this order:
1. lock current behavior
2. add or adjust contract
3. implement smallest behavior
4. handle failure path
5. wire integration
6. remove obsolete code
7. update docs

Skip steps that do not apply.

If no tests exist, still prefer first locking behavior with:
- focused characterization test
- minimal regression test
- manual repro command
- captured failing command

Do not start with cleanup unless cleanup is required for the first working slice.

## AFK / HITL

Mark each slice:

`AFK` when:
- implementation is mechanical
- scope is clear
- risk is low
- checks are known
- no product/design decision remains

`HITL` when:
- decision is needed
- destructive change is possible
- behavior may change
- public contract may change
- security risk exists
- migration is involved
- uncertainty is high

If unsure, mark `HITL`.

## Verification rules

Each slice must name exact verification when known:
- exact test command
- exact lint command
- exact type-check command
- exact build command
- exact manual repro step
- exact command that failed before

If command is unknown, write:
- `Command: Unknown`
- `Must verify: <specific expected behavior>`

Do not write only:
- run tests
- check manually
- verify it works

## Safety

For destructive or irreversible changes:
- mark slice `HITL`
- require confirmation before execution

For risky but reversible changes:
- mark the risk
- include rollback or mitigation

Never hide:
- security bugs
- data loss risk
- secret leaks
- auth/permission changes
- unsafe shell/path handling
- high-probability near-term breakage

## Output format

Return only this structure.

# Slices

## Summary

<One paragraph. What this slice set achieves.>

## Assumptions

- <Assumption>

Omit this section if there are no assumptions.

## Slice 1: <title>

Mode: AFK | HITL  
Depends on: none | Slice N  
Risk: low | medium | high

### Goal

<One concrete goal.>

### Change

- <Concrete change>
- <Concrete change>

### Files / areas

- `<path or area>`
- `<path or area>`

Use `Unknown` if not inspected.

### Acceptance criteria

- <Observable result>
- <Observable result>

### Verification

- `<exact command>` — <expected result>
- <manual check> — <expected result>

### Non-goals

- <What this slice must not do>

### Risks

- <Risk and mitigation>

Omit this section if risk is low and obvious.

---

## Slice 2: <title>

<same structure>

## Final check

- `<exact command>` — <expected result>
- <manual check> — <expected result>

## Not included

- <Explicitly excluded work>

## Open questions

- <Question>

Omit this section if there are no open questions.

## Quality bar

Good slicing:
- preserves working repo after each slice
- makes review easy
- makes rollback possible
- keeps tests close to behavior
- avoids horizontal architecture work
- avoids issue-tracker language
- exposes HITL points clearly

Bad slicing:
- creates vague phases
- delays verification to the end
- separates tests from implementation without reason
- starts with architecture scaffolding
- hides risky decisions inside AFK work
- turns plan into fake project management
