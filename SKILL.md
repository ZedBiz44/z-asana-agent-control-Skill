---
name: z-asana-agent-control
description: Control daily ZedBiz agent work in Asana. Use for PAT-MCP identity checks, assigned-task updates, and read-only team or portfolio navigation.
---

# Z Asana Agent Control

## Use This Skill

Use for day-to-day Asana work owned by a ZedBiz AI agent, including assigned-task discovery, task reading, evidence-based progress comments, completing finished work, and read-only team or portfolio navigation required by that work.

Use the agent's approved PAT-backed Asana MCP only. Apply this Skill before any Asana query or update.

## Do Not Use This Skill

Do not use for project setup, project briefs or status updates, workflow redesign, portfolio changes, timeline-wide changes, custom-field administration, team-membership changes, bulk updates, deletes, or other structural Asana administration. Route those requests to `z-advanced-asana-control` and obtain the required approval.

Do not use a Jack-authenticated Codex, ChatGPT, browser, or other personal Asana connection for agent-owned work.

## Required Context

Confirm all of the following before task work:

- Agent name.
- Approved agent email and Asana user GID.
- Approved Asana workspace GID.
- Approved PAT-backed Asana MCP server.

Stop if any required value is missing, the MCP is unavailable, the tool route is unknown, or the route uses a personal identity. Do not guess identifiers or credentials.

## Required MCP Capabilities

Before accepting the requested work, confirm that the approved route exposes a current-user check, assigned-task discovery, task read, task comment, and the exact update or completion action requested. Confirm search or typeahead is available for any named object. For team or portfolio questions, confirm the corresponding read-only navigation tools are available.

If the requested capability is absent, stop and report the missing approved capability. Do not substitute a personal connector, unapproved direct REST, or a guessed endpoint.

## Preflight Identity and Route

- Identify the active Asana tool server and confirm it is the approved PAT-backed MCP route.
- Call `asana_get_user` with `user_gid: "me"`, or the current-user equivalent exposed by the approved server.
- Continue only when the returned email equals the approved agent email and the returned workspace list includes the approved workspace GID.
- Record the authenticated email, user GID, workspace GID, and approved MCP route in the task work note or completion evidence. Never record a PAT.

If a Codex or ChatGPT Asana connection returns Jack or another person, treat it as the wrong route. Continue looking for the approved agent PAT route, then stop if it is unavailable.

Use this failure message when the authority check fails:

> Asana work stopped. Expected the approved agent identity and workspace through the approved PAT MCP, but a different identity, workspace, or route was returned. Fix the approved Asana MCP before task execution continues.

A real, read-only current-user call is the authoritative connectivity check. For a Streamable HTTP deployment, a successful `/healthz` check may supplement, but never replace, that identity check. Do not treat a legacy SSE probe returning HTTP 400 as proof that an otherwise working Streamable HTTP route is unusable.

## Resolve Objects Safely

Resolve every name, email, project, section, task, tag, custom field, enum option, team, and portfolio to its GID before querying or changing it.

- Use the authenticated agent user GID for the agent's assigned-task search.
- Use the server's search or typeahead tools to resolve named objects.
- If multiple results match, ask for clarification rather than guessing.
- If object type is unclear, search projects and teams, then inspect portfolios visible to the authenticated agent. Report the confirmed type and GID.
- An empty portfolio result only proves that the authenticated agent cannot see a matching portfolio. It does not prove the portfolio does not exist.

For a team question, resolve the team first and pass its GID to the team-project listing tool. For a portfolio question, use only read operations such as accessible-portfolio listing, portfolio retrieval, and portfolio-item retrieval.

## Find and Prioritize Work

- Find incomplete tasks assigned to the authenticated agent user GID.
- Do not browse the entire workspace unless the assigned task clearly requires a wider, approved search.
- Prioritize urgent or high-priority work, work blocking other agents, near-due items, then older actionable work.
- Before starting, inspect dependencies and blockers. Skip blocked work unless asked to diagnose the blocker.
- Do not use a generic “My Tasks” view unless the identity preflight passed for this exact agent.
- Do not duplicate work already active by another person or agent unless directly assigned or explicitly directed to continue.

## Action Boundaries

| Level | Allowed work | Approval rule |
| --- | --- | --- |
| Safe | Read assigned tasks, comments, subtasks, attachments, dependencies, and task-level custom fields. Add concise evidence-based progress comments. | No extra approval after preflight. |
| Normal | Update the assigned task, complete it when done criteria are met, upload relevant evidence, create a small follow-up subtask, or add a needed follower. | Do only when it directly supports the assigned task. |
| Risky | Move one task between existing sections, update a task-level custom field, alter a dependency, reassign a task, or change one due date. | Require explicit task instruction, clear work necessity, or Jack's approval. |
| Restricted | Bulk changes, deletes, project or portfolio changes, team membership, project status updates, project briefs, and custom-field administration. | Stop and route to `z-advanced-asana-control` with approval. |

When custom fields are required, enumerate the available fields first. Use field GIDs and enum-option GIDs. Never invent values or options.

## Execute the Assigned Work

- Add a short `Starting work` comment when beginning material work.
- Move or set the task to `In Progress` only when the project already uses that status and the change is within the approved action boundary.
- Keep comments concise, factual, and tied to the expected outcome.
- Use valid `html_notes` or `html_text` only when rich text is necessary.
- For a reliable mention, add the person as a follower first, wait briefly for propagation, then use the MCP-supported Asana mention markup.
- Attach relevant proof or output when it materially supports review. Do not use project-brief attachment or inline-image workflows under this Skill.

## Apply the Operating Mode

In **Get-er-Done Mode**, execute the smallest useful version, test it in the real workflow, post proof, and complete the task only when its done criteria are met.

In **Diagnose Mode**, follow Diagnose, Solution, Confirmation, Act. Investigate and explain the safe options, then stop for confirmation before changing Asana. If a material new risk appears during action, stop and return to this sequence.

## Complete and Verify

Before completing a task:

- Confirm the stated done criteria and check dependencies or follow-up work.
- Add a final comment with the result and proof or relevant links.
- Create or explicitly identify needed follow-up work without duplicating an existing task.
- Complete the assigned task only after all prior checks pass.

Record enough evidence to show the approved identity, intended task, action taken, test or result, and completion status. Keep secrets, private PAT values, and unnecessary personal data out of Asana comments, prompts, Notion, GitHub, and logs.

## Recurring Checks and Failures

For recurring agents, use event or sync-token discovery when the approved route supports it. Store sync tokens only in approved runtime state, never in prompts, comments, Notion, GitHub, or the Skill.

If a tool call fails, check the approved route, identity, workspace, GID resolution, MCP registration, token injection, permissions, and rate limits. Do not fall back to `notion-rest` or direct Asana REST for normal task execution. Direct REST is diagnosis-only, requires Jack's approval, and must use the same approved agent authority.

Stop after three failed attempts or earlier when the error indicates identity, authorization, permission, or scope failure. Report the observed error, attempted safe checks, current stop condition, and decision required.

## Final Verification

Confirm that the approved PAT MCP was used, the authenticated identity and workspace matched, all objects were resolved to GIDs, the action stayed within the allowed level, evidence was added, and no credentials or restricted changes were exposed or made.
