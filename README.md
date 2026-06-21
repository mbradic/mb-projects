# mb-projects

My personal app for my projects

## Product Backlog

See [`BACKLOG.md`](./BACKLOG.md) for the current product backlog and versioning strategy. The backlog is maintained separately to enable frequent updates without changing the README.

## Agents

See [`AGENTS.md`](./AGENTS.md) for the current list of agents and their responsibilities.

## Development Workflow

```
main
  └─ feature/<area>      ← one branch per backlog item
       └─ PR → review → merge into main
```

1. **Issue-first** — every piece of work starts as a GitHub Issue linked to a backlog item.
2. **Branch** — create a feature branch (`feature/<short-name>`) from `main`.
3. **Local development** — build and run the app locally; write or update tests alongside code changes.
4. **Pull request** — open a draft PR early; use Copilot agents (project-manager, planning) to review scope and flag gaps.
5. **CI checks** — automated linting, unit tests, and integration tests must pass before review.
6. **Code review** — at least one human review; the reporting agent produces a change summary for context.
7. **Merge** — squash-merge into `main`; the project-manager agent closes the linked issue and updates the dashboard.
8. **Release** — tag `main` with a semantic version; the import/export agent archives a snapshot of project data.

## Versioning Strategy

The README and BACKLOG.md are versioned independently:

- **README.md**: Documents the overall project vision, agents, and workflows. Uses semantic versioning (MAJOR.MINOR.PATCH) for significant structural changes to documentation. Updates to this file typ[...]
- **BACKLOG.md**: Maintains the product backlog and can be updated frequently without triggering a version bump to the README. Uses its own semantic versioning scheme to track backlog changes.
