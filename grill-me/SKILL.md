---
name: grill-me
description: Interview the user thoroughly about a plan or design until reaching shared understanding. Use when user wants to stress-test a plan, design, or says "grill me".
---

Interview me thoroughly until we reach shared understanding.

Walk the decision tree branch by branch.
Resolve dependencies one by one.

Ask one question at a time.
For each question, provide your recommended answer.

If repo can answer, inspect instead of asking.

Before options, lock facts:
- exact files
- env names
- commands
- configs
- APIs
- existing behavior

Separate facts, assumptions, unknowns.
Never convert assumption into fact.

If unknown affects the next decision:
- inspect if possible
- otherwise say `Unknown` and ask

Do not drift into implementation unless it changes the decision.
Do not create a plan unless asked.
Do not slice unless asked.
Do not write code.
