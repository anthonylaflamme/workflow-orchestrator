# Portable Workflow Package

This folder packages a PRD-to-ticket workflow into a transportable bundle. It was distilled from the recent planning and review chats in this repo, especially the repeated pattern of reading the planning rules first, using role-based reviews, asking all needed questions, and producing one ExecPlan per feature.

## What This Package Contains

- `workflow/agent/PLANS.MD`: an unchanged copy of the ExecPlan rules.
- `workflow/docs/TEAM.MD`: the reusable team-role library.
- `workflow/agent/MAIN-ORCHESTRATOR.md`: the main prompt/instructions for turning a PRD into a reviewed ticket backlog.
- `workflow/agent/reviewer-registry.json`: the full reviewer catalog, aliases, and metadata for all available roles.
- `workflow/agent/reviewer-loop.json`: the ordered default and named reviewer loops.
- `workflow/agent/QUESTION-POLICY.md`: rules for when and how to pause for user decisions.
- `workflow/workspaces/`: one mutable workspace per PRD.

## Default Usage

1. Put or identify the PRD somewhere in the repo.
2. Point the agent at `workflow/agent/MAIN-ORCHESTRATOR.md`.
3. Give it the PRD path
4. Let the orchestrator scaffold or reopen `workflow/workspaces/<prd-slug>/`.
5. Answer the structured decision checkpoints the orchestrator raises. It may ask as many rounds of questions as needed to shape the backlog correctly.
6. Review the generated `workflow/workspaces/<prd-slug>/TICKET-INDEX.md`, `DECISIONS.md`, and per-ticket ExecPlans.
7. Each reviewer in the loop should revise until stable or blocked for their lens, not just perform a single shallow pass.
8. At the end of the default review loop, answer the final reviewer prompt with either `DONE` or the next reviewer id to run.

There is no fixed cap on ticket count. The workflow should create however many tickets the PRD actually requires.

## Example Prompt

Copy this prompt, paste it into the agent, and replace the PRD block with your own product requirements document.

```md
Use `workflow/agent/MAIN-ORCHESTRATOR.md` with <prd-path> as the source of truth for this run.
```

## Per-PRD Workspaces

Each PRD gets its own isolated workspace so multiple contributors can plan in parallel without overlapping on the same ticket index or decision log.

A typical workspace looks like:

- `workflow/workspaces/<prd-slug>/PRD.md` or `PRD-REFERENCE.md`
- `workflow/workspaces/<prd-slug>/TICKET-INDEX.md`
- `workflow/workspaces/<prd-slug>/DECISIONS.md`
- `workflow/workspaces/<prd-slug>/REVIEW-HISTORY.md`
- `workflow/workspaces/<prd-slug>/done.md`
- `workflow/workspaces/<prd-slug>/tickets/*.md`

## Extending The Workflow

To add a new reviewer, add the role to `workflow/docs/TEAM.MD` if needed, register it in `workflow/agent/reviewer-registry.json`, and then add it to `workflow/agent/reviewer-loop.json` if it should appear in the default or a named loop.

## Portability

This package is designed to stay self-contained under `workflow/`. You can move the folder to another repo and keep using the same relative paths inside it without touching that repo's root planning files.
