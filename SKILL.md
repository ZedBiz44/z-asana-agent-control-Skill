---
name: z-asana-agent-control
description: "Do routine ZedBiz Asana work through the runtime's approved connection: ChatGPT's connected Asana plugin or an OpenClaw agent's PAT-backed MCP. Verify the applicable identity, task boundary, evidence, and completion."
---

# Z Asana Agent Control

## Use This Skill

Use for day-to-day Asana work owned by a ZedBiz AI agent, including assigned-task discovery, task reading, evidence-based progress comments, completing finished work, and read-only team or portfolio navigation required by that work.

Apply this Skill before any Asana query or update. Use the approved route for the runtime:

- **ChatGPT/Codex:** use the connected Asana plugin. A connection authenticated as Jack is expected and approved when Jack asks ChatGPT to inspect or change Asana within the current request.
- **OpenClaw team agent:** use that agent's approved PAT-backed Asana MCP. Do not substitute Jack's ChatGPT connection or another agent's identity.

Also use this Skill when an email or background job starts Asana work, or when someone asks what you did, why you did it, or what you are working on in Asana. Read this Skill in that run; a separate chat's earlier skill load does not count.

## Do Not Use This Skill

Do not use for project setup, project briefs or status updates, workflow redesign, portfolio changes, timeline-wide changes, custom-field administration, team-membership changes, bulk updates, deletes, or other structural Asana administration. Route those requests to `z-advanced-asana-control` and obtain the required approval.

Do not use ChatGPT's Asana plugin to impersonate an OpenClaw team agent or claim that agent performed the work. Do not use browser automation or direct REST when the approved runtime route is available.

## Required Context

Confirm the runtime and its required context before task work:

- **ChatGPT/Codex:** connected Asana plugin, connected workspace/account identity when exposed, requested project or task, and required capabilities.
- **OpenClaw:** agent name, approved agent email and user GID, approved workspace GID, and approved PAT-backed Asana MCP server.

Stop if the applicable route is unavailable, the required workspace or target cannot be verified, or the runtime is trying to use the other runtime's authority. Do not guess identifiers or credentials.

## Required MCP Capabilities

Before accepting the requested work, inspect the approved route's exposed tools. Confirm the exact reads and writes required by the request. For OpenClaw assigned-task execution, also confirm current-user and assigned-task discovery. Confirm search or typeahead for named objects when available; otherwise use exact links or IDs supplied by the user and read them back.

If the requested capability is absent, stop and report it. Do not substitute browser automation, unapproved direct REST, the other runtime's connection, or a guessed endpoint.

## Preflight Identity and Route

For **ChatGPT/Codex**:

- Use the connected Asana plugin selected for the session.
- Read the connected account/workspace identity when the plugin exposes it. A Jack-authenticated connection is valid for Jack's request.
- Use supplied Asana links or exact IDs to resolve targets. Confirm the project/task belongs to the intended workspace before writing.
- Record that ChatGPT used the connected Asana plugin; do not claim an OpenClaw agent identity.

For an **OpenClaw team agent**:

- Confirm the active server is that agent's approved PAT-backed Asana MCP.
- Call `asana_get_user` with `user_gid: "me"`, or the exposed current-user equivalent.
- Continue only when the returned email, user GID, and workspace match the approved agent configuration.
- Record the authenticated agent identity, workspace, and route in the work evidence. Never record a PAT.

Use this failure message when the applicable authority check fails:

> Asana work stopped. The connected runtime route, identity, workspace, or requested target could not be verified. Fix the applicable ChatGPT Asana connection or OpenClaw agent MCP before execution continues.

For OpenClaw Streamable HTTP deployments, a successful `/healthz` check may supplement but never replace the identity read. Do not treat a legacy SSE probe returning HTTP 400 as proof that an otherwise working Streamable HTTP route is unusable.

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
- Do not use a generic “My Tasks” view unless the applicable connected identity is known. Prefer the exact project/task supplied by Jack for ChatGPT work.
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
- Save a compact `In progress` activity record to the active external memory provider using the rules below. Save important progress, changed plans, and blockers when they occur.
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
- Read back the actual task status, then save and verify the final external-memory activity record. Do not record `Complete` before Asana confirms completion.

