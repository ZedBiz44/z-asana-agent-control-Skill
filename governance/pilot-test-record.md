# Z Asana Agent Control Pilot and Trigger-Test Record

Date: 2026-08-27 MST | Tester: Manus | Status: Partial | Functional test pending

## Artifact and Environment

| Field | Record |
| --- | --- |
| Skill identifier | `z-asana-agent-control` |
| Repository and commit or release | `https://github.com/ZedBiz44/z-asana-agent-control-Skill`; initial source publication `1b27cdc49cedba1aeca36a137e2607071d86a11f`. |
| Deployable package path | `dist/z-asana-agent-control/` |
| Platform and version | OpenClaw 2026.7.1 on VPS1. |
| Pilot agent or environment | Terry, Amanda, and Inga controlled cohort. |
| Installation path | `/opt/openclaw/agents/<agent>/skills/` and `/opt/openclaw/agents/<agent>/workspace/skills/`, mounted as runtime discovery paths. |
| Fresh session or restarted gateway confirmed | Each agent container was restarted and returned healthy. |

## Discovery Check

| Check | Result | Evidence |
| --- | --- | --- |
| Package installed from current commit | Passed | Commit `733c340`; package hash `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`; installed by Manus on Terry, Amanda, and Inga. |
| Skill appears in the platform skill list | Passed | All three healthy, restarted runtimes report the new Skill only. |
| Expected metadata is visible | Passed | Each skills list reports `z-asana-agent-control` ready with the expected description; the retired identifier is absent. |

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
- Validation result: Package hash matched the committed deployable artifact in both live discovery paths for Terry, Amanda, and Inga. All containers reported healthy and only the renamed Skill was discoverable.
- Observed issue or none: Initial host writes were blocked by ownership. The approved Docker Alpine mount workaround installed the package safely. One Terry container-local backup and three Amanda advanced-control references remained after the first cleanup. They were removed or renamed, then final audit confirmed no legacy folders or references across live skill, workspace, and backup paths.

## Rollback Readiness

- Last known-good commit or release: The retired legacy package had SHA-256 `f1661c6124adb9a60fbf7b5d4df9526576ae076b1971cc73e93f3cef63ee096d` on all three agents before deletion. The deployed package has SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`.
- Verified rollback or removal method: The deploy procedure can remove the new package and refresh discovery. Restoring the legacy package is intentionally out of scope because Jack explicitly directed deletion of legacy copies and backup folders.
- Rollback test performed: No. A functional test by Jack is pending; no rollback is indicated while the new package is healthy and discoverable.

## Sign-Off

- Tester: Manus completed structural, deployment, health, discovery, capability-inventory, hash, and legacy-removal checks. Jack will perform functional tests.
- Reviewer: Pending Jack
- Approver: Jack authorized the controlled three-agent rollout on 2026-08-27 MDT.
- Deployment decision: Controlled three-agent pilot cohort deployed. Functional test and final approval pending.
