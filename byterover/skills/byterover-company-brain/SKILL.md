---
name: byterover-company-brain
description: Query accepted context from the selected Company Brain and create pending proposals when the user explicitly asks to save a statement.
---

<!-- byterover-brain-skill-version: 5 -->

# Use the Company Brain

1. Call `brain__query` before answering a company-specific question. If the host defers MCP tools, use tool discovery to load and then invoke `brain__query`; finding the tool is not a query result.
2. For a company brief or broad question, call `brain__query` with the empty input object `{}` first. Do not send `q`, `type`, or `limit` on this first call. If `hasMore` is true, call `brain__query` again with only `{ cursor: nextCursor }`. Continue until `hasMore` is false before treating the inventory as complete.
3. For a focused lookup, use one concise, distinctive name or concept. Do not copy a long user question or combine unrelated categories into one query. Do not substitute another MCP or local files for Company Brain context.
4. Use `brain__query({ objectId })` when you need the complete accepted object named by an earlier result. Do not combine `objectId` with other fields.
5. Base claims attributed to the Company Brain only on returned objects. Distinguish missing context from a contradictory fact. Never fill a gap by guessing.
6. Include useful source labels and the returned Brain revision when they help the reader verify the answer.
7. If `brain__query` is unavailable, report that the Company Brain connection is not loaded. Never ask for Company IDs, Brain IDs, credentials, API endpoints, or local paths.
8. `brain__query` reads accepted context only. Do not claim that a missing statement is accepted Brain knowledge.
9. Call `brain__learn({ statement })` only when the user explicitly asks to save that exact statement. Do not infer or expand the statement.
10. `brain__learn` creates a pending proposal for review in Grove. It does not accept, approve, update, or delete Brain knowledge. Report the pending state accurately.
