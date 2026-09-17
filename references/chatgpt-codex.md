# Direct user-authorized Asana work
This route applies only to a direct request from the signed-in user through an approved ChatGPT/Codex connection. It is not an alternate route for another agent's assigned work.

## Verify authority
- Call the connector's current-user tool and verify the returned identity and intended workspace against the user's assignment.
- For Jack-authorized work, verify that the connected account is Jack's expected account; a connector name alone is not proof.
- Record the acting account separately from the assistant author. Cody is the Codex agent identity; actions through Jack's connection are account actions authorized by Jack.
- If the user asks what Amanda did, to process an agent's inbox/queue, or to work as a named agent, use that agent's own approved route. Do not relabel the work personal to bypass this boundary.
- Do not request a new PAT for the native connector route. Stop for the actual missing connection, identity, workspace or capability instead.

## Execute and verify
Apply the shared skill's GID resolution, scope, action boundaries, operating mode, evidence and completion checks.
Use z-asana-procedures for routine setup/release quality and z-advanced-asana-control for structural or bulk work.
Use the connector's available current schema, not hardcoded OpenClaw tool names.
For task discovery distinguish tasks assigned to the connected user from tasks explicitly named by the user. Do not silently process an entire personal queue.
If a connector write times out, inspect the exact object before retrying. Never create duplicate tasks to recover a lost response.

## Memory and records
Keep required task progress and completion evidence on the authorized task.
Use an external activity-memory provider only if it is available, approved for this context and permitted by host/user instructions. Do not apply OpenClaw worker-memory requirements to personal Codex memory or change a memory system to satisfy this skill.
Do not automatically write Codex's personal memory; obey its explicit permission rules.
Report task outcome and any required but unconfirmed record separately. A missing optional provider does not undo completed business work.
