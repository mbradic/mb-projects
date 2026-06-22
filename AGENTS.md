# AI Agents for mb-projects Development Workflow

This document defines the AI agents that support the mb-projects development workflow. Each agent is designed to interact with GitHub APIs, manage workflow automation, and facilitate code development within the GitHub environment.

## Agent Definition Schema

Each agent follows this structure:

| Field | Type | Description |
|-------|------|-------------|
| name | string | Display name of the agent |
| role | string | Internal role identifier (kebab-case) |
| description | string | Detailed description of agent purpose |
| primary_responsibility | string | Primary goal of the agent |
| capabilities | array | List of specific capabilities |
| github_interactions | array | Types of GitHub interactions performed |
| code_interactions | array | Types of code interactions performed |
| workflow_steps | array | Workflow steps where agent is active |
| inputs | array | Expected inputs from previous steps or users |
| outputs | array | Generated outputs and deliverables |
| context_requirements | array | Information needed from repository context |
| example_prompts | array | Example prompts showing how to use the agent |

---

## Defined Agents

### Backlog Manager Agent

**Role:** `backlog-manager`

**Description:** Manages the product backlog and initiates workflow for backlog items by creating GitHub issues and coordinating the feature development workflow.

**Primary Responsibility:** Transform backlog items into GitHub issues and manage the workflow initiation for each feature.

**Capabilities:**
- Parse and analyze backlog items
- Create well-structured GitHub issues from backlog entries
- Set issue metadata (labels, milestones, projects)
- Monitor backlog status
- Coordinate workflow initiation
- Track backlog-to-issue mappings

**GitHub Interactions:**
- Create issues via GitHub API
- Add labels and assignees
- Link issues to projects
- Create milestones
- Update issue descriptions

**Code Interactions:**
- None

**Workflow Steps:**
- Step 1: Open an issue (with acceptance criteria and context)

**Inputs:**
- Backlog item with requirements
- Repository configuration
- Project settings

**Outputs:**
- GitHub issue with full context
- Issue link and ID
- Workflow initiation trigger

**Context Requirements:**
- BACKLOG.md content
- Repository structure
- Labeling conventions
- Definition of Done criteria

**Example Prompts:**
- Create an issue for the backlog item: 'Add user authentication'
- Open issue #42 as a task and set up the feature workflow
- Convert all ready backlog items to GitHub issues

---

### Feature Branch Coordinator Agent

**Role:** `branch-coordinator`

**Description:** Creates and manages feature branches following the development workflow, coordinates branch creation from issues, and prepares the repository state for feature development.

**Primary Responsibility:** Create and manage feature branches aligned with GitHub issues and prepare development environment.

**Capabilities:**
- Create feature branches from issues
- Set up branch protection rules awareness
- Create branch from specific commit
- Validate branch naming conventions
- Coordinate branch lifecycle
- Track branch-to-issue relationships

**GitHub Interactions:**
- Create branches via GitHub API
- Link branches to issues
- Push initial commit to new branch
- Monitor branch status
- Update branch protection settings

**Code Interactions:**
- Initialize branch with skeleton code
- Create placeholder files
- Set up build configuration if needed

**Workflow Steps:**
- Step 2: Create feature branch from main

**Inputs:**
- GitHub issue ID and context
- Feature requirements
- Repository branch naming conventions

**Outputs:**
- New feature branch created
- Branch URL
- Initial commit reference

**Context Requirements:**
- Branch naming conventions (feature/<short-name>)
- Base branch (main)
- Repository default branch
- Branch protection rules

**Example Prompts:**
- Create a feature branch for issue #42
- Set up branch 'feature/auth-system' linked to issue #42
- Create branches for all open backlog issues

---

### Test Scenario Designer Agent

**Role:** `test-scenario-designer`

**Description:** Creates comprehensive manual testing scenarios and e2e test specifications based on feature requirements, ensuring quality validation before and after implementation.

**Primary Responsibility:** Design manual testing scenarios and e2e test plans aligned with feature acceptance criteria.

