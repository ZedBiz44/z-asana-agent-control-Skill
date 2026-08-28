# Z Asana Agent Control Implementation Profile

Date: 2026-08-27 MST | Prepared by: Manus | Status: VPS1 rollout complete | Functional test pending

## Identity and Ownership

| Field | Decision |
| --- | --- |
| Skill display name | Z Asana Agent Control |
| Canonical skill identifier | `z-asana-agent-control` |
| Owner or publisher | ZedBiz44 |
| Repository | `https://github.com/ZedBiz44/z-asana-agent-control-Skill` |
| Authoritative branch | `main` |
| Legacy source | `ZedBiz-openclaw-ai-agents-vps1-vps2/skills/zedbiz-asana-agent-control` at `5dab6560b9a088b3f5079845b78a419cbc02fe7a` |
| License or attribution decision | ZedBiz-owned migration from the legacy ZedBiz44 repository. No separate license file was present in the reviewed legacy skill folder. |
| Naming exception | None. Repository package identifier and runtime metadata use the `z-` namespace. |

## Purpose and Scope

| Field | Decision |
| --- | --- |
| Primary job | Control regular agent-owned Asana task work through the approved PAT-backed MCP route. |
| Intended users | ZedBiz AI agents performing ordinary assigned-task work in Asana. |
| Positive triggers | Identity preflight, assigned-task discovery, task read/update/comment/complete, and read-only team or portfolio navigation. |
| Requests that must not trigger | Structural project, portfolio, custom-field, team-membership, bulk, delete, or personal-account actions. |
| Included actions | Scoped task actions within `SKILL.md` safe, normal, and explicitly approved risky boundaries. |
| Excluded actions | All restricted administrative actions; route to `z-advanced-asana-control`. |

## Platforms and Packaging

| Field | Decision |
| --- | --- |
| Supported platform | OpenClaw-compatible agent runtimes using an approved agent PAT-backed Asana MCP route. |
| Authoring source path | Repository root `SKILL.md` and `agents/openai.yaml`. |
| Deployable package path | `dist/z-asana-agent-control/`. |
| Required platform adapters | `agents/openai.yaml` only. No separate Codex or Hermes adapter is provided. |
| Target installation locations | Confirm the live runtime's skill root and precedence before installation. The current VPS1 cohort uses either workspace plus managed roots or managed root only. |
| Platform validators | ZedBiz repository validator, target platform skill discovery, exact package hash, and read-only agent-identity plus workspace preflight. |

## Controls and Approval

| Field | Decision |
| --- | --- |
| Risk tier | Fleet. The Skill controls private, live Asana access and is intended for multiple agents. |
| Default operating mode | Preserve the mode in the requesting task. Get-er-Done Mode executes within boundaries; Diagnose Mode requires confirmation before changes. |
| Human approver | Jack or an authorized ZedBiz operational owner. |
| Completed VPS1 cohort | Amanda, Edith, Gohzed, Grogar, Inga, Maggie, Marsha, Terry, Victor, and Vivian. |
| Approval record | Jack authorized the controlled initial cohort and the VPS1 expansion on 2026-08-27 MDT. |
| Wider rollout rule | Each distinct runtime or Asana-route pattern still requires a read-only identity, workspace, capability, discovery, and health preflight before installation. |
| Stop and escalation conditions | Identity mismatch, wrong workspace, unknown route, unavailable approved MCP, missing `asana_get_user`, ambiguous GID, restricted action, permission failure, material new risk, or unresolved approval. |
| Retry limit | Three failed safe checks, unless an earlier identity, authorization, permission, or scope failure requires an immediate stop. |

## Security and Rollback

| Field | Decision |
| --- | --- |
| Security review record | `governance/security-rollback-review.md` |
| Approved data and source boundaries | Approved agent-owned Asana data only, accessed through the approved PAT-backed MCP route. |
| Approved execution boundaries | Read and narrow task-write actions in `SKILL.md`; no unrestricted administration or personal Asana route. |
| Current package fingerprint | SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Legacy handling | Retired package directories, discovery copies, and backup artifacts were removed from the ten completed VPS1 agents. Restoring the legacy package is intentionally excluded by Jack's deletion directive. |
| Rollback owner | Jack or the authorized ZedBiz platform operator performing the rollout. |
| Verified rollback or removal procedure | New package removal and runtime refresh are available. Legacy restoration is intentionally excluded because Jack directed deletion of legacy copies and backups. |

## Completion Evidence

| Evidence | Status |
| --- | --- |
| Structural validator result | Passed on 2026-08-27 MST with `validate_skill.py --repository .` before publication. |
| Initial platform validation | Passed package discovery, health, MCP tool inventory, and exact-hash checks on Terry, Amanda, and Inga. |
| Expanded VPS1 validation | Passed direct authenticated Asana current-user, workspace, and 76-tool capability checks for Edith, Gohzed, Grogar, Maggie, Marsha, and Victor. Final audit passed for all ten deployed VPS1 agents. |
| Trigger-test record | `governance/pilot-test-record.md`; Jack's functional prompts remain pending. |
| Deferred installation conditions | Wilma is unhealthy. Harry has no configured OpenClaw-managed Asana MCP route. Rocky's 41-tool route lacks `asana_get_user` and remains on hold. |
| Deployed commit or release | Approved package from commit `733c340`, deployed with the current exact package hash to the ten-agent VPS1 cohort. |
| GitHub issue or change record | [Issue #1](https://github.com/ZedBiz44/z-asana-agent-control-Skill/issues/1), with additional VPS4 Rocky finding in [VPS4 issue #38](https://github.com/ZedBiz44/ZedBiz-openclaw-vps4/issues/38). |
| Notion operational summary | [Z Asana Agent Control SOP](https://app.notion.com/p/3c9a3e33d58181fab8a5c2a180b648af). |
| Final approver and date | Pending Jack's functional workflow validation. |
