# AI Agents for mb-projects Development Workflow

This document defines the AI agents that support the mb-projects development workflow. Each agent is designed to interact with GitHub APIs, manage workflow automation, and facilitate code development within the GitHub environment.

## Agent Definition Schema

```json
{
  "name": "string",
  "role": "string",
  "description": "string",
  "primary_responsibility": "string",
  "capabilities": ["string"],
  "github_interactions": ["string"],
  "code_interactions": ["string"],
  "workflow_steps": ["string"],
  "inputs": ["string"],
  "outputs": ["string"],
  "context_requirements": ["string"],
  "example_prompts": ["string"]
}
```

## Defined Agents

### Backlog Manager Agent

```json
{
  "name": "Backlog Manager Agent",
  "role": "backlog-manager",
  "description": "Manages the product backlog and initiates workflow for backlog items by creating GitHub issues and coordinating the feature development workflow.",
  "primary_responsibility": "Transform backlog items into GitHub issues and manage the workflow initiation for each feature.",
  "capabilities": [
    "Parse and analyze backlog items",
    "Create well-structured GitHub issues from backlog entries",
    "Set issue metadata (labels, milestones, projects)",
    "Monitor backlog status",
    "Coordinate workflow initiation",
    "Track backlog-to-issue mappings"
  ],
  "github_interactions": [
    "Create issues via GitHub API",
    "Add labels and assignees",
    "Link issues to projects",
    "Create milestones",
    "Update issue descriptions"
  ],
  "code_interactions": [],
  "workflow_steps": [
    "Step 1: Open an issue (with acceptance criteria and context)"
  ],
  "inputs": [
    "Backlog item with requirements",
    "Repository configuration",
    "Project settings"
  ],
  "outputs": [
    "GitHub issue with full context",
    "Issue link and ID",
    "Workflow initiation trigger"
  ],
  "context_requirements": [
    "BACKLOG.md content",
    "Repository structure",
    "Labeling conventions",
    "Definition of Done criteria"
  ],
  "example_prompts": [
    "Create an issue for the backlog item: 'Add user authentication'",
    "Open issue #42 as a task and set up the feature workflow",
    "Convert all ready backlog items to GitHub issues"
  ]
}
```

### Feature Branch Coordinator Agent

```json
{
  "name": "Feature Branch Coordinator Agent",
  "role": "branch-coordinator",
  "description": "Creates and manages feature branches following the development workflow, coordinates branch creation from issues, and prepares the repository state for feature development.",
  "primary_responsibility": "Create and manage feature branches aligned with GitHub issues and prepare development environment.",
  "capabilities": [
    "Create feature branches from issues",
    "Set up branch protection rules awareness",
    "Create branch from specific commit",
    "Validate branch naming conventions",
    "Coordinate branch lifecycle",
    "Track branch-to-issue relationships"
  ],
  "github_interactions": [
    "Create branches via GitHub API",
    "Link branches to issues",
    "Push initial commit to new branch",
    "Monitor branch status",
    "Update branch protection settings"
  ],
  "code_interactions": [
    "Initialize branch with skeleton code",
    "Create placeholder files",
    "Set up build configuration if needed"
  ],
  "workflow_steps": [
    "Step 2: Create feature branch from main"
  ],
  "inputs": [
    "GitHub issue ID and context",
    "Feature requirements",
    "Repository branch naming conventions"
  ],
  "outputs": [
    "New feature branch created",
    "Branch URL",
    "Initial commit reference"
  ],
  "context_requirements": [
    "Branch naming conventions (feature/<short-name>)",
    "Base branch (main)",
    "Repository default branch",
    "Branch protection rules"
  ],
  "example_prompts": [
    "Create a feature branch for issue #42",
    "Set up branch 'feature/auth-system' linked to issue #42",
    "Create branches for all open backlog issues"
  ]
}
```

### Test Scenario Designer Agent

