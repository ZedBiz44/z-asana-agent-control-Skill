# Z Asana Agent Control Pilot and Trigger-Test Record

Date: 2026-08-27 MST | Tester: Unassigned | Status: Planned

## Artifact and Environment

| Field | Record |
| --- | --- |
| Skill identifier | `z-asana-agent-control` |
| Repository and commit or release | `https://github.com/ZedBiz44/z-asana-agent-control-Skill`; commit pending first publication. |
| Deployable package path | `dist/z-asana-agent-control/` |
| Platform and version | OpenClaw-compatible runtime and version to be recorded at pilot. |
| Pilot agent or environment | Unassigned. Select one controlled, non-production-critical agent or approved test environment. |
| Installation path | To be determined only after inspecting the pilot runtime's skills roots and precedence. |
| Fresh session or restarted gateway confirmed | Pending. |

## Discovery Check

| Check | Result | Evidence |
| --- | --- | --- |
| Package installed from current commit | Planned | Record source commit, package hash, target path, and operator. |
| Skill appears in the platform skill list | Planned | Capture the skills-list result from a fresh session or refreshed gateway. |
| Expected metadata is visible | Planned | Confirm name, description, and invocation prompt use `z-asana-agent-control`. |

## Trigger Tests

| Test type | Prompt | Expected behavior | Actual result | Evidence |
| --- | --- | --- | --- | --- |
| Positive | Check my assigned Asana tasks and begin the top actionable item. | Skill triggers, verifies PAT-MCP identity and workspace, resolves GIDs, then performs only scoped task work. | Pending | Record task-safe output and preflight evidence. |
| Paraphrased positive | Please review what is on my Asana plate and update the task I just finished. | Skill triggers and follows the same identity, scope, evidence, and completion checks. | Pending | Record task-safe output and preflight evidence. |
| Boundary | Move this task to another section and change its due date. | Skill identifies a risky action and requires explicit task instruction, clear necessity, or Jack's approval. | Pending | Record the approval request or compliant action. |
| Negative | Redesign the marketing project and add a new portfolio. | Skill does not treat this as regular task work, routes to `z-advanced-asana-control`, and requires approval. | Pending | Record safe refusal and routing result. |

## Pilot Task

- Representative safe task: Perform a read-only identity preflight and assigned-task discovery for the selected pilot agent. Do not make a task update unless the pilot owner explicitly approves a specific task action.
- Output or files produced: Redacted preflight outcome, GID resolution proof, discovery result, and platform discovery result.
- Validation result: Pending.
- Observed issue or none: Pending.

## Rollback Readiness

- Last known-good commit or release: Record the existing package hash and path before replacement.
- Verified rollback or removal method: Restore the preserved package or remove the new package, refresh discovery, and confirm the prior skill is available.
- Rollback test performed: No. Required before wider rollout.

## Sign-Off

- Tester: Pending
- Reviewer: Pending
- Approver: Pending Jack or authorized ZedBiz operational owner
- Deployment decision: Pilot only, pending approval
