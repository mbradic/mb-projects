# Development Workflow

## Overview

This workflow defines the end-to-end development process with explicit stages for staging environments, structured manual testing, dependency management, and measurable quality gates. It incorporates the AI agent architecture and scales to support larger teams and more complex features.

---

## Git Branching Strategy

```
main (production-ready)
  ├─ feature/<short-name>        ← one branch per backlog item
  │   └─ PR → CI checks → review → merge
  │
staging (pre-production environment)
  └─ deployed from main after release tag
```

### Branch Naming Conventions

- **Features:** `feature/<issue-number>-<short-name>` (e.g., `feature/42-user-auth`)
- **Bug fixes:** `bugfix/<issue-number>-<short-name>` (e.g., `bugfix/43-login-crash`)
- **Hotfixes:** `hotfix/<short-name>` (e.g., `hotfix/critical-security`)

---

## Workflow Steps (Enhanced)

### Step 1: Issue-First Planning
**Owner:** Backlog Manager Agent  
**Duration:** < 1 day

1. Create GitHub issue from backlog item with:
   - Acceptance criteria (testable, measurable)
   - User story context
   - Linked project/milestone
   - Labels (priority, area, complexity)
   - Assigned owner

2. Set complexity level (impacts downstream workflow):
   - **Small:** 1-2 day effort, few dependencies
   - **Medium:** 3-5 day effort, some dependencies
   - **Large:** 5+ day effort, many dependencies

**Output:** GitHub issue ready for branching

---

### Step 2: Create Feature Branch
**Owner:** Feature Branch Coordinator Agent  
**Duration:** 1 hour

1. Create branch from `main`
2. Link branch to issue (GitHub automatically tracks)
3. Initial commit references issue: `git commit -m "chore: initialize branch for issue #42"`
4. For **Large** features: create draft PR immediately for visibility

**Output:** Feature branch created and linked

---

### Step 3: (Optional) Design Review
**Owner:** Code Review Expert / Methodology Expert Agents  
**Duration:** 2-4 hours (only for Medium/Large features)  
**When to skip:** Small, straightforward changes

For features with architectural impact:
1. Create ADR (Architecture Decision Record) or design doc in PR as comment
2. Schedule async review using `co-authors` feature in GitHub
3. Resolve architectural concerns before development
4. Reduces mid-development refactoring

**Output:** Design approved, ready for test scenarios

---

### Step 4: Create Test Scenarios
**Owner:** Test Scenario Designer Agent  
**Duration:** 2-8 hours (proportional to feature complexity)

1. **Manual Testing Scenarios:**
   - Document step-by-step user workflows
   - Include positive cases and edge cases
   - Specify expected results and error conditions
   - Create data setup requirements
   - Template: `tests/manual/[feature-name].md`

2. **E2E Test Specifications:**
   - Create test code (Cypress, Playwright, etc.)
   - Define test fixtures and mocks
   - Identify test data seeds required
   - Location: `tests/e2e/[feature-name].spec.ts`

3. **Test Coverage Goals:**
   - Critical paths: 100% coverage
   - Error handling: 80%+ coverage
   - Edge cases: document uncovered scenarios and why

4. **Testing Checklist in Issue:**
   - Add task list to issue body for manual test sign-off
   - Each task represents a manual testing scenario

**Output:** Test plan reviewed and approved by user (Step 5)

---

### Step 5: User Review & Approval of Test Plan
**Owner:** User/Product Owner  
**Duration:** 1-2 hours

1. Review manual testing scenarios
2. Verify all acceptance criteria are covered
3. Request clarifications or additional test cases
4. Approve test plan by checking `✅ Tests approved` on issue

**Failure Path:** Return to Step 4 for revisions

**Output:** Test plan approved, ready for implementation

---

### Step 6: Local Development & Implementation
**Owner:** Feature Developer Agent  
**Duration:** 1-10 days (depends on complexity)

1. Implement feature code locally
2. Write code alongside tests:
   - Unit tests as you write code
   - Integration tests for component interactions
   - Follow existing code style and patterns

3. Run tests locally:
   ```bash
   npm run lint        # Code quality
   npm run test        # Unit tests
   npm run test:e2e    # E2E tests locally
   ```

4. Commit frequently with clear messages:
   - `feat: add user authentication endpoint`
   - `test: add tests for auth validation`
   - Reference issue: `feat: add login form (issue #42)`

