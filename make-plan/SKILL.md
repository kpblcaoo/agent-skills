---
name: make-plan
description: Create a short implementation plan from a task, discussion, issue, bug report, or grill-me summary. Use when user asks to plan, or before risky/non-trivial edits where implementation path is unclear.
---

# make-plan

Create an implementation plan.

Short. Direct. No theater.
No fake maturity.
No assumptions as facts.

## Use when

Use this skill when user asks to:
- make a plan
- plan implementation
- summarize next steps
- turn discussion into work plan
- prepare before coding
- plan after grill-me

Do not use for tiny obvious edits.

## Prime directive

Fix current pain.
Small correct plan > impressive plan.
Challenge overengineering.
Prefer existing patterns over new abstractions.

## Truth

Never convert assumption into fact.

Use facts from:
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

Do not invent files, APIs, commands, dependencies, or project structure.

## Ambiguity

If ambiguity changes implementation, ask one clear question before planning.

If safe default exists:
- state the assumption
- continue

Do not ask questions that only polish the plan.

## Plan rules

Plan must be implementable.
Plan must be scoped.
Plan must include verification.
Plan must include non-goals.

Do not hide unresolved decisions inside steps.
Do not create broad phases like:
- refactor architecture
- improve tests
- clean code
- add security

Make each step bounded.

A step should be one of:
- one concrete code/docs/config change
- one command to run
- one decision to make
- one focused verification action

If a step touches many files, many concepts, or many risks, split it.

Bad step:
- update the auth module

Good steps:
- add token expiry validation in `auth/session.ts`
- update session expiry tests
- run `npm test -- auth/session`

## Abstraction rule

Add abstraction only when there is:
- current duplication
- current pain
- current contract risk
- current security risk
- unavoidable near-term breakage risk

Otherwise keep design boring.

## Verification rules

Name the exact check when known:
- exact test command
- exact lint command
- exact type-check command
- exact build command
- exact manual repro step
- exact command that failed before

If command is unknown, say what must be checked and mark command as `Unknown`.

Do not write only:
- run tests
- check lint
- verify manually

## Output format

Return only this structure.

# Plan

## Problem

<What hurts now. Concrete.>

## Goal

<Desired end state. Concrete.>

## Non-goals

- <What will not be done>

## Current facts

- <Known fact>
- <Known fact>

## Assumptions

- <Assumption>

Omit this section if there are no assumptions.

## Decisions

- <Decision 1>
- <Decision 2>

Use 1-3 decisions.
Do not force a single "main" decision if the plan has independent choices.

## Steps

1. <Bounded concrete step>
2. <Bounded concrete step>
3. <Bounded concrete step>

## Verification

- `<exact command>` — <what must pass>
- <manual check> — <expected result>

## Risks

- <Risk and mitigation>

## Open questions

- <Question>

Omit this section if there are no open questions.

## Quality bar

A good plan:
- can be executed without guessing
- has a clear stopping point
- avoids speculative architecture
- names what will not be done
- separates facts from assumptions
- names exact verification when known
- exposes risks honestly

A bad plan:
- sounds impressive
- hides decisions
- creates vague phases
- adds abstractions without current need
- says "run tests" without naming a check
- pretends unknowns are facts
