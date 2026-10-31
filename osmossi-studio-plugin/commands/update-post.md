---
description: Change, move, mark as ready/posted, or delete a post in the Osmossi calendar
argument-hint: "[which post and what to change — e.g. 'mark the Bum Bag carousel as posted']"
---

Use the osmossi-studio skill.

Change in the Osmossi calendar: $ARGUMENTS

1. Find the post: query `posts` and match on title, date, platform or products. If more than one matches, list them and ask which.
2. Read it (`get`) to have its current `version`.
3. Apply only the requested change with `update` (include `updatedAt`) pinned with `if_version`. For several posts at once, use one `batch`.
4. For a delete, show the post and get a yes first unless the user named it exactly.
5. Confirm what changed in one line and give the app link.
