# Input format and limits

Most exported logs need converting first. This worksheet does not import raw MCP JSON-RPC envelopes or automatically join request/response pairs. Conversion is manual in this version.

Supply one normalized JSON object per physical line. Each record needs a nonempty `tool`, `tool_name` or `name` string. The exact invented example is [log.jsonl](../log.jsonl).

```json
{"tool":"find_slots","session_key":"invented-a","server":"invented-server","args":{"duration_minutes":"thirty"},"ok":false}
{"tool":"find_slots","session_key":"invented-a","server":"invented-server","args":{"duration_minutes":30},"ok":true,"retry_of":1}
```

These are invented records, not a required MCP protocol message format.

- Argument objects: `args`, `arguments`, `params` or `input`.
- Return fields: `returned_ids`, `result` or `output`.
- Status: explicit `ok` or `isError` booleans; a nonempty `error` also flags an error. A result on its own is not a success status. Missing status stays unknown; conflicting fields are flagged.
- `retry_of`: a 1-based physical line number pointing to an earlier error for the same tool/session. Different explicit session IDs invalidate the link. A missing session ID leaves source identity unverified. Repeated names alone do not establish a retry.
- String matches: exact strings of 4–200 characters in return fields and later arguments. Common words can match too. Numbers are not compared. Matching is limited to six nested levels, 250 strings per field and 24 matches per record; it is not exhaustive or a causal trace.

Maximum input: 2 MiB and 2,000 lines. Unreadable lines are listed as skipped with their physical line numbers. Counts cover accepted records only.

Remove secrets and personal data before import. Please use made-up examples in public issues.