5. Push to feature branch and create **Draft PR** with:
   - Clear title: `[WIP] Add user authentication`
   - Link to issue: `Closes #42`
   - Summary of changes
   - Known limitations or TODOs

**Output:** Draft PR created with working code

---

### Step 7: Automated CI/CD Checks
**Owner:** GitHub Actions  
**Duration:** 5-15 minutes

**CI Pipeline runs automatically on PR creation:**

1. **Linting:**
   - ESLint for code style
   - TypeScript compiler for type safety
   - Prettier for formatting (auto-fix available)
   - ✅ **Pass requirement:** No errors or warnings

2. **Unit Tests:**
   - Jest or test runner configured in package.json
   - ✅ **Pass requirement:** 100% pass rate
   - Coverage threshold: 80% (configurable per team)

3. **Integration Tests:**
   - Database/API integration tests
   - ✅ **Pass requirement:** 100% pass rate

4. **Build Check:**
   - Verify production build succeeds
   - ✅ **Pass requirement:** No build errors

5. **Security Scan:**
   - CodeQL or similar vulnerability scanner
   - ✅ **Pass requirement:** No critical vulnerabilities

**Failure Handling:**
- ❌ **Linting fails:** Developer fixes locally, pushes fix
- ❌ **Tests fail:** Developer investigates, fixes code or updates test
- ❌ **Build fails:** Developer debugs build, pushes fix
- ❌ **Security scan:** Developer addresses vulnerability or gets exception
- Auto-comments on PR with failure details

**Output:** CI checks pass (green check on PR)

---

### Step 8: Code Review
**Owner:** Code Review Expert Agent + Minimum 1 Human Reviewer  
**Duration:** 2-24 hours

**Review focuses on:**
- Code quality and maintainability
- Security vulnerabilities
- Performance implications
- Adherence to architecture and patterns
- Test coverage adequacy
- Documentation completeness

**Code Review Checklist:**
- [ ] Code follows style guide
- [ ] All acceptance criteria implemented
- [ ] Test coverage adequate (80%+)
- [ ] No security issues
- [ ] Error handling present
- [ ] Documentation updated
- [ ] No breaking changes documented

**Review Outcomes:**
- ✅ **Approved:** Ready for merge
- 🔄 **Changes Requested:** Developer addresses feedback, updates PR
- 💬 **Comment:** Informational, not blocking

**Iterative Process:** Repeat code review → changes → push until approved

**Output:** Code review approved

---

### Step 9: Merge to Main
**Owner:** Developer / Workflow Manager Agent  
**Duration:** 1 hour

**Merge Requirements Met:**
- ✅ CI checks pass
- ✅ Code review approved
- ✅ Branch is up-to-date with main (no conflicts)
- ✅ All conversations resolved

**Merge Strategy: Squash Merge**
- Combines all feature commits into single commit on main
- Keeps main history clean
- Commit message: `feat: add user authentication (issue #42)`

**After Merge:**
1. Delete feature branch
2. Close linked issue or move to next stage
3. Create git tag for release: `v1.2.0`

**Output:** Code merged to main, ready for deployment

---

### Step 10: Deploy to Staging
**Owner:** Deployment Orchestrator Agent  
**Duration:** 10-30 minutes

**Deployment Process:**
1. Trigger deployment pipeline (manual or automated)
2. Build application with merged code
3. Deploy to staging environment
4. Verify deployment succeeded
5. Collect deployment logs/artifacts
6. Report staging URL in issue

**Verification:**
- Health check endpoints respond correctly
- Database migrations applied successfully
- Environment variables configured correctly
- All services responding

**Failure Handling:**
- ❌ **Deployment fails:** Investigate logs, rollback if needed, fix and redeploy
- ❌ **Service health check fails:** Verify configuration, redeploy
- Automated notifications to Slack/email on failure

**Output:** Code successfully deployed to staging environment

---

### Step 11: Run E2E Tests on Staging
**Owner:** E2E Test Runner Agent  
**Duration:** 5-30 minutes (depends on test suite size)

**Test Execution:**
1. Run full e2e test suite against staging environment
2. Execute tests in headless mode
3. Capture screenshots/video on failure
4. Generate test report

**Test Report Includes:**
- Total tests run
- Pass/fail counts
- Failed test details (screenshot, console logs, stack trace)
- Test execution time
- Performance metrics

**Test Results Posting:**
1. Comment on PR/issue with test results
2. Attach artifacts (screenshots, video)
3. Create GitHub check with results

