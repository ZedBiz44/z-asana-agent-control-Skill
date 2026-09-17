# Z Asana Agent Control Skill

This repository is the authoritative GitHub source for `z-asana-agent-control`, the regular-workflow guardrail for ZedBiz AI agents using Asana. It ensures day-to-day task work uses the correct user-authorized connection or PAT-backed agent identity, resolves object GIDs safely, and keeps structural administration outside the regular task path.

## When to Use

Use this Skill before an AI agent reads or performs ordinary work on its own assigned Asana tasks. Appropriate requests include finding the agent's assigned incomplete work, reading task context, posting evidence-based progress, updating a directly assigned task, completing verified work, and read-only navigation of teams or portfolios needed to answer an assigned-task question.

The Skill checks the selected user or agent account before work. It supports both Get-er-Done Mode and Diagnose Mode, while preserving their distinct authorization rules.

## Do Not Use

Do not use this Skill for project setup, project briefs or status updates, project or portfolio restructuring, broad timeline changes, custom-field administration, team membership, bulk updates, or deletion. Route those actions to `z-advanced-asana-control` and obtain the required approval.

Do not use a Jack-authenticated Codex, ChatGPT, browser session, or any personal Asana connection for agent-owned work. Do not store or expose secrets, personal access tokens, sync tokens, passwords, private keys, or complete environment files.

## Authoritative Files and Package

`SKILL.md` is the authoritative runtime instruction set. `agents/openai.yaml` contains discovery metadata for an OpenAI-compatible runtime. The `governance/` directory holds the implementation profile, security and rollback review, and pilot test record for this Fleet-class skill. The human-readable [operational SOP](https://app.notion.com/p/3c9a3e33d58181fab8a5c2a180b648af) is maintained in Notion and does not replace the GitHub source.

The committed `dist/z-asana-agent-control/` directory is the deployable package. It is derived from the root `SKILL.md` plus the runtime resources named in `package-resources.txt`; it must remain content-equivalent to the source at the documented release commit. The authoring repository, rather than the deployed package, is the source of truth.

## Validate and Deploy

Run the ZedBiz developer validator from a trusted checkout of `z-ai-skill-developer-Skill`:

```bash
python3 /path/to/z-ai-skill-developer-Skill/scripts/validate_skill.py --repository /path/to/z-asana-agent-control-Skill
```

Confirm the source and deployable `SKILL.md` files are identical, then install only `dist/z-asana-agent-control/` into the approved OpenClaw skill root. Start a fresh session or restart the gateway if skill metadata is cached. Confirm discovery in the platform skill list and test a single pilot agent with a read-only identity preflight before wider rollout. Record source commit, installation path, discovery evidence, and pilot outcome in `governance/pilot-test-record.md`.

## Safety and Approval Boundaries

The Skill reads and can update private Asana data through an approved agent PAT route. It therefore requires the preflight identity and workspace checks, GID resolution, narrow assigned-task scope, explicit action levels, and stop conditions documented in `SKILL.md`.

Risky task changes require an explicit task instruction, clear work necessity, or Jack's approval. Destructive, structural, bulk, portfolio, project, and production-impacting administration remains restricted until routed through the advanced control Skill with human approval. Roll back a failed pilot by removing the deployed package or restoring the last known-good package, then capture the evidence in the governance records.

## Shared ChatGPT, Cody and agent instructions

Direct user-authorized ChatGPT/Cody work uses the verified connected account. Work owned by an OpenClaw/Hermes agent uses its approved agent connection. The current SKILL.md governs this distinction. No new connection or memory service is installed by this package.

The deployable package includes SKILL.md and every directory listed in package-resources.txt, including agents/openai.yaml. Rebuild it from this source before installing; do not install an old committed dist entry in isolation. Source and generated dist files must match. See the 2026-09-17 follow-up record in z-ai-skill-developer-Skill for Cody verification and separate ChatGPT status.
