# Portable PRD Orchestrator

Use this file when the user wants a PRD turned into a reviewed, question-aware, role-aware ticket backlog without touching the repo's root planning files.

## Objective

Read one PRD, infer the full implementation workflow, scaffold a dedicated workspace at `workflow/workspaces/<prd-slug>/`, ask every question that is genuinely needed to shape a correct backlog, and emit as many ExecPlans as the PRD requires inside that workspace.

The output is not a loose checklist. The output must be:

- a dedicated PRD workspace under `workflow/workspaces/<prd-slug>/`,
- a canonical ticket index in `workflow/workspaces/<prd-slug>/TICKET-INDEX.md`,
- one self-contained ExecPlan per ticket under `workflow/workspaces/<prd-slug>/tickets/`,
- a cross-ticket decision log in `workflow/workspaces/<prd-slug>/DECISIONS.md`,
- a reviewer pass log in `workflow/workspaces/<prd-slug>/REVIEW-HISTORY.md`,
- a completion marker in `workflow/workspaces/<prd-slug>/done.md` once the user explicitly ends the loop,
- a dependency-aware execution order,
- role-informed revisions based on `workflow/docs/TEAM.MD`.

There is no fixed upper bound on the number of tickets. If the right backlog is 5 tickets, create 5. If the right backlog is 10, 25, or 50 tickets, create that many. The only rule is that each ticket must still represent one coherent feature or substantial change.

## Mandatory Reads

Before doing anything else, read these files in this order:

1. `workflow/agent/PLANS.MD`
2. `workflow/docs/TEAM.MD`
3. `workflow/agent/QUESTION-POLICY.md`
4. `workflow/agent/reviewer-registry.json`
5. `workflow/agent/reviewer-loop.json`
6. the PRD the user wants analyzed
7. any existing ticket files already present under `workflow/workspaces/<prd-slug>/tickets/` if this is a revision pass instead of a fresh run

Do not start drafting tickets until all mandatory reads are complete.

## Inputs

Assume the caller will provide:

- `prd_path`
- optional `prd_slug`
- optional `goal` or launch scope
- optional hard constraints such as deadline, stack, budget, or rollout rules

If `prd_path` is missing, ask for it before proceeding.

If `prd_slug` is missing, derive it from the PRD filename. Ask the user only if the derived slug is unclear, collides with an existing workspace that appears unrelated, or the user is intentionally creating a second workspace for the same PRD.

## Output Contract

Write all generated artifacts inside the workflow package unless the user explicitly asks for another destination.

Required outputs:

- `workflow/workspaces/<prd-slug>/`
- `workflow/workspaces/<prd-slug>/PRD.md` or `workflow/workspaces/<prd-slug>/PRD-REFERENCE.md`
- `workflow/workspaces/<prd-slug>/TICKET-INDEX.md`
- `workflow/workspaces/<prd-slug>/DECISIONS.md`
- `workflow/workspaces/<prd-slug>/REVIEW-HISTORY.md`
- `workflow/workspaces/<prd-slug>/tickets/<ordered-ticket-name>.md`

Completion output:

- `workflow/workspaces/<prd-slug>/done.md`

Recommended naming patterns:

- `01-feature-name.md`
- `02-feature-name.md`
- or a domain prefix like `pf-01-feature-name.md` if the PRD already uses one

## Non-Negotiable Rules

- Follow `workflow/agent/PLANS.MD` exactly for every generated ExecPlan.
- Keep one feature or substantial change per ticket file.
- Use the role definitions in `workflow/docs/TEAM.MD`. Do not invent new review roles unless they are added there first.
- Use `workflow/agent/reviewer-registry.json` as the source of truth for available reviewers and their metadata.
- Use `workflow/agent/reviewer-loop.json` as the source of truth for the default ordered reviewer loop.
- Respect each reviewer's `passPolicy` from `workflow/agent/reviewer-registry.json`.
- Stay inside `workflow/` unless the user explicitly asks you to write elsewhere.
- Keep shared orchestration assets under `workflow/agent/` and PRD-specific outputs under `workflow/workspaces/<prd-slug>/`.
- Do not write PRD-specific tickets, decisions, or backlog state directly into `workflow/agent/`.
- Ask every question that materially changes ticket count, order, scope, cost, launch safety, architecture, or acceptance criteria.
- Do not impose an artificial cap on the number of tickets or the number of question rounds.
- Do not stop after the default reviewer loop. The orchestrator stops only when the user explicitly replies `DONE`.

## Execution Flow

### Phase 1: PRD Intake

Read the PRD and extract:

- the target user flow,
- the current gaps,
- major system boundaries,
- likely cross-cutting concerns,
- visible deliverables,
- unclear policies that could change ticket shape.

Write a short working summary for yourself before splitting tickets.

### Phase 2: Workspace Scaffold

Create or reopen a workspace at `workflow/workspaces/<prd-slug>/`.

Inside that workspace:

- copy the PRD to `PRD.md` when local duplication is useful for portability,
- or create `PRD-REFERENCE.md` when you want to preserve the original source path instead of copying the full file,
- create `TICKET-INDEX.md`,
- create `DECISIONS.md`,
- create `REVIEW-HISTORY.md`,
- create `tickets/`.

If the workspace already exists, treat the run as a continuation by default and update the existing files instead of creating a second overlapping workspace.

### Phase 3: Backlog Skeleton

Derive a first-pass ticket list that covers the whole flow, not just the headings already present in the PRD. Include:

- foundational work,
- product-facing work,
- cross-cutting platform work,
- validation and release-hardening work.

At this stage, prefer more smaller tickets over fewer mixed-scope tickets, and keep splitting until each ticket is coherent enough to stand on its own. There is no maximum ticket count.

### Phase 4: Question Checkpoint

