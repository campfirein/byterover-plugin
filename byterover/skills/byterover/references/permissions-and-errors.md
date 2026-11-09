# Permissions and errors

Backend RBAC resolves the current drive scope for every request. The MCP server does not store roles, drive lists, or
separate permissions. A user with no assigned drive has an empty scope.

- `unauthenticated`: let the host start OAuth again.
- `forbidden`: report that current RBAC does not allow the request. Do not widen scope or try another drive.
- `not_found`: report the missing document or evidence without invention.
- `conflict`: refresh the selected document evidence before retrying the same read.
- `rate_limited`: retry after the returned delay when present.
- `drive_unavailable`, `model_unavailable`, or `timeout`: report the temporary failure and retry only when appropriate.

Never turn an error into a permission change. Never poll for ingest completion.
