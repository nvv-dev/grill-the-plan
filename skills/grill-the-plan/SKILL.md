---
name: grill-the-plan
description: Use when a spec, plan or design needs to be pressure-tested before implementation — "grill me on this plan", "what am I missing?", or as the clarification step between a spec and a technical plan. Interrogates the plan one decision at a time and records the answers in the glossary and ADRs.
disable-model-invocation: true
---

# Grill the plan

Walk the plan as a decision tree and resolve every open branch with the human before anyone writes code. Ambiguity found now costs a question; found in review it costs a rewrite.

## How to run it

1. Read the spec or plan, the project glossary (`GLOSSARY.md` or equivalent) and the existing ADRs (`docs/adr/`). Do not ask about anything they already answer.
2. List the open decisions as a tree: scope, actors, data, states and transitions, error cases, permissions, integrations, non-functional limits (volume, latency, cost), rollout and migration.
3. Ask **one question at a time**, starting with the branch that unblocks the most others. Offer 2–4 concrete options with their consequences, and say which you would pick and why.
4. After each answer:
   - add or fix the term in the glossary if the answer introduced or sharpened a domain term;
   - if the decision is costly to reverse, draft an ADR (see `writing-adrs`);
   - mark the branch resolved and move to the next.
5. Stop when every branch is resolved or explicitly deferred with an owner and a date.

## Rules

- No question the documents already answer. No question whose answer would not change the design.
- Use the glossary's terms exactly. If the human uses a different word for the same thing, ask which one wins and record it.
- Do not move from spec to plan while any `[NEEDS CLARIFICATION]` marker or open branch remains, unless the human accepts the risk explicitly; record that acceptance.
- Keep each question short. The human may answer from a phone.

## Output

- The updated glossary entries and ADR drafts (as file changes or a patch).
- A summary: resolved decisions (one line each), deferred decisions (owner, date), risks the human accepted.

## Known failures

_Record real mistakes here with a date and the rule that prevents them._
