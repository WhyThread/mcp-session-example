# MCP Session Triage

A free browser worksheet for reviewing one MCP tool-call log. Inspect explicit errors and retries, mark which calls fit the task, and download a short Markdown note.

**No signup, API key or model call.** The example is invented. The worksheet does not establish whether the user completed their task.

## Try it

[Open the browser worksheet](https://whythread.github.io/mcp-session-example/worksheet/) or [browse the free resources](https://whythread.github.io/mcp-session-example/). No account is needed.

To run it locally, from this directory:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open <http://127.0.0.1:8000/worksheet/>. The six-call sample is already loaded. Stop the server with Ctrl+C when finished.

1. Read the sample task and inspect the first call. Its wrong-tool annotation was written for this invented scenario.
2. Follow line 2's argument error to the explicit retry on line 3.
3. Mark relevance yourself, then select or download the review note.

Most logs need converting to the [documented shape](docs/format.md) first. Raw MCP JSON-RPC messages are not imported directly; for example, this reader expects an explicit status on each tool-call record, not nested inside a response envelope. Conversion is manual in this version. Remove secrets and personal data before loading a file.

## What it shows

- Explicit recorded statuses, including unknown or conflicting status.
- Valid `retry_of` links to an earlier error from the same tool/source.
- Exact string reuse between recorded return values and later arguments. A match does not prove causation.
- Your relevance judgments and separately supplied notes.

Read the [worked example](docs/worked-example.md), [short guide](worksheet/session-triage-guide.md), or the exact [six source records](log.jsonl). The [browser guide](worksheet/session-triage-guide.html) works from the local server.

## What remains unknown

The file cannot show a request that made no tool call, recover the whole conversation, or establish task completion. It does not automatically detect the wrong tool or explain why a model selected one.

The worksheet runs in your browser and does not upload your log, call a model, or use cookies or browser storage. Your browser may restore form text. Hosting still receives ordinary page requests, and optional external links open separate sites.

## Contribute

Useful contributions include small synthetic examples, a reproducible parser bug, a clearer explanation or an accessibility fix. See [CONTRIBUTING.md](CONTRIBUTING.md). Do not post private logs, credentials or customer records in issues.

## About

Made by [WhyThread](https://whythread.com/?utm_source=github&utm_medium=referral&utm_campaign=session_triage). The worksheet works independently of the product. AI tools assisted with implementation and review.

## License

[MIT](LICENSE).
