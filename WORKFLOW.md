# Development Workflow

## Git Branching Strategy

```
main
  └─ feature/<short-name>      ← one branch per backlog item
       └─ PR → review → merge into main
```

## Workflow Steps

1. **Issue-first** — every piece of work starts as a GitHub Issue linked to a backlog item.
2. **Branch** — create a feature branch (`feature/<short-name>`) from `main`.
3. **Local development** — build and run the app locally; write or update tests alongside code changes.
4. **Pull request** — open a draft PR early; use Copilot agents (e.g., `workflow-manager`, `methodology-expert`) to review scope and flag gaps.
5. **CI checks** — automated linting, unit tests, and integration tests must pass before review.
6. **Code review** — at least one human review; the `code-review-expert` agent can produce a change summary for context.
7. **Merge** — squash-merge into `main`; close the linked issue and update workflow status (the `workflow-manager` agent can help coordinate this).
8. **Release** — tag `main` with a semantic version; the `deployment-orchestrator` agent can create release/deployment records.
