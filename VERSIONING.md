# Versioning Strategy

This document defines the general versioning approach for `mb-projects`.

## Principles

- Use one clear versioning scheme for released work.
- Treat planning metadata separately from released versions.
- Keep document history in Git instead of assigning semantic versions to individual markdown files.

## Release Versioning

Released work uses semantic versioning with tags in the format `vMAJOR.MINOR.PATCH`.

- **MAJOR**: Breaking changes to released behavior, public interfaces, or established workflow expectations.
- **MINOR**: Backward-compatible features, capabilities, or meaningful workflow additions.
- **PATCH**: Backward-compatible fixes, clarifications, and small improvements.

Git tags and GitHub releases are the source of truth for published versions.

## Planning and Backlog Versioning

Backlog items should use a **Target Release** or milestone to show when work is expected to ship.

- A target release is a planning value, not a released version.
- Target releases may change as priorities or scope change.
- Individual backlog entries should not imply that the backlog document itself has its own semantic version.

## Documentation Versioning

Repository documents such as `README.md`, `BACKLOG.md`, `AGENTS.md`, and `WORKFLOW.md` are not versioned independently.

- Git history tracks document changes.
- Optional `Last Updated` metadata can show recency.
- Documentation changes contribute to release notes only when they affect released behavior, process expectations, or public usage.

## Future Extension

If the repository later contains multiple releasable components, the default should remain a single repository release version unless a component explicitly needs its own documented lifecycle.
