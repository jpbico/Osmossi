---
description: Research current Google, Pinterest, Etsy and Amazon trends and update the Osmossi trend notes
argument-hint: "[optional focus — e.g. 'holiday gifts' or 'home decor']"
---

Use the osmossi-studio skill.

Refresh the Osmossi trend notes. Focus: $ARGUMENTS (if empty: what Osmossi sells — handwoven and beaded bags, palm hats, placemats and home décor, gifts for women — for the coming 4–8 weeks).

1. List the `trends` collection to see what is there and when each was checked.
2. Search the web for current evidence on each source (Google, Pinterest, Etsy, Amazon). Prefer the platform's own reports and trend tools; label third-party data `"weak"`.
3. For each finding, decide: update an existing card (same id, new `checked`, new numbers), add a new card, or leave it. Never add a number you didn't find a source for.
4. Show the user the planned changes (new, updated, unchanged) as a short list, then write them in one `batch` (pin `if_version` on updated cards).
5. Confirm and give the app link, then list the source URLs you used.
