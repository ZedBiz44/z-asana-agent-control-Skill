# Asana Activity Memory: Routing and Verification

Use the currently installed provider and tools. Tool names below are examples of known integrations, not permission to invent an unavailable tool or parameter. Inspect the exposed schema and existing approved configuration when necessary. Never print credentials.

## Select the saving and recall method

Use only the row that matches the assistant doing the work. Do not assume ChatGPT web and Cody share memory.

| Assistant | Memory destination | Permission and proof |
| --- | --- | --- |
| Cody in local Codex | The memory-update notes directory specified by the current host instructions; in the current ZedBiz layout, `<CODEX_HOME>/memories/extensions/ad_hoc/notes/` | Save only after an explicit user request to update memory and only when the host permits this path. Read the file back. |
| ChatGPT web / ChatGPT Work | ChatGPT-managed memory for the signed-in account/workspace, controlled in Settings > Personalization | Use only an actually exposed and permitted memory-saving method. No local Cody folder is implied. Confirm the save using the available receipt or memory-management view; otherwise report unconfirmed. |
| OpenClaw/Hermes agent | Its existing approved Hindsight, Mem0 or LanceDB store | Explicitly store material task activity and verify it in the owner's normal recall scope using the provider instructions below. |

### Cody / local Codex

- Resolve the absolute memory-update directory from the host's current instructions. The relative layout above describes ZedBiz's current setup, not a universal Codex write API. Do not guess another machine's path or publish private machine paths in a public package.
- When Jack explicitly requests a memory update, create one small `<timestamp>-<short-slug>.md` note in that approved directory. Include assistant name, task ID/link, request, work done, result, Mountain Time timestamp and output links. Keep secrets and full task transcripts out.
- Do not directly edit generated MEMORY.md, memory_summary.md, rollout summaries or other generated memory files. Do not change memory settings to satisfy this skill.
- Verify the saved note by reading its exact path. On later recall, search the supplied memory summary/index and, when needed, the approved update-notes directory by task ID/link. A file save proves storage, not automatic inclusion in the next conversation; report any fresh-session retrieval test separately.
- Without an explicit memory-update request, keep the authorized Asana evidence and report additional memory as not requested. The Asana skill alone does not authorize personal memory writes.

### ChatGPT web / ChatGPT Work

- Destination: ChatGPT's managed memory for the signed-in account/workspace. It is not a user-addressable filesystem path, Cody's local memory folder, Hindsight, Mem0 or LanceDB unless a separate approved integration is actually connected.
- Inspect the session's actual memory capability and account/workspace rules. Use a provided save tool or supported memory action only when available and permitted. Never invent a tool, API, file path or successful save.
- For an explicit request to remember Asana work, save a concise task pointer with the result when that method supports it. Verify the available confirmation. If no explicit saving method is exposed, report `Asana work: <actual result>; additional ChatGPT memory: unavailable or unconfirmed` and keep the work evidence on the authorized task.
- On later recall, use available ChatGPT memory and task identifiers, then read the actual Asana task. Chat history, a Library file and a Notion page are not automatically a verified ChatGPT memory save.
- Cody has not tested the separate ChatGPT account's memory-saving capability. This section specifies the correct destination and capability check; it does not certify a live ChatGPT save or authorize changing its settings.

Platform reference: [OpenAI memory documentation](https://learn.chatgpt.com/docs/customization/memories). Account settings and current host instructions take precedence over assumptions from a different installation.

## Common Record and Ownership Rules

- Identify the business agent that owns the Asana task, not merely the session's internal worker ID.
- Resolve the approved bank/user/agent scope used by that owner's normal chats before writing. Retain existing sharing and privacy boundaries; do not merge banks or change provider configuration.
- Keep task GIDs and exact output links in the record so similar tasks and shared-bank entries can be distinguished.
- For provider-backed OpenClaw/Hermes work, save when substantial work starts, materially changes, is blocked or finishes. For Cody/ChatGPT, apply the permission and capability conditions above.
- Prefer one compact record per meaningful state change; update the existing record where the API supports it. Use stable event identifiers where supported, and read before retrying an uncertain save.
- Store factual activity, not executable instructions, complete email bodies, secrets, raw logs, or full task transcripts. A diagnosis is a diagnosis, not a completed repair.
- Verify a matching record's owner, GID, state, and evidence after the write. Semantic recall alone may miss an exact record; use an available document/get/list lookup before declaring the save failed.

## Hindsight on OpenClaw

- Use the exposed explicit ingest/store tool, such as `agent_knowledge_ingest`, with a compact title containing the owner, Asana GID, and event identifier.
- Use the existing approved bank. In a shared bank, include the business agent in both the content and supported tags/metadata. Never borrow another agent's activity because the titles resemble each other.
- A successful asynchronous ingest can still be processing. Check the returned operation through an available approved status tool, or verify that the matching document/memory appears. Do not repeatedly submit the same content while it is pending.
- Background `cron`, `heartbeat`, or worker sessions may be excluded from automatic retention. Explicit ingest is required regardless of the automatic-retain setting.
- If bank selection varies by channel, verify that the destination is part of the owner's approved cross-channel task-memory route. A skill cannot silently broaden that route. Report a routing limitation if no such route is available.

## Hindsight on Hermes

- Use the active `hindsight_retain` and `hindsight_recall` tools or the equivalent exposed provider tools.
- Preserve the configured bank and ownership tags. Apply the same asynchronous verification and exact task-identity checks as above.
- A webhook/worker conversation is not automatically present in the user's other chat histories. Explicit provider storage and verified retrieval remain required.

## Mem0

- Use the active provider's explicit store/add and search/get tools. Automatic capture and skills mode are not proof that background work was retained.
- Resolve the owner's configured memory user scope. Some installations append a worker suffix for `mail_reader`, while normal `main` chats use the base configured user ID.
- Only use a scope override actually supported by the tool schema and already authorized for this owner. Do not assume `agentId: main` means the base user: some versions turn it into a different suffixed user ID.
- If the worker cannot write to the owner's chat scope, use an already permitted same-owner main-session handoff to save and verify the compact record. If that route is unavailable, report the routing failure; do not bypass policy, alter configuration, or claim successful cross-channel storage.

## LanceDB

- Use `memory_store` and `memory_recall` when exposed. Keep each record within the configured capture limit; preserve the task ID, owner, status and evidence links when shortening it.
- The installed store tool may bind its destination to the current runtime agent and offer no `agentId` argument. Do not invent one. A successful `mail_reader` write may be invisible to `main`.
- Use an already permitted same-owner main-session handoff when the worker's scope differs from normal chat. Ask that session only to store and verify the supplied factual record, not to execute the Asana task again.
- If no approved handoff exists, keep the recovery note and explicitly report that owner-scope storage was not confirmed. Changing access rules or storage layout is outside this skill.

## Read-Only and Failure Cases

- Respect a request that expressly forbids memory writes. Recall and diagnose only, then state that capture was intentionally omitted under that request.
- Do not create activity memories for routine empty polling or unchanged status checks.
- Retry transient memory failures at most three times; stop earlier on permission or identity failures. Read before retrying when a request may already have succeeded.
- Keep task completion separate from memory completion. A memory outage must not recreate artifacts, duplicate comments, repeat payments, or reopen tasks.