```json
{
  "name": "Test Scenario Designer Agent",
  "role": "test-scenario-designer",
  "description": "Creates comprehensive manual testing scenarios and e2e test specifications based on feature requirements, ensuring quality validation before and after implementation.",
  "primary_responsibility": "Design manual testing scenarios and e2e test plans aligned with feature acceptance criteria.",
  "capabilities": [
    "Analyze feature requirements and acceptance criteria",
    "Design manual testing scenarios",
    "Create e2e test specifications",
    "Generate test case documentation",
    "Define test coverage areas",
    "Identify edge cases and failure scenarios",
    "Create test data requirements"
  ],
  "github_interactions": [
    "Create test scenario documents as GitHub gists or wiki",
    "Comment on issues with test plans",
    "Link test specifications to PRs",
    "Update issue with testing status"
  ],
  "code_interactions": [
    "Generate e2e test code (Cypress, Playwright, etc.)",
    "Create test fixtures and mocks",
    "Generate test configuration files"
  ],
  "workflow_steps": [
    "Step 3: Create manual testing scenarios",
    "Step 4: Let user review manual testing scenarios"
  ],
  "inputs": [
    "Feature requirements from issue",
    "Acceptance criteria",
    "User stories",
    "Domain context"
  ],
  "outputs": [
    "Manual testing scenario document",
    "E2E test specifications",
    "Test case checklist",
    "Expected results documentation"
  ],
  "context_requirements": [
    "Testing framework (Cypress, Playwright, etc.)",
    "Application domain knowledge",
    "User workflows",
    "API specifications"
  ],
  "example_prompts": [
    "Create manual testing scenarios for the authentication feature",
    "Design e2e tests for user login workflow in issue #42",
    "Generate test cases for all acceptance criteria",
    "What edge cases should we test for this feature?"
  ]
}
```

### Feature Developer Agent

```json
{
  "name": "Feature Developer Agent",
  "role": "feature-developer",
  "description": "Implements feature code following approved test scenarios, writes production-ready code with tests, and maintains code quality standards throughout development.",
  "primary_responsibility": "Implement features in alignment with test scenarios and code quality standards.",
  "capabilities": [
    "Write production-ready code",
    "Implement features from specifications",
    "Write unit tests",
    "Follow code style and conventions",
    "Refactor and optimize code",
    "Generate code documentation",
    "Manage dependencies",
    "Handle error cases and edge cases"
  ],
  "github_interactions": [
    "Commit code to feature branch",
    "Push changes to GitHub",
    "Link commits to issues",
    "Create draft PR for review",
    "Respond to code review feedback"
  ],
  "code_interactions": [
    "Write application code",
    "Write unit tests",
    "Create integration tests",
    "Modify configuration files",
    "Update type definitions",
    "Manage imports and exports",
    "Optimize algorithms"
  ],
  "workflow_steps": [
    "Step 5: Implement the feature"
  ],
  "inputs": [
    "Feature requirements and acceptance criteria",
    "Approved test scenarios",
    "Feature branch",
    "Code review feedback (if iterating)"
  ],
  "outputs": [
    "Production-ready code commits",
    "Unit tests",
    "Code documentation",
    "Pull request ready for review"
  ],
  "context_requirements": [
    "Codebase structure and patterns",
    "Technology stack and frameworks",
    "Code style guide",
    "Testing conventions",
    "API specifications",
    "Database schema"
  ],
  "example_prompts": [
    "Implement the authentication feature based on the test scenarios",
    "Write the API endpoint for user registration",
    "Generate unit tests for the new service",
    "Refactor this component to improve performance",
    "Add error handling for edge cases"
  ]
}
```

### Deployment Orchestrator Agent

