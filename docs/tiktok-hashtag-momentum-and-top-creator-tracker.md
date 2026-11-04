# TikTok Hashtag Momentum & Top Creator Tracker: free n8n workflow

A free n8n workflow that runs the [TikTok Hashtag Momentum & Top Creator Tracker](https://apify.com/dataspryva/tiktok-hashtag-momentum-and-top-creator-tracker) Apify Actor and returns `rankIndex`, `hashtagName`, `publishCnt`, `vv` and more as clean, deduped rows for Google Sheets or your next node.

- Job: TikTok trending hashtags
- Platform: TikTok
- Workflow file: [workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json](../workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json`)
- Actor: https://apify.com/dataspryva/tiktok-hashtag-momentum-and-top-creator-tracker
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/tiktok-hashtag-momentum-and-top-creator-tracker/SKILL.md

## Watch the Short

- [Catch rising TikTok hashtags before Friday](https://www.youtube.com/shorts/C3buLaYtlGg)

## What it does

Reads TikTok Creative Center's trending-hashtag list for any country and returns rank, post and view counts, a day-by-day momentum curve, and top creators behind each trend.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | trendingHashtags | Choose 'Trending hashtags' for TikTok's ranked hashtag charts (post/view counts, popularity curve, creators) or 'Trending videos' for TikTok's ranked video charts (views… |
| `countries` | array | no | ["US"] | (mode=trendingHashtags) One or more markets to read the hashtag chart for. Each market adds its own ranked rows. |
| `periods` | array | no | ["7"] | (mode=trendingHashtags) Lookback windows in days. 7 shows recent spikes, 90 shows longer-term trends. Select one or more. |
| `includeOverallRanking` | boolean | no | true | (mode=trendingHashtags) Include each market's overall top-3 hashtag chart. Turn off to read only the industry charts selected below. |
| `scanAllIndustries` | boolean | no | true | (mode=trendingHashtags) Read all 19 industry charts for every market and window. This widens coverage from 3 to up to 60 hashtags per market and window, because each industry… |
| `industries` | array | no | [] | (mode=trendingHashtags) Specific industry charts to read when 'Scan all industries' is off. Ignored when scanning all industries. 19 public categories are available. |
| `includeCreatorLeaders` | boolean | no | false | (mode=trendingHashtags) Add creator rows that aggregate the creators TikTok credits across the collected hashtags, sorted by how many trends they appear in. |
| `minHashtagAppearances` | integer | no | 2 | (mode=trendingHashtags, creator leaderboard only) Only list creators credited on at least this many collected hashtag rows. |
| `videoCountries` | array | no | ["US"] | (mode=trendingVideos) Markets with a public TikTok trending-video chart. Select one or more. |
| `videoPeriods` | array | no | ["7"] | (mode=trendingVideos) Windows in days for the trending-video chart: 7 for videos created in the last week, 30 for the last month. |
| `videoSortBy` | string | no | views | (mode=trendingVideos) Metric used for the video ranking. |
| `videoOrganicOnly` | boolean | no | false | (mode=trendingVideos) Rank only organic (non-promoted) videos. TikTok returns a different ranking for organic-only charts. |

4 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "trendingHashtags",
  "countries": [
    "US"
  ],
  "periods": [
    "7"
  ],
  "maxItems": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `rankIndex` | Rank |
| `hashtagName` | Hashtag |
| `publishCnt` | Post Count |
| `vv` | Video Views |

The full dataset has 9 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `hashtagName` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