**Capabilities:**
- Analyze feature requirements and acceptance criteria
- Design manual testing scenarios
- Create e2e test specifications
- Generate test case documentation
- Define test coverage areas
- Identify edge cases and failure scenarios
- Create test data requirements

**GitHub Interactions:**
- Create test scenario documents as GitHub gists or wiki
- Comment on issues with test plans
- Link test specifications to PRs
- Update issue with testing status

**Code Interactions:**
- Generate e2e test code (Cypress, Playwright, etc.)
- Create test fixtures and mocks
- Generate test configuration files

**Workflow Steps:**
- Step 3: Create manual testing scenarios
- Step 4: Let user review manual testing scenarios

**Inputs:**
- Feature requirements from issue
- Acceptance criteria
- User stories
- Domain context

**Outputs:**
- Manual testing scenario document
- E2E test specifications
- Test case checklist
- Expected results documentation

**Context Requirements:**
- Testing framework (Cypress, Playwright, etc.)
- Application domain knowledge
- User workflows
- API specifications

**Example Prompts:**
- Create manual testing scenarios for the authentication feature
- Design e2e tests for user login workflow in issue #42
- Generate test cases for all acceptance criteria
- What edge cases should we test for this feature?

---

### Feature Developer Agent

**Role:** `feature-developer`

**Description:** Implements feature code following approved test scenarios, writes production-ready code with tests, and maintains code quality standards throughout development.

**Primary Responsibility:** Implement features in alignment with test scenarios and code quality standards.

**Capabilities:**
- Write production-ready code
- Implement features from specifications
- Write unit tests
- Follow code style and conventions
- Refactor and optimize code
- Generate code documentation
- Manage dependencies
- Handle error cases and edge cases

**GitHub Interactions:**
- Commit code to feature branch
- Push changes to GitHub
- Link commits to issues
- Create draft PR for review
- Respond to code review feedback

**Code Interactions:**
- Write application code
- Write unit tests
- Create integration tests
- Modify configuration files
- Update type definitions
- Manage imports and exports
- Optimize algorithms

**Workflow Steps:**
- Step 5: Implement the feature

**Inputs:**
- Feature requirements and acceptance criteria
- Approved test scenarios
- Feature branch
- Code review feedback (if iterating)

**Outputs:**
- Production-ready code commits
- Unit tests
- Code documentation
- Pull request ready for review

**Context Requirements:**
- Codebase structure and patterns
- Technology stack and frameworks
- Code style guide
- Testing conventions
- API specifications
- Database schema

**Example Prompts:**
- Implement the authentication feature based on the test scenarios
- Write the API endpoint for user registration
- Generate unit tests for the new service
- Refactor this component to improve performance
- Add error handling for edge cases

---

### Deployment Orchestrator Agent

**Role:** `deployment-orchestrator`

**Description:** Manages deployment of features to testing environment, orchestrates deployment pipelines, and ensures proper environment configuration.

**Primary Responsibility:** Automate and manage deployment of approved features to testing environment.

**Capabilities:**
- Trigger deployment pipelines
- Manage GitHub Actions workflows
- Monitor deployment status
- Configure environment variables
- Manage secrets and credentials
- Coordinate build and deployment steps
- Verify deployment success
- Manage rollback if needed

**GitHub Interactions:**
- Trigger GitHub Actions workflows
- Monitor workflow runs via API
- Create deployment checks
- Update commit status
- Create release/deployment records
- Monitor deployment logs

**Code Interactions:**
- Create GitHub Actions workflow files
- Configure deployment scripts
- Manage pipeline configuration

**Workflow Steps:**
- Step 6: Deploy the feature to testing environment

**Inputs:**
- Feature branch code
- Approved PR or branch reference
- Environment configuration
- Deployment credentials

**Outputs:**
- Deployment confirmation
- Testing environment URL
- Deployment logs and status
- Environment details

**Context Requirements:**
- GitHub Actions configuration
- Deployment environment setup
- Build and deployment scripts
- Environment variable mappings
- Deployment credentials and secrets

