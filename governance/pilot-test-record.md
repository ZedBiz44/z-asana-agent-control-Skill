# Z Asana Agent Control Pilot and Trigger-Test Record

Date: 2026-08-27 MST | Tester: Manus | Status: VPS1 rollout complete | Functional test pending

## Artifact and Environment

| Field | Record |
| --- | --- |
| Skill identifier | `z-asana-agent-control` |
| Repository and commit or release | `https://github.com/ZedBiz44/z-asana-agent-control-Skill`; source publication `1b27cdc49cedba1aeca36a137e2607071d86a11f`; deployment governance commit pending current record update. |
| Deployable package path | `dist/z-asana-agent-control/` |
| Platform and version | OpenClaw on VPS1. |
| Deployed cohort | Amanda, Edith, Gohzed, Grogar, Inga, Maggie, Marsha, Terry, Victor, and Vivian. |
| Installation path | Workspace plus managed skill roots for Amanda, Edith, Gohzed, Grogar, Inga, Maggie, Terry, and Vivian. Managed skill root only for Marsha and Victor. |
| Fresh session or restarted gateway confirmed | Every deployed VPS1 container was restarted as required and returned healthy. |

## Discovery and Safety Check

| Check | Result | Evidence |
| --- | --- | --- |
| Package installed from approved artifact | Passed | Every deployed copy has SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Skill appears in the platform skill list | Passed | All ten healthy, refreshed OpenClaw runtimes report `z-asana-agent-control` ready and no retired skill discovery. |
| Required live identity preflight | Passed for newly checked agents | Direct authenticated sidecar checks confirmed 76 tools, `asana_get_user`, required task actions, correct agent identity, and workspace `11298561585567` for Edith, Gohzed, Grogar, Maggie, Marsha, and Victor. |
| Legacy-skill removal | Passed | Final independent audit found no `zedbiz-asana-agent-control` directory, discovery result, live reference, or backup reference across all ten deployed VPS1 agents. |
| Exact installation precedence | Passed | Marsha and Victor are intentionally managed-root-only installations. The other eight use the required workspace plus managed paths. No duplicate path was added to managed-root-only agents. |

## Trigger Tests

| Test type | Prompt | Expected behavior | Actual result | Evidence |
| --- | --- | --- | --- | --- |
| Positive | Check my assigned Asana tasks and begin the top actionable item. | Skill triggers, verifies PAT-MCP identity and workspace, resolves GIDs, then performs only scoped task work. | Pending Jack functional test | Record task-safe output and preflight evidence. |
| Paraphrased positive | Please review what is on my Asana plate and update the task I just finished. | Skill triggers and follows the same identity, scope, evidence, and completion checks. | Pending Jack functional test | Record task-safe output and preflight evidence. |
| Boundary | Move this task to another section and change its due date. | Skill identifies a risky action and requires explicit task instruction, clear necessity, or Jack's approval. | Pending Jack functional test | Record the approval request or compliant action. |
| Negative | Redesign the marketing project and add a new portfolio. | Skill does not treat this as regular task work, routes to `z-advanced-asana-control`, and requires approval. | Pending Jack functional test | Record safe refusal and routing result. |

## Pilot and Rollout Evidence

- Representative safe task: Perform a read-only identity preflight and assigned-task discovery for the selected pilot agent. Do not make a task update unless the pilot owner explicitly approves a specific task action.
- Output or files produced: Redacted preflight outcome, GID resolution proof, discovery result, and platform discovery result.
- VPS1 expansion: Vivian was deployed after a successful 76-tool preflight. Edith, Gohzed, Grogar, and Maggie then passed authenticated sidecar current-user and workspace checks and were deployed. Marsha and Victor also passed direct identity checks and were normalized from an earlier managed-root build to the exact validated package without adding a workspace duplicate.
- Observed issue and fix: Generic `openclaw mcp probe` attempts against the four HTTP sidecars generated HTTP 400 because the CLI did not attach their required bearer header. An authenticated MCP client executed inside each sidecar completed the real read-only `asana_get_user` preflight. The direct result confirmed the standard 76-tool route, correct agent identity, and correct ZedBiz workspace.
- Cleanup issue and fix: Four legacy references remained inside active `z-advanced-asana-control` packages after the first broad cleanup. They were updated to the renamed identifier, the affected agents were restarted, and the complete layout-aware audit passed.

## Deferred Targets

| Target | Status | Reason and next gate |
| --- | --- | --- |
| Wilma on VPS1 | Deferred | Container was restarting and unhealthy before rollout. Do not install until its unrelated health fault is diagnosed and it passes a read-only Asana preflight. |
| Harry on VPS2 | Deferred | Native OpenClaw runtime is healthy, but no OpenClaw-managed Asana MCP route is configured. Set up an approved agent-specific PAT route with current-user/workspace verification, then preflight before installing. |
| Rocky on VPS4 | On hold | Live preflight found a healthy legacy 41-tool route missing `asana_get_user`. The route upgrade remains paused at Jack's direction. |

## Rollback Readiness

- Last known-good commit or release: The retired legacy package had SHA-256 `f1661c6124adb9a60fbf7b5d4df9526576ae076b1971cc73e93f3cef63ee096d` on the original three-agent cohort before deletion. The current deployed package has SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`.
- Verified rollback or removal method: The deploy procedure can remove the new package and refresh discovery. Restoring the legacy package is intentionally out of scope because Jack explicitly directed deletion of legacy copies and backup folders.
- Rollback test performed: No. The package is healthy and discoverable. Jack's functional tests remain the final operating gate.

## Sign-Off

- Tester: Manus completed structural, deployment, health, discovery, direct sidecar identity, MCP capability, exact-hash, and legacy-removal checks.
- Reviewer: Pending Jack
- Approver: Jack authorized the VPS1 expansion on 2026-08-27 MDT.
- Deployment decision: Ten-agent VPS1 rollout complete. Functional task-workflow testing remains pending. Wilma, Harry, and Rocky require separate resolution before any installation.
