# Question Policy

Use this file when the orchestrator needs user input while turning a PRD into a ticket backlog.

## When To Ask

Ask the user only when a decision materially changes one or more of the following:

- scope,
- launch risk,
- operational complexity,
- cost,
- pricing or quota behavior,
- artifact ownership,
- recovery or rollback rules,
- invariants that later tickets will assume.

If the decision is local, reversible, or can be safely defaulted without affecting downstream ticket structure, do not ask. Pick the default and record it.

## How To Ask

Every question should include:

1. the decision that is unresolved,
2. why it matters,
3. the recommended default,
4. a concrete set of options when the choice is discrete,
5. the downstream impact of each option.

The orchestrator may ask as many questions, and as many rounds of questions, as it genuinely needs to produce a high-quality backlog. Group related decisions together only when the user can answer them independently without confusion. Split them apart when combining them would hide trade-offs or make later ticket-writing weaker.

## Preferred Formats

Use structured multiple-choice questions when the options are discrete and the answer should be easy to select.

Use plain text only when:

- the decision is nuanced,
- the options are not yet stable,
- or the user needs to describe a policy in their own words.

## Recommended Defaults

- Ask every unresolved question that materially affects ticket count, ordering, acceptance criteria, scope, cost, launch risk, or long-lived architecture.
- If there are many open decisions, ask them in as many batches as needed instead of forcing one oversized question set.
- If only one blocker remains, ask that one question by itself.
- If the user does not respond immediately and the default is safe, proceed with the default and note it in the relevant ticket's `Decision Log`.

## Good Question Shape

Use a short preamble, then the choices. A good preamble sounds like this:

`I can finish the backlog with a recommended default here, but this one decision changes ticket scope and rollout behavior.`

Then present the choices with consequences

## What To Avoid

- Do not ask open-ended questions when discrete options would work.
- Do not ask a question whose answer is already implied by the PRD or prior user instructions.
- Do not interrupt the flow repeatedly for minor implementation details that do not change the backlog in a meaningful way.
- Do not ask for choices without explaining the effect on the resulting tickets.
