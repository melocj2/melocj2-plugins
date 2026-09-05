---
description: Stop the recurring vibe-check quiz running in this session
---
Cancel the recurring vibe-check quiz loop in this session.

Steps:
1. Identify the active loop that fires `/vibe-check:vibe-check` (use the task id from when it
   was started if known; otherwise list the session's active scheduled loops and match it).
2. Cancel/delete that loop so it fires no more.
3. Confirm to the user it is stopped. If none was running, say so plainly.

Note: the user can also press Esc to stop a self-paced loop immediately, and any loop stops
automatically when the session ends.
