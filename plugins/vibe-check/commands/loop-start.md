---
description: Start a session-scoped recurring vibe-check quiz every N minutes (default 30)
argument-hint: [minutes e.g. 5]
---
Start a recurring quiz that runs the `/vibe-check:vibe-check` command on a repeating
interval, scoped to THIS session only.

Interval (minutes): read `$ARGUMENTS`.
- If it is a bare number (e.g. `5`), treat it as minutes → `5m`.
- If it already has a unit (e.g. `90s`, `1h`), honor it as given.
- If empty, default to 30 minutes.

Steps:
1. If a vibe-check quiz loop is already running in this session, cancel it first (so
   re-running this command simply changes the interval).
2. Start the loop by running: `/loop <interval> /vibe-check:vibe-check`
   (use `/loop 30m /vibe-check:vibe-check` if no value was given).
3. Confirm to the user: the quiz runs every <interval>, it stops automatically when this
   session ends, and they can cancel early with `/vibe-check:loop-stop` or by pressing Esc.