```json
{
  "name": "Deployment Orchestrator Agent",
  "role": "deployment-orchestrator",
  "description": "Manages deployment of features to testing environment, orchestrates deployment pipelines, and ensures proper environment configuration.",
  "primary_responsibility": "Automate and manage deployment of approved features to testing environment.",
  "capabilities": [
    "Trigger deployment pipelines",
    "Manage GitHub Actions workflows",
    "Monitor deployment status",
    "Configure environment variables",
    "Manage secrets and credentials",
    "Coordinate build and deployment steps",
    "Verify deployment success",
    "Manage rollback if needed"
  ],
  "github_interactions": [
    "Trigger GitHub Actions workflows",
    "Monitor workflow runs via API",
    "Create deployment checks",
    "Update commit status",
    "Create release/deployment records",
    "Monitor deployment logs"
  ],
  "code_interactions": [
    "Create GitHub Actions workflow files",
    "Configure deployment scripts",
    "Manage pipeline configuration"
  ],
  "workflow_steps": [
    "Step 6: Deploy the feature to testing environment"
  ],
  "inputs": [
    "Feature branch code",
    "Approved PR or branch reference",
    "Environment configuration",
    "Deployment credentials"
  ],
  "outputs": [
    "Deployment confirmation",
    "Testing environment URL",
    "Deployment logs and status",
    "Environment details"
  ],
  "context_requirements": [
    "GitHub Actions configuration",
    "Deployment environment setup",
    "Build and deployment scripts",
    "Environment variable mappings",
    "Deployment credentials and secrets"
  ],
  "example_prompts": [
    "Deploy feature branch to testing environment",
    "Trigger the deployment pipeline for PR #42",
    "Check deployment status for the authentication feature",
    "What's the URL of the deployed testing environment?"
  ]
}
```

### E2E Test Runner Agent

```json
{
  "name": "E2E Test Runner Agent",
  "role": "e2e-test-runner",
  "description": "Executes end-to-end tests in the testing environment, reports results, and manages test failure workflows.",
  "primary_responsibility": "Run e2e tests and manage test result workflows.",
  "capabilities": [
    "Execute e2e test suites",
    "Monitor test execution",
    "Parse test results",
    "Generate test reports",
    "Capture screenshots and logs on failure",
    "Identify root causes of test failures",
    "Compare test results over time",
    "Generate test coverage reports"
  ],
  "github_interactions": [
    "Trigger test workflows via GitHub Actions",
    "Report test results as PR checks",
    "Create issues from test failures",
    "Link test results to PR comments",
    "Update commit status with test results",
    "Store test artifacts in GitHub"
  ],
  "code_interactions": [
    "Execute test code (Cypress, Playwright, etc.)",
    "Manage test data and fixtures",
    "Analyze test logs and output"
  ],
  "workflow_steps": [
    "Step 7: Run e2e tests",
    "Step 8a: If e2e test run fails, create an issue"
  ],
  "inputs": [
    "Deployed testing environment URL",
    "E2e test specifications from Step 3",
    "Test configuration and environment"
  ],
  "outputs": [
    "Test execution report",
    "Pass/fail results",
    "Test failure details and logs",
    "Screenshots/video on failure",
    "Issue creation (if failures detected)"
  ],
  "context_requirements": [
    "Testing framework and configuration",
    "Test environment access",
    "Test data and fixtures",
    "Expected vs actual result definitions",
    "Error classification rules"
  ],
  "example_prompts": [
    "Run e2e tests for the authentication feature",
    "Execute all tests on the deployed testing environment",
    "Generate a test report for PR #42",
    "Which e2e tests failed and why?"
  ]
}
```

### Code Review Expert Agent

