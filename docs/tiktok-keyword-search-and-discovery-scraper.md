# TikTok Keyword Search & Discovery Scraper: free n8n workflow

A free n8n workflow that runs the [TikTok Keyword Search & Discovery Scraper](https://apify.com/vexaloom-labs/tiktok-keyword-search-and-discovery-scraper) Apify Actor and returns `rank`, `caption`, `playCount`, `likeCount`, `commentCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: TikTok keyword search scraper
- Platform: TikTok
- Workflow file: [workflows/tiktok-keyword-search-and-discovery-scraper.json](../workflows/tiktok-keyword-search-and-discovery-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-keyword-search-and-discovery-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/tiktok-keyword-search-and-discovery-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/tiktok-keyword-search-and-discovery-scraper/SKILL.md

## What it does

Search TikTok by keyword or phrase and get matching videos with engagement stats, author profiles, music metadata, hashtags, and location tags, with optional discovery expansion for more results.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `searchType` | string | yes | videos | Videos: keyword video search. Photos: slideshow/photo search. Hashtags: hashtag metadata plus its top videos (uses the Hashtags field). |
| `queries` | array | no |  | Keywords or phrases to search for (searchType=videos or photos). Each query is searched independently. |
| `hashtags` | array | no |  | Hashtags to look up (searchType=hashtags). The # is optional, e.g. coffee or #coffee. |
| `maxResultsPerQuery` | integer | no | 30 | Maximum posts to collect per query or hashtag, before filters. TikTok itself usually returns about 150-220 posts per query even when you ask for more. |
| `sortBy` | string | no | relevance | Client-side sort applied after collecting results. TikTok's web search does not support server-side sorting, so this only reorders the posts TikTok returned. |
| `publishedWithin` | string | no | all | Client-side filter that drops posts older than the selected window, based on each post's creation time. |
| `minDurationSeconds` | integer | no |  | Drop videos shorter than this. Leave blank for no minimum. |
| `maxDurationSeconds` | integer | no |  | Drop videos longer than this. Leave blank for no maximum. |
| `excludeAds` | boolean | no | false | Drop posts TikTok flags as paid advertisements. |
| `minLikeCount` | integer | no |  | Drop posts with fewer likes than this. Leave blank for no minimum. |
| `minViewCount` | integer | no |  | Drop posts with fewer plays/views than this. Leave blank for no minimum. |
| `uniqueAuthors` | boolean | no | false | Keep at most one post per creator, so the results read like a creator shortlist. When a sort is selected, the top-ranked post from each creator is kept. |

5 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "queries": [
    "viral"
  ],
  "maxResultsPerQuery": 25,
  "searchType": "videos"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxResultsPerQuery` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.7:

| Field | Label |
|---|---|
| `postId` | Post ID |
| `rank` | Rank |
| `searchType` | Search Type |
| `caption` | Caption |
| `createdAt` | Created At |
| `author` | Author |
| `playCount` | Views |
| `likeCount` | Likes |
| `commentCount` | Comments |
| `shareCount` | Shares |
| `postUrl` | Post URL |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `postUrl` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-keyword-search-and-discovery-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
