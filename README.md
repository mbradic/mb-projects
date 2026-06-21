# mb-projects
My personal app for my projects

## Proposed product backlog

Based on the repository description, this app should help manage and track personal projects.

1. **Project dashboard** — view all projects with status, priority, and recent activity.
2. **Project detail pages** — store goals, notes, milestones, and links for each project.
3. **Task tracking** — create and organize tasks, due dates, and progress per project.
4. **Timeline and milestones** — plan upcoming work and highlight overdue items.
5. **Search and filtering** — quickly find projects and tasks by name, status, or tag.
6. **Notifications and reminders** — surface upcoming deadlines and stalled projects.
7. **Reporting** — summarize project progress, completed work, and next actions.
8. **Data import/export** — back up project data and move it between tools if needed.

## Proposed agents

| Agent | Responsibility |
|---|---|
| **Project manager agent** | Interprets natural-language instructions to create, update, or close projects and tasks; keeps status and priority fields consistent. |
| **Reminder & deadline agent** | Monitors due dates across all projects, fires notifications for upcoming or overdue items, and escalates stalled work. |
| **Planning agent** | Breaks high-level goals into tasks, suggests realistic timelines, and identifies scheduling conflicts on the timeline. |
| **Reporting agent** | Generates summaries of completed work, velocity, and next actions on demand or on a scheduled cadence. |
| **Search & context agent** | Answers natural-language queries about projects and tasks by combining full-text search with embedded project context. |
| **Import/export agent** | Handles structured data ingestion (CSV, JSON, Markdown) and exports data to external tools or backups. |

## Proposed development workflow

```
main
  └─ feature/<area>      ← one branch per backlog item
       └─ PR → review → merge into main
```

1. **Issue-first** — every piece of work starts as a GitHub Issue linked to a backlog item above.
2. **Branch** — create a feature branch (`feature/<short-name>`) from `main`.
3. **Local development** — build and run the app locally; write or update tests alongside code changes.
4. **Pull request** — open a draft PR early; use Copilot agents (project-manager, planning) to review scope and flag gaps.
5. **CI checks** — automated linting, unit tests, and integration tests must pass before review.
6. **Code review** — at least one human review; the reporting agent produces a change summary for context.
7. **Merge** — squash-merge into `main`; the project-manager agent closes the linked issue and updates the dashboard.
8. **Release** — tag `main` with a semantic version; the import/export agent archives a snapshot of project data.
