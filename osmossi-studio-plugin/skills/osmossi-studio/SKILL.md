---
name: osmossi-studio
description: Read and change the Osmossi Studio app (https://claude.ai/artifact/8sG5GhyLZu3ptF4RH1jtUY) — its Instagram and Pinterest posting calendar, its trend notes, and its Shopify store KPIs. Use whenever the user asks about Osmossi posts, the content calendar, what is scheduled, adding/moving/editing/deleting a post, marking a post ready or posted, refreshing or adding trends, or how osmossi.com is performing.
---

# Osmossi Studio

Osmossi Studio is a claude.ai artifact (a web app) that the Osmossi team uses for marketing:

- **App link:** https://claude.ai/artifact/8sG5GhyLZu3ptF4RH1jtUY
- **Calendar module** → database collection `posts`
- **Trends module** → database collection `trends`
- **Store results module** → live Shopify data (nothing stored in the app)

Whatever you write to `posts` or `trends` shows up live for everyone who has the app open. There is nothing to republish: never publish a new version of the page to change data.

## Tools to use

- **App data:** the artifact database tool (called `ArtifactData` in Claude Code and Cowork; some apps call its actions `read_db` / `write_db`). Every call takes `url: "https://claude.ai/artifact/8sG5GhyLZu3ptF4RH1jtUY"`.
  - Read: `action: "query"` with `collection` and an optional `query` (`where`, `order_by`, `limit`), or `action: "list"`, or `action: "get"` with `doc_id`.
  - Write: `set` (create or replace), `update` (merge fields), `delete`, and `batch` for more than two writes (one approval, all or nothing).
  - **Always pin writes to existing documents** with `if_version` set to the `version` you just read. If it fails because the document changed, read it again, merge your change into the new content, and write again. Omit `if_version` only when creating a new document.
- **Store data:** the Shopify connector, tool `run-analytics-query` (ShopifyQL). If it is not connected, tell the user to add Shopify in claude.ai Settings → Connectors.
- **Trend research:** web search. Never invent numbers.

If the artifact database tool is not available in this session, say so plainly and give the user the app link so they can make the change by hand. Do not guess at results.

## `posts` collection (calendar)

One document per post. Document id: `post-YYYYMMDD-short-slug` for new posts (lowercase, letters, digits and hyphens). Existing ids such as `ig-nov-01` or `pin-nov-03` stay as they are.

| Field | Type | Values |
|---|---|---|
| `platform` | string | `"instagram"` or `"pinterest"` (lowercase) |
| `status` | string | `"idea"`, `"ready"` (ready to post) or `"posted"` |
| `date` | string | `"YYYY-MM-DD"` |
| `time` | string | `"HH:MM"`, 24-hour, New York time (ET). May be `""` |
| `format` | string | Instagram: `"Reel"`, `"Carousel"`, `"Feed photo"`, `"Stories"`. Pinterest: `"Pin"`, `"Video Pin"` |
| `title` | string | Short name shown in the calendar, ≤ 120 characters. Required |
| `products` | string | Products and prices shown, e.g. `"Macuira collection ($199)"` |
| `caption` | string | Caption or Pin description, may be `""` |
| `notes` | string | Free notes, ≤ 400 characters |
| `updatedAt` | string | ISO timestamp of your write |

Rules:
- Write every field on `set`; use `update` to change only some fields, always with `updatedAt`.
- The app only knows the values above. A different `platform`, `status` or `format` breaks how the post is shown.
- To move a post, update `date` (and `time`); keep its id.
- When the user says "posted", set `status: "posted"`. When content is finished but not published, `"ready"`.
- Default times when none is given: Instagram Tue/Thu/Sat at 12:00, 19:00 or 10:00 (see the plan); Pinterest 20:00.
- Before deleting, show the user which post(s) will go and get a yes, unless they named the exact post.

## `trends` collection (trend notes)

One document per trend card. Ids `t1`, `t2`, … (use the next free number).

| Field | Type | Notes |
|---|---|---|
| `order` | number | Sort position on the page (1 = first) |
| `source` | string | Exactly `"Google"`, `"Pinterest"`, `"Etsy"` or `"Amazon"` (the page's filters use these) |
| `strength` | string | `"strong"` = the platform's own data; `"weak"` = third-party tool, a store page, or another country |
| `checked` | string | Date you checked it, e.g. `"Nov 12, 2026"` |
| `stat` | string | The headline number, e.g. `"+400% year over year"` |
| `headline` | string | What is trending |
| `meaning` | string | What it means for Osmossi, one or two plain sentences |
| `action` | string | One concrete thing to try |
| `url` | string | Source link (required) |
| `sourceName` | string | Who published it |

Rules: every stat needs a real source you found this session. Update a stale card in place (same id, new `checked`) rather than adding a duplicate. Delete a card only when the user asks or the trend is clearly over.

## Store KPIs (Shopify)

Useful queries (swap `-30d` for the period asked):

- Sales: `FROM sales SHOW orders, total_sales, average_order_value SINCE -30d UNTIL today COMPARE TO previous_period`
- Visits and conversion: `FROM sessions SHOW sessions, conversion_rate SINCE -30d UNTIL today COMPARE TO previous_period`
- Funnel: `FROM sessions SHOW sessions, sessions_with_cart_additions, sessions_that_reached_checkout, sessions_that_completed_checkout SINCE -30d UNTIL today`
- Traffic sources: `FROM sessions SHOW sessions GROUP BY referrer_source SINCE -30d UNTIL today`
- Best sellers: `FROM sales SHOW net_sales, orders GROUP BY product_title SINCE -30d UNTIL today ORDER BY net_sales DESC LIMIT 5`

`conversion_rate` comes back as a fraction (0.031 = 3.1%). Money comes as strings in USD. Explain each number in one plain sentence; the team is new to marketing.

## Brand rules (apply to anything you write into the app)

- Audience: Latina women living in the U.S. who value quality and tasteful details.
- Tone: warm, proud, plain. Say "handmade in small batches" and "each piece has its own subtle variations". Never "one of a kind" or "last one".
- Only state artisan and origin facts that are known. No blanket discounts; for Black Friday to Cyber Monday add value instead of cutting price.
- Sizes: Feed photo and Carousel 1080×1350 (4:5); Reel and Stories 1080×1920 (9:16); Pin 1000×1500 (2:3); Video Pin 6–15 s.
- Instagram posts go out Tuesday, Thursday and Saturday. Every product post links to a product page, not the homepage. Pins link to the product page on osmossi.com.
- Products and prices in use: Macuira collection $199, Half Moon $169, Pompoms Bag $169, Bum Bags $499, Mini Bag Victoria $488, Mini Bag Raining Gold $467, Rainbow Hat $159, Elegant Hat $149, placemats $37, Cielo wall décor.

## After every change

Tell the user in one or two lines what changed (post title, date, platform, status) and give the app link. If a write failed, say which one and why.