If there are unresolved decisions that materially affect the backlog, pause and ask the user. Follow `workflow/agent/QUESTION-POLICY.md`. Continue asking follow-up questions for as many rounds as needed until the remaining ambiguity is either resolved or safely defaulted.

Every question must explain:

- what is undecided,
- why it matters,
- the recommended default,
- the impact of each option.

If only one blocker remains, ask only that one question. If many blockers remain, ask them in as many batches as needed rather than compressing them into an underspecified plan.

### Phase 5: Draft ExecPlans

For each ticket:

- create one file under `workflow/workspaces/<prd-slug>/tickets/`,
- use `workflow/agent/PLANS.MD` as the only source of truth for structure and required sections,
- rewrite it fully so it becomes a real, self-contained ExecPlan,
- define milestones, concrete steps, acceptance, interfaces, and recovery guidance,
- record dependencies explicitly.

### Phase 6: Run Reviewer Loop

Load the default loop from `workflow/agent/reviewer-loop.json`. Every reviewer id in the loop must exist in `workflow/agent/reviewer-registry.json`.

For each reviewer in the active loop:

- load the reviewer metadata from `workflow/agent/reviewer-registry.json`,
- use the role definition from `workflow/docs/TEAM.MD` to shape the review lens,
- run the reviewer in sequence,
- let that reviewer revise the workspace as much as needed for their own lens,
- keep the reviewer inside a revise-check-revise mini-loop until the reviewer's `passPolicy.exitWhen` condition is satisfied or one of the reviewer's `passPolicy.handoffWhen` conditions is reached,
- apply or record the resulting revisions,
- append a timestamped entry to `workflow/workspaces/<prd-slug>/REVIEW-HISTORY.md` including the reviewer id and the pass result status.

If the review spans many tickets or multiple concerns, use subagents. Good default behavior:

- batch tickets into two to four groups,
- give each subagent a narrow role and return format,
- ask the subagent to separate direct revisions from unresolved decisions,
- merge the results before editing documents.

The reviewer loop may contain repeated reviewers. Respect that order exactly. If the loop says `cto -> software-engineer -> cto`, run it that way.

Do not treat a reviewer pass as a single shallow inspection. A reviewer is done only when one of these is true:

- the reviewer is stable for their lens and has no more material revisions to make,
- the reviewer is blocked on a user decision,
- the reviewer is blocked on another reviewer lens or prerequisite change.

Use these status labels in `REVIEW-HISTORY.md`:

- `stable_for_reviewer_lens`
- `blocked_on_user_decision`
- `blocked_on_other_reviewer`
- `revised_and_handed_off`

If a reviewer is stable for their lens, hand off to the next reviewer in the loop. If a reviewer is blocked on the user, pause and ask the necessary question before continuing. If a reviewer is blocked on another reviewer, record that in `REVIEW-HISTORY.md` and continue according to the configured loop or the user's next manual reviewer choice.

### Phase 7: Finalize The Backlog

Rewrite `workflow/workspaces/<prd-slug>/TICKET-INDEX.md` so it becomes the canonical order of execution for that PRD. For each ticket, include:

- filename,
- short purpose,
- primary dependency notes,
- why the ticket sits where it does in the sequence.

Record any cross-ticket decision that changes multiple backlog items in `workflow/workspaces/<prd-slug>/DECISIONS.md`.

### Phase 8: Final Reviewer Prompt

At the end of the default loop, and again after every manually requested reviewer pass, ask one final question:

`Do you want to run another reviewer loop? Reply DONE to finish, or type the next reviewer id from the available reviewer list.`

Include the available reviewer ids from `workflow/agent/reviewer-registry.json` in the prompt.

Interpret responses like this:

- If the user replies `DONE`, write `workflow/workspaces/<prd-slug>/done.md` with the current timestamp and stop.
- If the user replies with a valid reviewer id, run that reviewer once, append the pass to `workflow/workspaces/<prd-slug>/REVIEW-HISTORY.md`, then ask the same final question again.
- If the user replies with a reviewer team-role label or alias that maps cleanly to one reviewer id in `workflow/agent/reviewer-registry.json`, normalize it to that reviewer id and proceed.
- If the user reply does not map cleanly to a known reviewer, ask for clarification and do not stop.

## Extending The Workflow

To add a new reviewer:

1. Add the role to `workflow/docs/TEAM.MD` if it does not already exist.
2. Append the new reviewer id to `workflow/agent/reviewer-registry.json` `index`.
3. Add the reviewer metadata under `workflow/agent/reviewer-registry.json` `reviewers`.
4. Add the reviewer id to `workflow/agent/reviewer-loop.json` if it should appear in the default loop or in a named loop.
5. Update this orchestrator only if the new reviewer changes the rules of execution rather than just the available catalog.

Do not hardcode one-off role logic into ticket files. Keep reviewer identity in the registry and ordered execution in the reviewer loop file.

## Good Defaults

- Prefer additive tickets.
- Keep ticket acceptance behavior-based.
- Split platform-risk work away from user-facing work when they can ship independently.
- Default to subagents for broad reviews, not for simple edits.
- If a safe default exists, proceed and record it instead of over-questioning the user.

## Completion Criteria

The orchestration is complete only when:

- every required output file exists under `workflow/`,
- the PRD has a dedicated workspace under `workflow/workspaces/<prd-slug>/`,
- the ticket list covers the full PRD scope,
- every ticket is a valid ExecPlan-shaped document,
- the backlog order is explicit,
- the number of tickets reflects the actual shape of the work rather than an artificial target,
- unresolved decisions are either answered or clearly called out as blockers,
- the reviewer loop has either been continued manually or explicitly ended by the user,
- `workflow/workspaces/<prd-slug>/done.md` exists because the user replied `DONE`.
