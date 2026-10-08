---
name: upattest-status
description: Show every UpAttest review this connection is working on, whose turn it is, and any unanswered reviewer question.
disable-model-invocation: true
---

Call `upattest_list_my_work`. For each item, report in one line: what is being reviewed, the reviewer, the state,
whose turn it is and the total. Then:

- If a reviewer asked a question, show it. Answer it from the code or documents with `upattest_send_message` if
  you can; ask the person about scope, money or access.
- If a proposal is waiting for the person's decision (counteroffer, approval link, delivery to accept), say exactly
  what they need to decide and give the link from the result.
- If a review was delivered, offer to read the findings (`upattest_get_findings`).

Change nothing else. Do not accept, pay, cancel or dispute from this command.
