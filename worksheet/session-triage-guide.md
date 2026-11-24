# Six calls, five without errors. Did the booking work?

**Worked example: invented records, not a customer session or benchmark.**

[Open the worksheet](index.html) from a local static server, as described in the [README](README.md). Opening the file directly hasn't been verified. No account is needed. The sample is already loaded; you can also paste compatible JSONL or open a file on your computer. The page sends and saves no log data; your browser may restore form text. Remove secrets first. Optional links to external sites open separately.

## Start with the user's task

The sample goal is to reserve an appointment and receive a confirmation. There are six recorded calls, five with no error recorded. Those counts don't tell us whether the user got the appointment they wanted.

Write the task in a sentence before marking calls. A tool name alone doesn't tell us the user's intent.

## Check relevance separately from status

Line 1 calls `list_tasks`, even though the authored scenario is about a booking. Its response has no error. That makes it an example of a technically accepted call that doesn't fit the stated task.

Mark that row **Not relevant**. The page leaves that judgment to you; it doesn't detect wrong tool choices. For your own session, compare the selected tool's description with the one you expected. Look for vague or overlapping wording, then repeat the same task to see what changes.

## Follow the error and its explicit retry

Line 2 sends `"thirty"` as `duration_minutes` and records an invalid-argument error. Line 3 sends `30`, returns two time options, and explicitly links back to line 2 with `retry_of`.

The worksheet shows that value change. The useful check is whether the accepted type, unit and example are clear in the tool's input requirements. It doesn't prove which wording caused the error or that changing a description will fix it.

Repeated calls aren't automatically retries. Without a valid explicit link, keep that relationship unverified.

## Inspect the references without guessing what they prove

The booking reference returned on line 5 appears in the arguments of line 6. That's an exact value match between recorded fields. It helps you follow the supplied sequence, but it doesn't prove causation or that the agent used the result correctly.

Confirm the booking in the system that owns it and compare it with what the user asked for. A returned reference alone doesn't settle completion.

## Keep the missing evidence visible

This tool-call file doesn't show requests where no tool was called, the whole conversation, or activity outside the file. It can't reconstruct a docs-to-CLI-to-MCP journey by itself.

Add permitted transcript or outcome notes in the reviewer field. They stay labeled as your notes, with task completion unknown from the tool-call file alone. Copy or download the Markdown note to keep the evidence, your judgments and the limits together.

Compatible imports need one object per line and a tool name. The page documents the supported aliases, explicit status fields and retry-link convention. It lists skipped lines, and its counts cover accepted records only.

Made by WhyThread. [Exact synthetic source](https://github.com/WhyThread/mcp-session-example).
