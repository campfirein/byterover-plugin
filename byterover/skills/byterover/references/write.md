# Write

Use `write` only when the user asks to upload a complete file.

- A new path creates a document.
- The same path in the same drive creates a new revision of that document.
- Send the whole file. Do not edit, patch, or replace part of existing content.
- The current MCP transport accepts source files smaller than about 768 KiB. Do not claim that this MCP release can
  upload the product's full 1 GB file limit.
- Return the document ID, revision, and ingest state reported by the tool. Do not poll, and do not claim the revision is
  searchable before the returned state is `searchable`.

Backend RBAC decides whether the current user can write to the target. Do not infer or widen that permission.
