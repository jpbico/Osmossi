---
description: Show what is planned in the Osmossi posting calendar (this week by default)
argument-hint: "[this week | next week | November | 2026-11-01 to 2026-11-15]"
---

Use the osmossi-studio skill.

Show the Osmossi posting calendar for: $ARGUMENTS (if empty, this week, Monday to Sunday, New York time).

1. Query the `posts` collection for that date range (`where` on `date` with `>=` and `<=`, `order_by` `date`).
2. Show a short table: date, time (12-hour), platform, format, title, status. Mark today's posts.
3. Under the table, list in one line each: posts still at "idea" that go out in the next 3 days, and any Instagram post missing a caption.
4. End with the app link.