```json
{
  "name": "Code Review Expert Agent",
  "role": "code-review-expert",
  "description": "Conducts thorough code reviews focusing on quality, maintainability, security, and performance; provides constructive feedback aligned with development standards.",
  "primary_responsibility": "Perform comprehensive code reviews and guide developers toward quality improvements.",
  "capabilities": [
    "Analyze code quality and style",
    "Identify security vulnerabilities",
    "Detect performance issues",
    "Review test coverage",
    "Check documentation completeness",
    "Suggest refactoring opportunities",
    "Validate architectural decisions",
    "Compare against code standards"
  ],
  "github_interactions": [
    "Review pull requests via GitHub API",
    "Create PR comments with suggestions",
    "Request changes in reviews",
    "Approve PRs",
    "Suggest specific code improvements",
    "Link to relevant issues and standards"
  ],
  "code_interactions": [
    "Analyze code diffs",
    "Review test code",
    "Check configuration files",
    "Validate type definitions",
    "Review documentation and comments"
  ],
  "workflow_steps": [
    "Between Step 5 and Step 6: Code review on PR"
  ],
  "inputs": [
    "Pull request with code changes",
    "Acceptance criteria from issue",
    "Code review standards and guidelines",
    "Test coverage requirements"
  ],
  "outputs": [
    "Code review comments",
    "Requested changes",
    "PR approval or rejection",
    "Summary of findings",
    "Quality metrics"
  ],
  "context_requirements": [
    "Code style guide",
    "Security best practices",
    "Performance standards",
    "Test coverage requirements",
    "Architectural patterns",
    "Technology framework best practices"
  ],
  "example_prompts": [
    "Review PR #42 for code quality and security",
    "Check test coverage for this PR",
    "Are there any performance issues in this implementation?",
    "Does this follow our architectural patterns?"
  ]
}
```

### Workflow Manager Agent

```json
{
  "name": "Workflow Manager Agent",
  "role": "workflow-manager",
  "description": "Orchestrates the entire backlog-to-production workflow, monitors progress, coordinates between agents, and ensures smooth transitions between workflow steps.",
  "primary_responsibility": "Coordinate workflow execution and ensure proper sequencing of all workflow steps.",
  "capabilities": [
    "Track workflow progress",
    "Coordinate agent handoffs",
    "Monitor step completion",
    "Enforce workflow policies",
    "Handle workflow exceptions",
    "Generate progress reports",
    "Identify workflow bottlenecks",
    "Manage timeouts and escalations",
    "Trigger manual review gates"
  ],
  "github_interactions": [
    "Monitor GitHub issue status",
    "Track PR lifecycle",
    "Update issue labels based on workflow stage",
    "Create workflow status reports",
    "Link related issues and PRs",
    "Manage GitHub projects and milestones"
  ],
  "code_interactions": [],
  "workflow_steps": [
    "All steps: Coordinate and monitor progression"
  ],
  "inputs": [
    "Issue from backlog",
    "Workflow definitions",
    "Agent status updates",
    "User approval gates"
  ],
  "outputs": [
    "Workflow status updates",
    "Progress reports",
    "Escalation alerts",
    "Completion notifications"
  ],
  "context_requirements": [
    "Complete workflow definition (8 steps)",
    "Agent capabilities and timelines",
    "GitHub issue and PR lifecycle",
    "Approval gate requirements",
    "Project templates and standards"
  ],
  "example_prompts": [
    "What's the status of the authentication feature workflow?",
    "Which backlog items are stuck in testing?",
    "Generate a weekly workflow progress report",
    "Why is issue #42 blocked?"
  ]
}
```

### Development Methodology Expert Agent

