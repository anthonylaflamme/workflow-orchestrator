# PRD Workspaces

This folder contains one mutable workspace per PRD.

Use the slugged structure:

- `workflow/workspaces/<prd-slug>/`

Each workspace should contain:

- `PRD.md` or `PRD-REFERENCE.md`
- `TICKET-INDEX.md`
- `DECISIONS.md`
- `REVIEW-HISTORY.md`
- `done.md`
- `tickets/`

The shared workflow core stays outside this folder under:

- `workflow/agent/`
- `workflow/docs/`

This separation lets multiple contributors plan different PRDs at the same time without overlapping on the same ticket index, decision log, or generated ticket files.

The orchestrator should keep asking whether to continue the reviewer loop until the user explicitly answers `DONE`. When that happens, it should write a timestamped `done.md` in the PRD workspace.
