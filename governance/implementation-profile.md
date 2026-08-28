# Z Asana Agent Control Implementation Profile

Date: 2026-08-27 MST | Prepared by: Manus | Status: Controlled Cohort Deployed | Functional Test Pending

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
| Target installation locations | Confirm the live runtime's skills root and precedence before pilot installation. Do not assume a path. |
| Platform validators | ZedBiz repository validator and the target platform's skills-list discovery check. |

## Controls and Approval

| Field | Decision |
| --- | --- |
| Risk tier | Fleet. The Skill controls private, live Asana access and is intended for multiple agents. |
| Default operating mode | Preserve the mode in the requesting task. Get-er-Done Mode executes within boundaries; Diagnose Mode requires confirmation before changes. |
| Human approver | Jack or an authorized ZedBiz operational owner. |
| Pilot agent or environment | Terry, Amanda, and Inga on VPS1. Jack authorized the controlled cohort deployment and will perform functional testing. |
| Wider rollout rule | Do not deploy beyond this cohort until functional tests pass, the pilot record is completed, and Jack confirms rollout. |
| Stop and escalation conditions | Identity mismatch, wrong workspace, unknown route, unavailable approved MCP, ambiguous GID, restricted action, permission failure, material new risk, or unresolved approval. |
| Retry limit | Three failed safe checks, unless an earlier identity, authorization, permission, or scope failure requires an immediate stop. |

## Security and Rollback

| Field | Decision |
| --- | --- |
| Security review record | `governance/security-rollback-review.md` |
| Approved data and source boundaries | Approved agent-owned Asana data only, accessed through the approved PAT-backed MCP route. |
| Approved execution boundaries | Read and narrow task-write actions in `SKILL.md`; no unrestricted administration or personal Asana route. |
| Last known-good commit or release | Retired legacy package SHA-256: `f1661c6124adb9a60fbf7b5d4df9526576ae076b1971cc73e93f3cef63ee096d`. New deployed package SHA-256: `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Rollback owner | Jack or the authorized ZedBiz platform operator performing the pilot. |
| Verified rollback or removal procedure | New package removal and runtime refresh are available. Legacy restoration is intentionally excluded because Jack directed deletion of legacy copies and backups. |

## Completion Evidence

| Evidence | Status |
| --- | --- |
| Structural validator result | Passed on 2026-08-27 MST with `validate_skill.py --repository .` before publication. |
| Platform validator result | Passed package discovery, health, MCP tool inventory, and exact-hash checks on Terry, Amanda, and Inga. |
| Trigger-test record | `governance/pilot-test-record.md`; functional prompts remain pending Jack's test. |
| Pilot result | Deployment infrastructure passed. Functional Asana workflow test pending. |
| Deployed commit or release | Deployed package from commit `733c340` to Terry, Amanda, and Inga. |
| GitHub issue or change record | [Issue #1](https://github.com/ZedBiz44/z-asana-agent-control-Skill/issues/1). |
| Notion operational summary | [Z Asana Agent Control SOP](https://app.notion.com/p/3c9a3e33d58181fab8a5c2a180b648af). |
| Final approver and date | Pending. |
