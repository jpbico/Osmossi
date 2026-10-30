---
description: Add a post or Pin to the Osmossi posting calendar
argument-hint: "[what, where and when — e.g. 'Reel about the Macuira weave on Instagram next Tuesday at noon']"
---

Use the osmossi-studio skill.

Add this to the Osmossi calendar: $ARGUMENTS

1. Work out platform, format, date, time, title and products from the request. Use the skill's defaults for anything missing; ask only if the platform or the date can't be inferred.
2. Query `posts` on that date first. If a post with the same platform and a similar title exists, ask whether to update it instead.
3. If the user asked for a caption or Pin description, write it following the brand rules.
4. Create the document with `set` (new id `post-YYYYMMDD-short-slug`, all fields, `status: "idea"` unless told otherwise).
5. Confirm in one line and give the app link.
