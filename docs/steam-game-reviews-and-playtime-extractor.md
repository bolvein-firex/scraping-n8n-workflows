# Steam Game Reviews & Playtime Extractor: free n8n workflow

A free n8n workflow that runs the [Steam Game Reviews & Playtime Extractor](https://apify.com/dataspryva/steam-game-reviews-and-playtime-extractor) Apify Actor and returns `gameTitle`, `rating`, `reviewText`, `authorName`, `authorPlaytimeForever` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Steam game reviews scraper
- Platform: Steam
- Workflow file: [workflows/steam-game-reviews-and-playtime-extractor.json](../workflows/steam-game-reviews-and-playtime-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/steam-game-reviews-and-playtime-extractor.json`)
- Actor: https://apify.com/dataspryva/steam-game-reviews-and-playtime-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/steam-game-reviews-and-playtime-extractor/SKILL.md

## What it does

Pull Steam customer reviews for any game by URL or name, with thumbs up/down verdicts, reviewer playtime, helpfulness votes, and language filters.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | reviews | reviews = one row per review; gameSummary = one row per game with metadata and overall score. |
| `appIds` | array | no | [] | Numeric app IDs, store URLs, community review URLs, or old appreviews URLs. Example: 1174180 or `https://store.steampowered.com/app/1174180/` |
| `startUrls` | array | no |  | Steam store page URLs for the games to scrape. Merged with appIds. |
| `gameNames` | array | no | [] | Search Steam by name. An exact case-insensitive title match is preferred over the first search result. |
| `maxReviews` | integer | no | 50 | Reviews to collect per game. Use 0 for every matching review (hard safety cap 1,000,000 per game). |
| `maxGames` | integer | no | 0 | Cap the merged game list. Use 0 for no cap. |
| `reviewType` | string | no | all | Filter reviews by recommendation verdict. |
| `language` | string | no | all | Steam language code for review text. Select All Languages to include every language. |
| `sortBy` | string | no | recent | recent and updated walk the full history; helpful is a ranked sample inside the helpfulness window; funny is also ranked and not exhaustive. |
| `helpfulWithinDays` | integer | no | 30 | Only for sortBy=helpful: rank reviews from the last 1-365 days. Use recent for full history. |
| `purchaseType` | string | no | all | Whether the reviewer acquired the game through Steam, outside Steam, or either. |
| `minPlaytimeHours` | integer | no | 0 | Minimum hours played at the time of review. Use 0 for no minimum. |

7 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "startUrls": [
    {
      "url": "https://store.steampowered.com/app/1174180/Red_Dead_Redemption_2/"
    }
  ],
  "maxReviews": 25,
  "mode": "reviews"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxReviews` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `gameTitle` | Game |
| `rating` | Rating |
| `reviewText` | Review |
| `authorName` | Author |
| `authorSteamId` | Author ID |
| `authorPlaytimeForever` | Playtime (hrs) |
| `votesHelpful` | Helpful Votes |
| `timestampCreated` | Date |
| `language` | Language |
| `steamPurchase` | Steam Purchase |
| `primarilySteamDeck` | Steam Deck |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/steam-game-reviews-and-playtime-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