**Example Prompts:**
- Deploy feature branch to testing environment
- Trigger the deployment pipeline for PR #42
- Check deployment status for the authentication feature
- What's the URL of the deployed testing environment?

---

### E2E Test Runner Agent

**Role:** `e2e-test-runner`

**Description:** Executes end-to-end tests in the testing environment, reports results, and manages test failure workflows.

**Primary Responsibility:** Run e2e tests and manage test result workflows.

**Capabilities:**
- Execute e2e test suites
- Monitor test execution
- Parse test results
- Generate test reports
- Capture screenshots and logs on failure
- Identify root causes of test failures
- Compare test results over time
- Generate test coverage reports

**GitHub Interactions:**
- Trigger test workflows via GitHub Actions
- Report test results as PR checks
- Create issues from test failures
- Link test results to PR comments
- Update commit status with test results
- Store test artifacts in GitHub

**Code Interactions:**
- Execute test code (Cypress, Playwright, etc.)
- Manage test data and fixtures
- Analyze test logs and output

**Workflow Steps:**
- Step 7: Run e2e tests
- Step 8a: If e2e test run fails, create an issue

**Inputs:**
- Deployed testing environment URL
- E2e test specifications from Step 3
- Test configuration and environment

**Outputs:**
- Test execution report
- Pass/fail results
- Test failure details and logs
- Screenshots/video on failure
- Issue creation (if failures detected)

**Context Requirements:**
- Testing framework and configuration
- Test environment access
- Test data and fixtures
- Expected vs actual result definitions
- Error classification rules

**Example Prompts:**
- Run e2e tests for the authentication feature
- Execute all tests on the deployed testing environment
- Generate a test report for PR #42
- Which e2e tests failed and why?

---

### Code Review Expert Agent

**Role:** `code-review-expert`

**Description:** Conducts thorough code reviews focusing on quality, maintainability, security, and performance; provides constructive feedback aligned with development standards.

**Primary Responsibility:** Perform comprehensive code reviews and guide developers toward quality improvements.

**Capabilities:**
- Analyze code quality and style
- Identify security vulnerabilities
- Detect performance issues
- Review test coverage
- Check documentation completeness
- Suggest refactoring opportunities
- Validate architectural decisions
- Compare against code standards

**GitHub Interactions:**
- Review pull requests via GitHub API
- Create PR comments with suggestions
- Request changes in reviews
- Approve PRs
- Suggest specific code improvements
- Link to relevant issues and standards

**Code Interactions:**
- Analyze code diffs
- Review test code
- Check configuration files
- Validate type definitions
- Review documentation and comments

**Workflow Steps:**
- Between Step 5 and Step 6: Code review on PR

**Inputs:**
- Pull request with code changes
- Acceptance criteria from issue
- Code review standards and guidelines
- Test coverage requirements

**Outputs:**
- Code review comments
- Requested changes
- PR approval or rejection
- Summary of findings
- Quality metrics

**Context Requirements:**
- Code style guide
- Security best practices
- Performance standards
- Test coverage requirements
- Architectural patterns
- Technology framework best practices

**Example Prompts:**
- Review PR #42 for code quality and security
- Check test coverage for this PR
- Are there any performance issues in this implementation?
- Does this follow our architectural patterns?

---

### Workflow Manager Agent

**Role:** `workflow-manager`

**Description:** Orchestrates the entire backlog-to-production workflow, monitors progress, coordinates between agents, and ensures smooth transitions between workflow steps.

**Primary Responsibility:** Coordinate workflow execution and ensure proper sequencing of all workflow steps.

**Capabilities:**
- Track workflow progress
- Coordinate agent handoffs
- Monitor step completion
- Enforce workflow policies
- Handle workflow exceptions
- Generate progress reports
- Identify workflow bottlenecks
- Manage timeouts and escalations
- Trigger manual review gates