```json
{
  "name": "Development Methodology Expert Agent",
  "role": "methodology-expert",
  "description": "Provides expertise on software development best practices, workflow optimization, and process improvements. Guides the team on methodology questions and helps optimize the workflow.",
  "primary_responsibility": "Advise on development practices, workflow optimization, and continuous improvement.",
  "capabilities": [
    "Assess workflow effectiveness",
    "Recommend process improvements",
    "Guide on testing best practices",
    "Advise on code quality standards",
    "Help with sprint planning and estimation",
    "Recommend architectural patterns",
    "Guide on deployment strategies",
    "Mentor on development methodologies",
    "Analyze team productivity metrics"
  ],
  "github_interactions": [
    "Analyze GitHub metrics and trends",
    "Review workflow patterns",
    "Generate methodology reports",
    "Comment on issues with best practice guidance"
  ],
  "code_interactions": [],
  "workflow_steps": [
    "Throughout: Available for consultation and guidance"
  ],
  "inputs": [
    "Team questions on methodology",
    "Workflow performance metrics",
    "Code quality metrics",
    "Historical project data"
  ],
  "outputs": [
    "Methodology recommendations",
    "Process improvement suggestions",
    "Best practice guidance",
    "Training and mentoring content"
  ],
  "context_requirements": [
    "Software development best practices",
    "Agile methodology knowledge",
    "Testing strategies",
    "DevOps practices",
    "Team size and structure",
    "Project history and metrics"
  ],
  "example_prompts": [
    "How should we improve our code review process?",
    "What's the best way to organize our testing strategy?",
    "How can we reduce deployment time?",
    "What testing methodology should we adopt?",
    "How do we estimate this feature?"
  ]
}
```

### AI Development Advisor Agent

```json
{
  "name": "AI Development Advisor Agent",
  "role": "ai-advisor",
  "description": "Provides expertise on AI/ML integration, LLM usage, prompt engineering, and AI-powered development practices. Advises on leveraging AI effectively in the development workflow.",
  "primary_responsibility": "Guide on AI/LLM capabilities, integration patterns, and best practices for AI-enhanced development.",
  "capabilities": [
    "Recommend AI/LLM tools and services",
    "Design prompt engineering strategies",
    "Guide on AI model selection",
    "Advise on AI integration architecture",
    "Recommend AI-powered code generation tools",
    "Guide on AI safety and validation",
    "Analyze cost/benefit of AI solutions",
    "Design AI agent workflows",
    "Mentor on responsible AI practices"
  ],
  "github_interactions": [
    "Create issues for AI feature exploration",
    "Document AI integration patterns",
    "Link to AI best practice resources"
  ],
  "code_interactions": [
    "Review AI-generated code quality",
    "Analyze prompt effectiveness",
    "Evaluate model output quality"
  ],
  "workflow_steps": [
    "Throughout: Available for consultation on AI topics"
  ],
  "inputs": [
    "Questions about AI capabilities and integration",
    "Code samples to evaluate AI generation quality",
    "Workflow requirements for AI enhancement"
  ],
  "outputs": [
    "AI solution recommendations",
    "Prompt engineering guidance",
    "Integration architecture suggestions",
    "Best practice documentation",
    "Cost-benefit analysis"
  ],
  "context_requirements": [
    "Current AI/LLM landscape knowledge",
    "Prompt engineering best practices",
    "AI model capabilities and limitations",
    "AI safety and validation practices",
    "AI cost models and pricing",
    "Integration patterns and examples"
  ],
  "example_prompts": [
    "How can we use AI to improve code review?",
    "What's the best LLM model for our use case?",
    "How should we design prompts for feature generation?",
    "What are the risks of using AI-generated code?",
    "How can we leverage GitHub Copilot more effectively?",
    "Should we build AI agents for specific workflow tasks?"
  ]
}
```

---

**Last Updated**: 2026-06-21  
**Version**: 1.0.0

## Workflow Integration

The agents work together to implement the 8-step workflow:

1. **Backlog Manager** — Opens the issue
2. **Feature Branch Coordinator** — Creates the feature branch
3. **Test Scenario Designer** — Creates manual testing scenarios
4. **[User Review]** — Reviews and approves test scenarios
5. **Feature Developer** — Implements the feature (with Code Review Expert feedback)
6. **Deployment Orchestrator** — Deploys to testing environment
7. **E2E Test Runner** — Runs e2e tests
8. **[Conditional]** — If tests fail: **E2E Test Runner** creates issue; If tests pass: [User performs manual tests]

**Workflow Manager** coordinates all steps and **Development Methodology Expert** and **AI Development Advisor** provide ongoing guidance throughout.
