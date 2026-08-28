# Z Asana Agent Control Pilot and Trigger-Test Record

Date: 2026-08-28 MST | Tester: Manus | Status: VPS1 and VPS2 technical rollout complete | Functional test pending

## Artifact and Environment

| Field | Record |
| --- | --- |
| Skill identifier | `z-asana-agent-control` |
| Repository and commit or release | `https://github.com/ZedBiz44/z-asana-agent-control-Skill`; approved deployable package SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Deployable package path | `dist/z-asana-agent-control/` |
| Platform and version | OpenClaw on VPS1 containers and OpenClaw 2026.7.1 native systemd services on VPS2. |
| Deployed cohort | VPS1: Amanda, Edith, Gohzed, Grogar, Inga, Maggie, Marsha, Terry, Victor, Vivian. VPS2: Harry, Suzy, Frank. |
| Installation path | VPS1 uses the previously verified managed and workspace paths. VPS2 uses `/root/.openclaw-<agent>/workspace/skills/z-asana-agent-control/`. |
| Fresh session or restarted gateway confirmed | Every deployed agent was restarted as required and returned healthy. |

## Discovery and Safety Check

| Check | Result | Evidence |
| --- | --- | --- |
| Package installed from approved artifact | Passed | Every deployed copy has SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Skill appears in the platform skill list | Passed | All thirteen healthy, refreshed OpenClaw runtimes report `z-asana-agent-control` and do not report the retired identifier. |
| Required live identity preflight | Passed | VPS1 direct authenticated sidecar checks confirmed 76 tools, `asana_get_user`, required task actions, correct identity, and workspace. VPS2 direct authenticated checks confirmed the standard 47-tool route, including `asana_get_user`, assigned-task discovery, task read, task comment, and task update. |
| VPS2 identity and workspace | Passed | Harry, Suzy, and Frank authenticated as their own `@agents.zbiz.ca` identities and each reported workspace `11298561585567`. |
| Legacy-skill removal | Passed | Final audits found no `zedbiz-asana-agent-control` directory, discovery result, live reference, or backup reference across deployed VPS1 or VPS2 skill paths. |
| VPS2 service isolation | Passed | Each native standard MCP service binds only to `127.0.0.1` on a unique port, with no Caddy route or public listener. |

## Trigger Tests

| Test type | Prompt | Expected behavior | Actual result | Evidence |
| --- | --- | --- | --- | --- |
| Positive | Check my assigned Asana tasks and begin the top actionable item. | Skill triggers, verifies PAT-MCP identity and workspace, resolves GIDs, then performs only scoped task work. | Technical preflight passed; functional task test pending Jack | Record task-safe output and preflight evidence. |
| Paraphrased positive | Please review what is on my Asana plate and update the task I just finished. | Skill triggers and follows the same identity, scope, evidence, and completion checks. | Pending Jack functional test | Record task-safe output and preflight evidence. |
| Boundary | Move this task to another section and change its due date. | Skill identifies a risky action and requires explicit task instruction, clear necessity, or Jack's approval. | Pending Jack functional test | Record the approval request or compliant action. |
| Negative | Redesign the marketing project and add a new portfolio. | Skill does not treat this as regular task work, routes to `z-advanced-asana-control`, and requires approval. | Pending Jack functional test | Record safe refusal and routing result. |

## Pilot and Rollout Evidence

- VPS1 rollout: Vivian was deployed after a successful 76-tool preflight. Edith, Gohzed, Grogar, and Maggie then passed authenticated sidecar current-user and workspace checks and were deployed. Marsha and Victor passed direct identity checks and were normalized from an earlier managed-root build to the exact validated package without adding a workspace duplicate.
- VPS2 pilot: Harry deployed first. His native loopback-only standard MCP service authenticated as `harry@agents.zbiz.ca`, reported user GID `1215559750337835`, workspace `11298561585567`, and five incomplete assigned tasks. Suzy and Frank were deployed after Harry passed and completed equivalent read-only tests.
- VPS2 service design: Existing agent-specific 1Password references resolve at process startup through `op run`. The local MCP service and OpenClaw route both reference the agent's existing Asana item. No PAT was stored in Git, an OpenClaw JSON value, a systemd unit, a command argument, or a deployment record.
- Observed issue and fix: The first native pilot wrongly attempted to create separate bearer items. Agent service accounts correctly denied write permission. The guarded installer fully rolled Harry back. The installer was changed to use the established startup-time injection pattern and then passed. A second error used the email item label field rather than its protected email field; it was corrected before successful deployment.
- Cleanup issue and fix: Four VPS1 legacy references remained inside active `z-advanced-asana-control` packages after broad cleanup. They were updated to the renamed identifier, restarted, and passed the complete layout-aware audit.

## Deferred Targets

| Target | Status | Reason and next gate |
| --- | --- | --- |
| Wilma on VPS1 | Deferred | Container was restarting and unhealthy before rollout. Do not install until its unrelated health fault is diagnosed and it passes a read-only Asana preflight. |
| Rocky on VPS4 | On hold | Live preflight found a healthy legacy 41-tool route missing `asana_get_user`. Route-upgrade work remains paused at Jack's direction. |

## Rollback Readiness

- Last known-good commit or release: The retired legacy package had SHA-256 `f1661c6124adb9a60fbf7b5d4df9526576ae076b1971cc73e93f3cef63ee096d` on the original three-agent VPS1 cohort before deletion. The current deployed package has SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`.
- Verified rollback or removal method: The native VPS2 installer backs up the current OpenClaw configuration and environment, removes the new route and service, restores the original configuration, and restarts only the affected agent if preflight fails. The first Harry pilot exercised and passed this rollback path. Legacy restoration is intentionally excluded because Jack directed deletion of legacy copies and backup folders.
- Rollback test performed: Yes. Harry's first guarded native attempt failed before any Asana call and restored his prior no-Asana configuration. The corrected implementation was then deployed and independently validated.

## Sign-Off

- Tester: Manus completed structural, deployment, health, discovery, direct sidecar identity, MCP capability, exact-hash, legacy-removal, native loopback-isolation, and rollback checks.
- Reviewer: Pending Jack functional task-workflow tests.
- Approver: Jack authorized VPS1 expansion and all-three-agent VPS2 rollout.
- Deployment decision: Thirteen-agent VPS1 and VPS2 technical rollout complete. Functional task-workflow testing remains pending. Wilma and Rocky require separate resolution before installation.