Record enough evidence to show the runtime route, intended task, action taken, test or result, and completion status. Keep secrets, private PAT values, and unnecessary personal data out of Asana comments, prompts, Notion, GitHub, and logs.

## Save Task Activity to External Memory

This is a required explicit tool action, including in email-triggered, scheduled, and background sessions. An Asana comment, final chat reply, local daily note, or automatic conversation capture is not a substitute.

- Use the agent's existing active external memory provider. Follow [provider routing and verification](references/task-memory.md); do not install or reconfigure a provider for this step.
- Save when substantial work begins, the status or next action materially changes, work is blocked, or work finishes. Do not save every lookup, empty task check, trivial comment, or repeated notification.
- Include the owning agent's name, task GID and link, what was requested and why (only if known), actions actually taken, current status, output/evidence links, timestamp with timezone, and next action or blocker.
- Use an existing task record or a stable agent/task/event identifier where supported. Search before retrying a save whose outcome is uncertain. Keep records concise and within the provider's size limit.
- Verify the write response and read the matching record back. For asynchronous saves, confirm processing completed or the record became available; an accepted queue item alone is not a completed save.
- Use the same approved task-memory scope that the owning agent's normal chats search. The internal worker name `mail_reader` is not the business agent's identity. Do not claim cross-channel recall merely because a write succeeded in a worker-only scope.
- If saving or routing fails, report `Task work: <actual status>; external memory: not confirmed — <reason>`. Preserve a compact recovery note in the existing approved task evidence or local runtime notes. Retry only the memory step within the normal retry limit; never repeat completed business actions or reopen a finished task just because memory failed.
- Do not publish new Notion/GitHub documents solely to replace a missing activity-memory save. Existing requirements for those systems still apply when the assignment calls for them.

Example record shape (replace every value with observed facts):

`Agent: <owner> | Asana: <GID and URL> | Requested: <short instruction/reason> | Action: <work actually done> | Status: <in progress/blocked/complete> | Evidence: <output URLs> | Updated: <ISO timestamp with offset> | Next: <action or none>`

## Recall Previous Asana Work

- Before explaining past work or resuming a task, search external memory using the task GID and owning agent. If the GID is unknown, use the task title, output title/link, and relevant date to identify candidates.
- Confirm task identity, agent ownership, timestamps, and output links. A similar task by another agent in a shared bank is not evidence that you did the work.
- Use the applicable ChatGPT-plugin or OpenClaw-MCP preflight before checking live task details, comments, or current status. Memory is historical context; the live task and verified outputs settle current facts.
- When recall is empty, inspect the specific task and permitted execution history. Do not conclude that no work occurred, or invent a reason for it. Say what is verified and what remains unknown.
- If you recover a missing material activity record, save a clearly labelled retrospective entry with the original work time when known and the current recording time. Do not invent missing details or duplicate a matching record.

## Recurring Checks and Failures

For recurring agents, use event or sync-token discovery when the approved route supports it. Store sync tokens only in approved runtime state, never in prompts, comments, Notion, GitHub, or the Skill.

If a tool call fails, check the applicable route, identity, workspace, GID resolution, plugin/MCP registration, OpenClaw token injection when applicable, permissions, and rate limits. Do not fall back to `notion-rest` or direct Asana REST for normal task execution. Direct REST is diagnosis-only, requires Jack's approval, and must use the same authorized runtime identity.

Stop after three failed attempts or earlier when the error indicates identity, authorization, permission, or scope failure. Report the observed error, attempted safe checks, current stop condition, and decision required.

## Final Verification

Confirm that ChatGPT used its connected Asana plugin or the OpenClaw agent used its approved PAT MCP, the applicable identity/workspace/target matched, all objects were resolved, the action stayed within the allowed level, evidence was added, and no credentials or restricted changes were exposed or made. For OpenClaw material work, report whether the external-memory record was verified in the owning agent's approved scope; never hide a failed save behind a successful task result.
