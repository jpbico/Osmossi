# Osmossi Studio plugin for Cowork

This plugin lets Claude in your Cowork project operate the **Osmossi Studio** app
(https://claude.ai/artifact/8sG5GhyLZu3ptF4RH1jtUY): the posting calendar, the trend notes and the store report.

Changes Claude makes show up in the app right away for everyone who has it open.

## What you can ask

| Command | What it does |
|---|---|
| `/osmossi-studio:calendar` | Shows what's planned (this week by default) and what still needs work |
| `/osmossi-studio:add-post` | Adds a post or Pin, e.g. "Reel about the Macuira weave next Tuesday at noon" |
| `/osmossi-studio:update-post` | Moves, edits, marks ready/posted, or deletes a post |
| `/osmossi-studio:plan-pins` | Plans Pinterest Pins that reuse your Instagram posts |
| `/osmossi-studio:refresh-trends` | Researches Google, Pinterest, Etsy and Amazon trends and updates the Trends tab |
| `/osmossi-studio:store-report` | Plain-language Shopify report with next steps |

You don't have to use the commands: asking in plain words ("what's going out this week?",
"mark the Bum Bag carousel as posted") works too, because the plugin's skill teaches Claude how the app's data is organized.

## Install

1. Download `osmossi-studio-plugin.zip`.
2. In the Claude desktop app, open Cowork's plugin settings and upload the zip.
   (Team and Enterprise admins can instead add it to the organization's plugin marketplace so everyone gets it.)
3. Make sure **Shopify** is connected in claude.ai **Settings → Connectors** for the store report.
4. In your Osmossi project, try: `/osmossi-studio:calendar`.

To install from GitHub instead (Claude Code, or an organization marketplace that points at this repository):

```
/plugin install osmossi-studio --marketplace jpbico/Osmossi
```

The first time Claude changes the app's data, Cowork asks you to approve it.

## Requirements

- Claude must be able to open the app: it uses your claude.ai account, so the people using the plugin need access to the app (share it from the app's Share menu).
- Writing to the calendar needs edit or Contributor access to the app.
- Trend refreshes use web search.

## How it works

The app keeps its data in claude.ai's database for that artifact, in two collections:
`posts` (calendar) and `trends` (trend notes). The full field list is in
`skills/osmossi-studio/SKILL.md`. Store numbers come live from the Shopify connector.