**Outcomes:**
- ✅ **All pass:** Proceed to Step 12 (manual testing)
- ❌ **Some fail:** Create issue for test failures, investigate

**Failure Path on Test Failure:**
1. Create issue linked to feature: "E2E test failures in [feature-name]"
2. Assign to Feature Developer for investigation
3. Either fix code or update e2e test expectations
4. Redeploy and rerun tests

**Output:** E2E tests pass on staging environment

---

### Step 12: Manual Testing on Staging
**Owner:** QA Team / Product Owner  
**Duration:** 2-8 hours (depends on complexity)

**Testing Procedure:**
1. Access staging environment URL provided in issue
2. Follow manual testing scenarios created in Step 4
3. Test all acceptance criteria manually
4. Document any issues/edge cases discovered
5. Verify user experience meets expectations

**Testing Checklist:**
- Open checklist in issue (created in Step 4)
- Mark each manual test scenario as complete: ✅
- Add comments for any issues discovered
- Include screenshots of critical workflows

**Outcomes:**
- ✅ **All pass:** Approve for production release
- ❌ **Issues found:** Create issue and assign to Feature Developer
  - Return to Step 6 for bug fixes
  - Redeploy to staging (Step 10)
  - Rerun e2e tests (Step 11)
  - Repeat manual testing (Step 12)

**Sign-off:**
- QA lead adds comment: `✅ Manual testing complete, approved for production`
- Update issue label: `status/ready-for-production`

**Output:** Manual testing complete, feature approved for production

---

### Step 13: Deploy to Production
**Owner:** Deployment Orchestrator Agent  
**Duration:** 15-60 minutes

**Pre-Production Checklist:**
- [ ] All tests passing
- [ ] Manual testing approved
- [ ] Release notes drafted
- [ ] Rollback plan documented
- [ ] On-call engineer available

**Deployment Steps:**
1. Create release branch or tag: `v1.2.0`
2. Generate changelog from commits
3. Trigger production deployment
4. Monitor deployment progress
5. Verify health checks pass
6. Monitor application logs for errors
7. Verify critical user paths working

**Deployment Monitoring:**
- CPU/memory usage within bounds
- Error rates normal (not spiking)
- Response times acceptable
- No database issues
- Integrations with external services working

**Failure/Rollback:**
- ❌ **Deployment fails:** Investigate, fix, redeploy
- ❌ **Post-deployment issue:** Trigger rollback to previous version
  - Rollback is automated: `git revert [commit]` + redeploy
  - Notify team and stakeholders
  - Create incident issue

**Output:** Code successfully deployed to production

---

### Step 14: Release & Post-Deployment
**Owner:** Workflow Manager Agent  
**Duration:** 1-2 hours

**Release Activities:**
1. Create GitHub release with semantic version
2. Publish changelog
3. Close all related issues
4. Communicate release to stakeholders
5. Update documentation if needed

**Post-Deployment Monitoring:**
- Monitor error rates and logs for 24 hours
- Watch for performance anomalies
- Track user feedback for issues
- Prepare hotfix if critical issues discovered

**Release Tag Format:**
- Semantic versioning: `v[MAJOR].[MINOR].[PATCH]`
- Example: `v1.2.3`
- Annotated tags with release notes

**Output:** Release complete, feature in production

---

## Dependency Management

### Issue Dependencies

Use GitHub issue linking to represent dependencies:

```
Issue A blocks Issue B if:
  - Issue B requires code from Issue A
  - Issue B cannot be tested without Issue A
  - Issue B testing depends on Issue A

In Issue B, add: "Depends on #[A issue number]"
In Issue A, add: "Blocks #[B issue number]"
```

### Workflow Blocking

- **Blocked:** Cannot proceed until dependency is resolved
  - Label: `status/blocked`
  - Add note: `Blocked by #[issue]`
  
- **Ready:** All dependencies met
  - Label: `status/ready`
  - Can proceed to development

### Complex Feature Coordination

For features with many dependencies (Large complexity):
1. Use GitHub project board to visualize workflow
2. Create epic issue linking all sub-issues
3. Use milestones to group related work
4. Run retrospective after completion to document lessons

---

## Feature Complexity Decision Matrix

Choose which steps to include based on feature complexity:

