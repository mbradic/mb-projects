# Versioning Strategy

The mb-projects repository uses independent versioning for different documentation components to enable flexible updates without unnecessary version bumps across all files.

## Version Scheme

All versioned components use [semantic versioning (MAJOR.MINOR.PATCH)](https://semver.org):

- **MAJOR** (v[X].0.0): Breaking changes or significant restructuring
- **MINOR** (v0.[X].0): New features or significant additions
- **PATCH** (v0.0.[X]): Bug fixes, clarifications, or minor updates

**Example:** `v1.2.3`

## Component Versioning

### README.md

- **Purpose:** Documents the overall project vision, agents, and workflows
- **Update Frequency:** Low - only when project structure changes significantly
- **Versioning:** Uses semantic versioning for significant structural changes to documentation
- **Triggers Version Bump:** 
  - Major restructuring of sections
  - Changes to main project description
  - New core documentation structure

### BACKLOG.md

- **Purpose:** Maintains the product backlog with prioritized features and tasks
- **Update Frequency:** High - updated frequently as backlog items progress
- **Versioning:** Uses independent semantic versioning to track backlog changes
- **Triggers Version Bump:**
  - Significant changes to milestone structure
  - Major backlog reorganization
  - Completion of major features

### Workflow Documentation (WORKFLOW.md)

- **Purpose:** Documents development workflow, branching strategy, and process steps
- **Update Frequency:** Medium - updated when workflow changes
- **Versioning:** Uses independent semantic versioning
- **Triggers Version Bump:**
  - Changes to workflow steps
  - New process definitions
  - Updates to branching strategy

### Agents Documentation (AGENTS.md)

- **Purpose:** Lists all agents and their responsibilities
- **Update Frequency:** Medium - updated when agents are added/removed
- **Versioning:** Uses independent semantic versioning
- **Triggers Version Bump:**
  - New agents added
  - Agent responsibilities changed
  - Major agent refactoring

## Release Tags

Release tags follow semantic versioning format:

- Format: `v[MAJOR].[MINOR].[PATCH]`
- Type: Annotated git tags with release notes
- Example: `v1.2.3`

## Release Process

When creating a release:

1. Update all relevant documentation files
2. Create a git tag with semantic version: `git tag -a v1.2.3 -m "Release v1.2.3"`
3. Push tags to repository: `git push origin --tags`
4. Create release notes with summary of changes

## Last Updated

See individual file headers for last update timestamps.
