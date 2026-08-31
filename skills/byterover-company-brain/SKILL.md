---
name: byterover-company-brain
description: Query accepted context and submit knowledge to a ByteRover Company Brain.
---

<!-- byterover-brain-skill-version: 8 -->

# Use the Company Brain

1. Call `brain__query` before answering a company-specific question. If the host defers MCP tools, use tool discovery to load and then invoke `brain__query`; finding the tool is not a query result.
2. For a company brief or broad question, call `brain__query` with `{}` first. This overview names readable Brains and the Brain that answered. Follow `nextCursor` with `{ cursor }` for at most three pages. If `hasMore` is true but `nextCursor` is null, say that stable continuation is unavailable.
3. For a focused lookup, use one concise, distinctive name or concept. Use `budget: "small"` for a narrow answer, `"medium"` by default, and `"large"` only for broad context. Do not copy a long user question or combine unrelated categories into one query.
4. Use `brain__query({ objectId })` when you need the complete accepted object named by an earlier result. Do not combine `objectId` with `q`, `type`, `limit`, `cursor`, or `operationId`; `brain` and `budget` may still select its source and envelope.
5. Send `brain` only when the user names a specific readable Brain. Use its exact id or name from the overview. Never guess a Brain id.
6. Base claims attributed to the Company Brain only on returned objects. Distinguish missing context from a contradictory fact. Never fill a gap by guessing.
7. Include useful source labels and the returned Brain revision when they help the reader verify the answer. If `brain__query` is unavailable after tool discovery, report that ByteRover Brain is not loaded in this agent session. If `brain__query` or `brain__learn` returns HTTP 401, `invalid_token`, or `invalid_grant`, report that ByteRover Brain is not authenticated, use the host's MCP login flow, and retry. Never ask for Company IDs, credentials, API endpoints, or local paths.
8. `brain__query` reads accepted context only. Do not claim that a missing statement is accepted Brain knowledge.
9. Use `trigger: "user"` only when the user explicitly asks to save that exact statement. For knowledge detected by the agent, use `trigger: "agent"`, include a short safe `context`, and include `contextOperationId` when the statement came from an earlier Brain query. Never infer or expand the statement.
10. Claim that the Brain changed only when the outcome is `added` or `updated`. For `queued`, use `brain__query({ operationId })` later to check status. For any other outcome, say that the statement was not saved and include the returned reason. If the tool returns `insufficient_scope`, reconnect and grant `brain:learn`.