| Step | Small | Medium | Large |
|------|:-----:|:------:|:-----:|
| 1. Issue Planning | ✅ | ✅ | ✅ |
| 2. Create Branch | ✅ | ✅ | ✅ |
| 3. Design Review | ⏭️ | ✅ | ✅ |
| 4. Test Scenarios | ✅ | ✅ | ✅ |
| 5. User Review | ✅ | ✅ | ✅ |
| 6. Implementation | ✅ | ✅ | ✅ |
| 7. CI Checks | ✅ | ✅ | ✅ |
| 8. Code Review | ✅ | ✅ | ✅ |
| 9. Merge | ✅ | ✅ | ✅ |
| 10. Deploy Staging | ⏭️ | ✅ | ✅ |
| 11. E2E Tests | ⏭️ | ✅ | ✅ |
| 12. Manual Testing | ⏭️ | ✅ | ✅ |
| 13. Deploy Production | ✅ | ✅ | ✅ |
| 14. Release | ✅ | ✅ | ✅ |

**Legend:**
- ✅ Mandatory
- ⏭️ Optional/Skip for small changes

---

## CI/CD Failure Handling

### CI Check Failures

```
Test Fails
  ↓
Auto-comment on PR with failure details
  ↓
Developer investigates locally
  ↓
Developer fixes code
  ↓
Developer pushes fix
  ↓
CI automatically reruns
  ↓
If still failing → developer escalates or requests help
```

**Timeout:** If CI check not resolved in 48 hours, issue marked `status/stale` and unscheduled

### Deployment Failures

```
Deployment Fails
  ↓
Notification sent (Slack, email)
  ↓
On-call engineer investigates
  ↓
Option A: Fix issue → redeploy
Option B: Rollback to previous version
  ↓
Create incident issue with root cause
```

---

## Workflow Metrics & SLAs

Track these metrics to measure workflow health:

| Metric | SLA | Owner |
|--------|-----|-------|
| Issue to PR time | < 2 days | Developer |
| PR review time | < 24 hours | Code Reviewer |
| CI check time | < 15 min | Infrastructure |
| Tests to production | < 4 hours | QA/Deployment |
| Production deployment time | < 60 min | DevOps |
| Bug discovery (staging) | > 80% | QA |
| Rollback rate | < 5% | DevOps |
| Mean time to recovery (MTTR) | < 30 min | On-call |

### Weekly Metrics Review

Every Friday, review:
- Average cycle time (from issue to production)
- Number of regressions found in production
- Deployment frequency
- Lead time for changes
- Time to recovery from incidents

---

## Agent Workflow Mapping

```
Step 1 → Backlog Manager Agent
Step 2 → Feature Branch Coordinator Agent
Step 3 → Code Review Expert / Methodology Expert Agents
Step 4 → Test Scenario Designer Agent
Step 5 → [User/Product Owner]
Step 6 → Feature Developer Agent
Step 7 → GitHub Actions (CI/CD)
Step 8 → Code Review Expert Agent + Human Reviewer
Step 9 → Workflow Manager Agent
Step 10 → Deployment Orchestrator Agent
Step 11 → E2E Test Runner Agent
Step 12 → [QA Team/Product Owner]
Step 13 → Deployment Orchestrator Agent
Step 14 → Workflow Manager Agent

Throughout → Methodology Expert (guidance) + AI Advisor (AI practices)
```

---

## Common Workflows

### Standard Feature (Small)
```
Issue → Branch → Tests → Code → CI ✅ → Review ✅ → Merge → Production
Duration: 2-4 days
Steps: 1, 2, 4, 5, 6, 7, 8, 9, 13, 14
```

### Complex Feature (Large)
```
Issue → Branch → Design Review → Tests → Code → CI ✅ → Review ✅ 
→ Merge → Staging → E2E Tests ✅ → Manual Tests ✅ → Production
Duration: 2-4 weeks
Steps: 1-14 (all steps)
```

### Urgent Hotfix
```
Issue (hotfix branch) → Code → CI ✅ → Review ✅ (expedited) 
→ Merge → Production (expedited monitoring)
Duration: < 4 hours
Steps: 1, 2, 6, 7, 8, 9, 13, 14
```

---

## Continuous Improvement

After each release:
1. **Retrospective:** What went well? What could improve?
2. **Metrics review:** Are we meeting SLAs?
3. **Process updates:** Implement improvements
4. **Team feedback:** Gather suggestions from developers and QA

---

## Reference

- **Original Workflow:** See `WORKFLOW.md`
- **Agent Definitions:** See `AGENTS.md`
- **Backlog:** See `BACKLOG.md`
- **Versioning Strategy:** See `VERSIONING.md`
- **Git Flow:** https://github.com/nvie/gitflow
- **Semantic Versioning:** https://semver.org
