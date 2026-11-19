Synthetic example — invented data, not a real customer.

# Our app returned a booking reference. Was the job done?

## What it looked like

Across 1 session, 5 of the 6 calls came back without an error. A success total alone would not show where the session took a wrong turn.

## What actually happened

1. The session used `list_tasks`, which lists open tasks, although the sample goal was to book an appointment. [(see record 1)](log.jsonl#L1)
2. `find_slots`, which finds appointment times, rejected the word “thirty” as the appointment length. [(see record 2)](log.jsonl#L2)
3. A linked retry used 30 minutes and returned 2 time options. [(see record 3)](log.jsonl#L3)
4. `get_slot`, which looks up a time option, returned the chosen option’s reference. [(see record 4)](log.jsonl#L4)
5. `reserve_slot`, which requests a booking, returned a booking reference. [(see record 5)](log.jsonl#L5)
6. `get_booking`, which looks up a booking, returned that same reference. [(see record 6)](log.jsonl#L6)

## What this means

- The first tool choice did not match the sample’s stated goal.
- The search error was a wrong value, not evidence of an outage.
- The next search succeeded after the value changed; the earlier error still matters.

## The decision

> **One test to try**
>
> Try adding “Task lists only; not appointment bookings” to the task tool’s description. Repeat the same booking test and check whether it still picks the task tool first.

## What this can't tell you

Requests where no tool was called are invisible in this log.  
The outcome is **unknown**: the log does not record whether the user got what they needed.

## See the evidence

| Step | Record | What it shows |
| --- | --- | --- |
| 1 | [Record 1](log.jsonl#L1) | Open tasks were fetched instead of appointment times. |
| 2 | [Record 2](log.jsonl#L2) | A word was rejected where a whole number was required. |
| 3 | [Record 3](log.jsonl#L3) | The corrected search returned time options. |
| 4 | [Record 4](log.jsonl#L4) | The selected time option was looked up. |
| 5 | [Record 5](log.jsonl#L5) | The booking request returned a reference. |
| 6 | [Record 6](log.jsonl#L6) | The booking lookup returned the same reference. |

Made by WhyThread — we're learning how MCP app owners understand what agents do with their apps.  
Questions or thoughts: reply in the thread that linked you here.
