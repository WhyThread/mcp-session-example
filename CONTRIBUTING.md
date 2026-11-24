# Contributing

Keep changes focused on helping someone inspect one supplied session accurately.

- Use a tiny invented JSONL example for a bug or proposed input alias. State the expected and actual behavior.
- Keep missing status unknown. Preserve explicit retry validation and the distinction between exact value reuse and causation.
- Keep relevance judgments separate from recorded fields. Do not infer task completion from successful calls.
- Preserve the no-upload, no-model-call behavior of the worksheet.
- For UI changes, check keyboard use and a narrow mobile viewport.

Do not include real customer logs, credentials, private URLs or personal data in an issue or pull request. A tool name and synthetic values are usually enough to reproduce a parser problem. If you cannot make a safe reproduction, describe the behavior without the data.

Start the local server using the README instructions. Try the embedded sample, your invented case, the generated note and the guide link. Explain the check you performed in your pull request.

No response-time or feature-delivery promise is made.