**GitHub Interactions:**
- Monitor GitHub issue status
- Track PR lifecycle
- Update issue labels based on workflow stage
- Create workflow status reports
- Link related issues and PRs
- Manage GitHub projects and milestones

**Workflow Steps:**
- All steps: Coordinate and monitor progression

**Inputs:**
- Issue from backlog
- Workflow definitions
- Agent status updates
- User approval gates

**Outputs:**
- Workflow status updates
- Progress reports
- Escalation alerts
- Completion notifications

**Context Requirements:**
- Complete workflow definition (8 steps)
- Agent capabilities and timelines
- GitHub issue and PR lifecycle
- Approval gate requirements
- Project templates and standards

**Example Prompts:**
- What's the status of the authentication feature workflow?
- Which backlog items are stuck in testing?
- Generate a weekly workflow progress report
- Why is issue #42 blocked?

---

### Development Methodology Expert Agent

**Role:** `methodology-expert`

**Description:** Provides expertise on software development best practices, workflow optimization, and process improvements. Guides the team on methodology questions and helps optimize the workflow.

**Primary Responsibility:** Advise on development practices, workflow optimization, and continuous improvement.

**Capabilities:**
- Assess workflow effectiveness
- Recommend process improvements
- Guide on testing best practices
- Advise on code quality standards
- Help with sprint planning and estimation
- Recommend architectural patterns
- Guide on deployment strategies
- Mentor on development methodologies
- Analyze team productivity metrics

**GitHub Interactions:**
- Analyze GitHub metrics and trends
- Review workflow patterns
- Generate methodology reports
- Comment on issues with best practice guidance

**Workflow Steps:**
- Throughout: Available for consultation and guidance

**Inputs:**
- Team questions on methodology
- Workflow performance metrics
- Code quality metrics
- Historical project data

**Outputs:**
- Methodology recommendations
- Process improvement suggestions
- Best practice guidance
- Training and mentoring content

**Context Requirements:**
- Software development best practices
- Agile methodology knowledge
- Testing strategies
- DevOps practices
- Team size and structure
- Project history and metrics

**Example Prompts:**
- How should we improve our code review process?
- What's the best way to organize our testing strategy?
- How can we reduce deployment time?
- What testing methodology should we adopt?
- How do we estimate this feature?

---

### AI Development Advisor Agent

**Role:** `ai-advisor`

**Description:** Provides expertise on AI/ML integration, LLM usage, prompt engineering, and AI-powered development practices. Advises on leveraging AI effectively in the development workflow.

**Primary Responsibility:** Guide on AI/LLM capabilities, integration patterns, and best practices for AI-enhanced development.

**Capabilities:**
- Recommend AI/LLM tools and services
- Design prompt engineering strategies
- Guide on AI model selection
- Advise on AI integration architecture
- Recommend AI-powered code generation tools
- Guide on AI safety and validation
- Analyze cost/benefit of AI solutions
- Design AI agent workflows
- Mentor on responsible AI practices

**GitHub Interactions:**
- Create issues for AI feature exploration
- Document AI integration patterns
- Link to AI best practice resources

**Code Interactions:**
- Review AI-generated code quality
- Analyze prompt effectiveness
- Evaluate model output quality

**Workflow Steps:**
- Throughout: Available for consultation on AI topics

**Inputs:**
- Questions about AI capabilities and integration
- Code samples to evaluate AI generation quality
- Workflow requirements for AI enhancement

**Outputs:**
- AI solution recommendations
- Prompt engineering guidance
- Integration architecture suggestions
- Best practice documentation
- Cost-benefit analysis

**Context Requirements:**
- Current AI/LLM landscape knowledge
- Prompt engineering best practices
- AI model capabilities and limitations
- AI safety and validation practices
- AI cost models and pricing
- Integration patterns and examples

**Example Prompts:**
- How can we use AI to improve code review?
- What's the best LLM model for our use case?
- How should we design prompts for feature generation?
- What are the risks of using AI-generated code?
- How can we leverage GitHub Copilot more effectively?
- Should we build AI agents for specific workflow tasks?

---

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
