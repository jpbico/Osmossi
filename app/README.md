# Osmossi Studio app

`osmossi-studio.html` is the source of the Osmossi Studio app, published on claude.ai at
https://claude.ai/artifact/8sG5GhyLZu3ptF4RH1jtUY

It has three modules:

- **Calendar**: Instagram and Pinterest posting calendar (month and list views, add, edit, delete, status).
- **Trends**: trend notes from Google, Pinterest, Etsy and Amazon, with links to each site's live trend tool and "Get post ideas".
- **Store results**: live KPIs from Shopify (sales, orders, average order, visits, conversion, funnel, traffic sources, best sellers).

## How it runs

The page is a single HTML file with no build step. It only works fully inside claude.ai, which provides these capabilities:

| Capability | Used for |
|---|---|
| `db` | Calendar posts (`posts` collection) and trend notes (`trends` collection) |
| `mcp` → Shopify `run-analytics-query` | Store results |
| `sample` | "Get post ideas" on trend cards |
| `user` | Who is viewing |

Opened as a plain file in a browser, the page still renders, and each module explains what it needs. The data fields are listed in `../osmossi-studio-plugin/skills/osmossi-studio/SKILL.md`.

## Updating the live app

Edit this file, then ask Claude to republish it to the artifact link above, keeping the same capabilities. The calendar and trend data live in the artifact's database, not in this file, so republishing doesn't change them.
