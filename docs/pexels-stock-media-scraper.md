# Pexels Stock Media Scraper: free n8n workflow

A free n8n workflow that runs the [Pexels Stock Media Scraper](https://apify.com/nimbryxo-studio/pexels-stock-media-scraper-2) Apify Actor and returns `title`, `photographerName`, `width`, `height`, `orientation` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Pexels stock media scraper
- Platform: Pexels
- Workflow file: [workflows/pexels-stock-media-scraper.json](../workflows/pexels-stock-media-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/pexels-stock-media-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/pexels-stock-media-scraper-2
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/pexels-stock-media-scraper/SKILL.md

## What it does

Scrape free stock photos and videos from Pexels. Search by keyword, browse curated/popular media, a photographer's portfolio, or a curated collection. Get direct image and video file URLs, photographer credit, tags, colors, and more.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to fetch from Pexels. |
| `searchQuery` | string | no |  | Keyword to search for (mode=search). Example: `nature`, `city skyline`, `coffee`. |
| `mediaType` | string | no | photos | Which kind of media to return. For mode=search this selects between Pexels' separate photo-search and video-search pages (`all` is treated as `photos`). |
| `orientation` | string | no | all | Filter results by image/video orientation. |
| `minWidth` | integer | no | 0 | Only return media whose width is at least this many pixels. 0 disables the filter. |
| `minHeight` | integer | no | 0 | Only return media whose height is at least this many pixels. 0 disables the filter. |
| `minDuration` | integer | no | 0 | Only return videos at least this many seconds long (videos only; ignored for photos). 0 disables the filter. |
| `maxDuration` | integer | no | 0 | Only return videos at most this many seconds long (videos only; ignored for photos). 0 disables the filter. |
| `peopleCount` | string | no | all | Filter photo search results by how many people appear in them (mode=search, photos only). |
| `photoIds` | array | no | [] | Pexels photo IDs or full photo page URLs (mode=byPhotoId: look up these exact photos; mode=similarPhotos: find photos visually/topically similar to each of these). |
| `username` | string | no |  | Pexels photographer handle or profile URL (mode=byUser). Example: `alex-ivanov-773258579` or `https://www.pexels.com/@alex-ivanov-773258579/`. |
| `collectionSlug` | string | no |  | Pexels curated collection slug or full collection URL (mode=byCollection). Example: `aquatic-aesthetic-bw7dkse` or `https://www.pexels.com/collections/aquatic-aesthetic-bw7dkse/`. |

2 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQuery": "nature",
  "photoIds": [
    "18872916"
  ],
  "username": "alex-ivanov-773258579",
  "collectionSlug": "aquatic-aesthetic-bw7dkse",
  "mode": "search"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 30, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `photoId` | Photo Id |
| `videoId` | Video Id |
| `title` | Title |
| `photographerName` | Photographer Name |
| `width` | Width |
| `height` | Height |
| `orientation` | Orientation |
| `durationSeconds` | Duration Seconds |
| `license` | License |
| `attribution` | Attribution |
| `downloadUrl` | Download Url |
| `pageUrl` | Page Url |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `videoId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/pexels-stock-media-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
