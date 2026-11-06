# Dailymotion Video Discovery by Topic & Channel: free n8n workflow

A free n8n workflow that runs the [Dailymotion Video Discovery by Topic & Channel](https://apify.com/dataspryva/dailymotion-video-discovery-by-topic-and-channel) Apify Actor and returns `title`, `ownerUsername`, `views`, `likes`, `duration` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Dailymotion video discovery
- Platform: Dailymotion
- Workflow file: [workflows/dailymotion-video-discovery-by-topic-and-channel.json](../workflows/dailymotion-video-discovery-by-topic-and-channel.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/dailymotion-video-discovery-by-topic-and-channel.json`)
- Actor: https://apify.com/dataspryva/dailymotion-video-discovery-by-topic-and-channel
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/dailymotion-video-discovery-by-topic-and-channel/SKILL.md

## What it does

Search Dailymotion by keyword, browse trending or topic videos, or pull a channel's uploads, with language, country, and duration filters, views, likes, tags, and owner details per video.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to fetch from Dailymotion. |
| `searchQueries` | array | no |  | One or more keywords to search (mode=search, mode=searchUsers). Each query is paginated up to Max items. Existing tasks with the old `searchQuery` field keep working. |
| `topic` | string | no | news | Dailymotion category to browse (mode=byTopic). |
| `videoIds` | array | no | [] | Specific videos to look up (mode=byVideoIds). Accepts bare IDs (`x4d4447`), dailymotion.com/video/... links, or dai.ly links. Unavailable IDs are skipped. |
| `sortBy` | string | no | relevance | Result order. Values apply where the Dailymotion API supports them: `relevance` needs mode=search/searchUsers; `popular` is mode=searchUsers only; `old`/`id-asc` are not available… |
| `language` | string | no |  | Only include videos in this language. Leave as All languages for every language. |
| `country` | string | no |  | Only include videos published from this country (mode=search, trending). Leave as All countries for every country. |
| `verifiedOnly` | boolean | no | false | Only include videos from verified Dailymotion channels (mode=search, trending). |
| `liveOnly` | boolean | no | false | Only include live streams instead of on-demand videos. |
| `tag` | string | no |  | Only include videos carrying this tag (mode=search, byTopic, byUser, byPlaylist). Example: `jazz`. |
| `createdAfter` | string | no |  | Only include videos published on or after this date, as `YYYY-MM-DD` (mode=search, trending, byTopic, byUser). Long ranges are fetched automatically in overlapping windows. |
| `createdBefore` | string | no |  | Only include videos published on or before this date, as `YYYY-MM-DD` (mode=search, trending, byTopic, byUser). Long ranges are fetched automatically in overlapping windows. |

5 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQueries": [
    "technology news"
  ],
  "maxItems": 25,
  "mode": "search"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `ownerUsername` | Owner Username |
| `views` | Views |
| `likes` | Likes |
| `duration` | Duration |
| `publishedAt` | Published At |
| `videoUrl` | Video Url |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/dailymotion-video-discovery-by-topic-and-channel.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
