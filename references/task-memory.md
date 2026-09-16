# Asana Activity Memory: Routing and Verification

Use the currently installed provider and tools. Tool names below are examples of known integrations, not permission to invent an unavailable tool or parameter. Inspect the exposed schema and existing approved configuration when necessary. Never print credentials.

## Common Record and Ownership Rules

- Identify the business agent that owns the Asana task, not merely the session's internal worker ID.
- Resolve the approved bank/user/agent scope used by that owner's normal chats before writing. Retain existing sharing and privacy boundaries; do not merge banks or change provider configuration.
- Keep task GIDs and exact output links in the record so similar tasks and shared-bank entries can be distinguished.
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
