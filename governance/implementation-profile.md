# Z Asana Agent Control Implementation Profile

Date: 2026-08-28 MST | Prepared by: Manus | Status: VPS1 and VPS2 technical rollout complete | Functional test pending

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
| Required platform adapters | `agents/openai.yaml` only. No separate Hermes adapter is provided. |
| VPS1 implementation | Agent-specific persistent Streamable HTTP MCP sidecars on the internal Docker network. |
| VPS2 implementation | Agent-specific persistent Streamable HTTP MCP systemd instances, each bound only to `127.0.0.1` and using the existing agent `op run` startup injection. |
| VPS2 installation location | `/root/.openclaw-<agent>/workspace/skills/z-asana-agent-control/`. |
| Platform validators | ZedBiz repository validator, target platform skill discovery, exact package hash, health, and read-only agent-identity plus workspace preflight. |

## Controls and Approval

| Field | Decision |
| --- | --- |
| Risk tier | Fleet. The Skill controls private, live Asana access and is intended for multiple agents. |
| Default operating mode | Preserve the mode in the requesting task. Get-er-Done Mode executes within boundaries; Diagnose Mode requires confirmation before changes. |
| Human approver | Jack or an authorized ZedBiz operational owner. |
| Completed VPS1 cohort | Amanda, Edith, Gohzed, Grogar, Inga, Maggie, Marsha, Terry, Victor, and Vivian. |
| Completed VPS2 cohort | Harry, Suzy, and Frank. |
| Approval record | Jack authorized the controlled initial cohort, the VPS1 expansion, and all-three-agent VPS2 rollout. |
| Wider rollout rule | Each distinct runtime or Asana-route pattern requires a read-only identity, workspace, capability, discovery, and health preflight before installation. |
| Stop and escalation conditions | Identity mismatch, wrong workspace, unknown route, unavailable approved MCP, missing `asana_get_user`, ambiguous GID, restricted action, permission failure, material new risk, or unresolved approval. |
| Retry limit | Three failed safe checks, unless an earlier identity, authorization, permission, or scope failure requires an immediate stop. |

## Security and Rollback

| Field | Decision |
| --- | --- |
| Security review record | `governance/security-rollback-review.md` |
| Approved data and source boundaries | Approved agent-owned Asana data only, accessed through the approved PAT-backed MCP route. |
| VPS2 credential process | Existing agent-owned 1Password Asana items remain as `op://agent-<agent>/asana-api-key-<agent>/credential` references in the agent `.env`. Each process resolves the reference only at startup through `op run`. |
| VPS2 network boundary | Each service binds to `127.0.0.1` only, with a unique port and no public Caddy route. |
| Current package fingerprint | SHA-256 `72d2ef93a498f30347bf00a074e3e6854118e52f003ca1d8785dd5b5a92a188c`. |
| Legacy handling | Retired package directories, discovery copies, and backup artifacts were removed from the completed VPS1 and VPS2 cohorts. Restoring the legacy package is intentionally excluded by Jack's deletion directive. |
| Rollback owner | Jack or the authorized ZedBiz platform operator performing the rollout. |
| Verified rollback or removal procedure | The VPS2 native installer restores the original `.env` and `openclaw.json`, removes the service and new package, then restarts only the affected agent on pilot failure. Harry's first guarded attempt exercised this path successfully. |

## Completion Evidence

| Evidence | Status |
| --- | --- |
| Structural validator result | Passed on 2026-08-27 MST with `validate_skill.py --repository .` before publication. |
| VPS1 validation | Passed package discovery, health, direct authenticated identity, capability inventory, exact-hash, and legacy-removal checks for the ten-agent cohort. |
| VPS2 validation | Passed native loopback isolation, service health, standard 47-tool capability check, exact hash, new-only discovery, and direct authenticated identity/workspace plus assigned-task discovery for Harry, Suzy, and Frank. |
| Verified VPS2 identities | Harry `1215559750337835`, Suzy `1215557534470003`, and Frank `1215596271715682`, each in workspace `11298561585567`. |
| Trigger-test record | `governance/pilot-test-record.md`; Jack's functional prompts remain pending. |
| Deferred installation conditions | Wilma is unhealthy. Rocky's 41-tool route lacks `asana_get_user` and remains on hold. |
| Technical source records | [VPS2 deployment record](https://github.com/ZedBiz44/ZedBiz-openclaw-ai-agents-vps1-vps2/blob/main/tracking/zedbiz-secondary-vps/2026-08-28-vps2-asana-mcp-skill-rollout.md); native deployment code in `docker/asana-http-mcp/deploy/vps2/`. |
| GitHub issue or change record | [Issue #1](https://github.com/ZedBiz44/z-asana-agent-control-Skill/issues/1), [VPS2 diagnosis issue #210](https://github.com/ZedBiz44/ZedBiz-openclaw-ai-agents-vps1-vps2/issues/210), and VPS4 Rocky issue #38. |
| Notion operational summary | [Z Asana Agent Control SOP](https://app.notion.com/p/3c9a3e33d58181fab8a5c2a180b648af). |
| Final approver and date | Pending Jack's functional workflow validation. |
