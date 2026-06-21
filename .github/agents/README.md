# AI Agents Configuration

This directory contains configuration files for the AI agents that power the mb-projects development workflow. Each agent is defined according to the schema and supports the 8-step feature development lifecycle.

## Overview

The agent system implements an automated workflow for feature development, from backlog items through to testing and deployment. The agents coordinate to provide:

- **Automated backlog-to-code** workflow
- **Continuous integration** with GitHub
- **Quality assurance** through testing and code review
- **Deployment orchestration** and monitoring
- **Guidance and expertise** on development best practices

## Agent Definitions

All agent configurations are stored as individual JSON files following the unified schema defined in `../../../AGENTS.md`.

### Core Agents (Workflow Execution)

1. **Backlog Manager** (`01-backlog-manager.json`)
   - Role: `backlog-manager`
   - Step: Step 1
   - Responsibility: Opens issues from backlog items

2. **Feature Branch Coordinator** (`02-branch-coordinator.json`)
   - Role: `branch-coordinator`
   - Step: Step 2
   - Responsibility: Creates feature branches

3. **Test Scenario Designer** (`03-test-scenario-designer.json`)
   - Role: `test-scenario-designer`
   - Steps: Step 3-4
   - Responsibility: Designs test scenarios

4. **Feature Developer** (`04-feature-developer.json`)
   - Role: `feature-developer`
   - Step: Step 5
   - Responsibility: Implements features

5. **Deployment Orchestrator** (`05-deployment-orchestrator.json`)
   - Role: `deployment-orchestrator`
   - Step: Step 6
   - Responsibility: Deploys to testing environment

6. **E2E Test Runner** (`06-e2e-test-runner.json`)
   - Role: `e2e-test-runner`
   - Steps: Step 7-8
   - Responsibility: Runs end-to-end tests

### Quality & Review Agents

7. **Code Review Expert** (`07-code-review-expert.json`)
   - Role: `code-review-expert`
   - Step: Between Step 5 and Step 6
   - Responsibility: Reviews code changes

### Orchestration & Guidance Agents

8. **Workflow Manager** (`08-workflow-manager.json`)
   - Role: `workflow-manager`
   - Steps: All steps
   - Responsibility: Coordinates workflow execution

9. **Development Methodology Expert** (`09-methodology-expert.json`)
   - Role: `methodology-expert`
   - Available: Throughout
   - Responsibility: Provides development best practices guidance

10. **AI Development Advisor** (`10-ai-advisor.json`)
    - Role: `ai-advisor`
    - Available: Throughout
    - Responsibility: Advises on AI/ML integration

## Agent Configuration Schema

Each agent configuration file follows this JSON schema:

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

### Field Descriptions

- **name**: Display name of the agent
- **role**: Internal role identifier (kebab-case)
- **description**: Detailed description of agent purpose
- **primary_responsibility**: Primary goal of the agent
- **capabilities**: List of specific capabilities
- **github_interactions**: Types of GitHub interactions performed
- **code_interactions**: Types of code interactions performed
- **workflow_steps**: Workflow steps where agent is active
- **inputs**: Expected inputs from previous steps or users
- **outputs**: Generated outputs and deliverables
- **context_requirements**: Information needed from repository context
- **example_prompts**: Example prompts showing how to use the agent

## Registry File

The `registry.json` file provides a central index of all agents with quick reference information:

- Agent listing with metadata
- Workflow definition showing the 8-step process
- Supporting agents information
- Metadata about the agent system

## Usage

### Loading Agent Configurations

Agents can be instantiated from the JSON files:

```bash
# Load a specific agent
jq '.' .github/agents/01-backlog-manager.json

# List all agents
jq '.agents[] | {name, role}' .github/agents/registry.json
```

### Integration with GitHub

Agents interact with GitHub through:

- **GitHub API**: Creating issues, managing PRs, updating branches
- **GitHub Actions**: Automating workflows and deployments
- **GitHub Projects**: Tracking workflow progress and status

### Workflow Coordination

The Workflow Manager Agent coordinates the execution of the 8-step workflow:

1. **Step 1**: Backlog Manager opens issue
2. **Step 2**: Branch Coordinator creates feature branch
3. **Step 3-4**: Test Scenario Designer creates test scenarios (with user review)
4. **Step 5**: Feature Developer implements code (with Code Review Expert)
5. **Step 6**: Deployment Orchestrator deploys to testing
6. **Step 7-8**: E2E Test Runner executes tests

Throughout this workflow:
- **Workflow Manager** monitors progress and coordinates handoffs
- **Development Methodology Expert** provides guidance on best practices
- **AI Development Advisor** advises on AI/ML capabilities

## Extending the Agent System

To add new agents:

1. Define the agent following the schema in `../../../AGENTS.md`
2. Create a new JSON file in this directory
3. Add the agent to `registry.json`
4. Update this README with agent information

## References

- Main agent definitions: `../../../AGENTS.md`
- Backlog items: `../../../BACKLOG.md`
- Repository README: `../../../README.md`

---

**Last Updated**: 2026-06-21  
**Version**: 1.0.0  
**Schema Version**: 1.0
