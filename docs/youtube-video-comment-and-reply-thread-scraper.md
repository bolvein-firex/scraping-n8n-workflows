# YouTube Video Comment & Reply Thread Scraper: free n8n workflow

A free n8n workflow that runs the [YouTube Video Comment & Reply Thread Scraper](https://apify.com/nimbryxo-studio/youtube-video-comment-and-reply-thread-scraper) Apify Actor and returns `authorName`, `text`, `likeCount`, `replyCount`, `isHearted` and more as clean, deduped rows for Google Sheets or your next node.

- Job: YouTube video comment scraper
- Platform: YouTube
- Workflow file: [workflows/youtube-video-comment-and-reply-thread-scraper.json](../workflows/youtube-video-comment-and-reply-thread-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/youtube-video-comment-and-reply-thread-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/youtube-video-comment-and-reply-thread-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/youtube-video-comment-and-reply-thread-scraper/SKILL.md

## What it does

Get a YouTube video's comments with nested replies attached, author identity, like counts, and pinned/hearted/verified flags, filterable by keyword and minimum likes.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `videoUrls` | array | no | [] | Watch, youtu.be, Shorts, embed, live, v/ links, or bare 11-character IDs. Every video is normalized to a watch URL internally. |
| `channelUrls` | array | no | [] | Channel /videos sources: /@handle, /channel/UC..., /c/name, /user/name, a bare @handle, or a UC... channel ID. Scrapes up to Max videos per source. |
| `playlistUrls` | array | no | [] | Playlist sources: youtube.com/playlist?list=... or a bare playlist ID. Scrapes up to Max videos per source. |
| `searchQueries` | array | no | [] | YouTube search terms or search-result URLs. Only video results are used, deduplicated, up to Max videos per source. |
| `maxVideosPerSource` | integer | no | 20 | Discovery cap for channel, playlist and search sources. 0 = every video the source exposes. |
| `maxComments` | integer | no | 100 | Top-level comments to examine per video. 0 = all. Comments rejected by filters still count toward this scan cap (so restrictive filters cannot paginate forever); replies do not. |
| `includeReplies` | boolean | no | true | Fetch reply threads. Emitted as flat rows by default; use Output mode tree to embed them instead. |
| `maxRepliesPerComment` | integer | no | 50 | Per-thread reply cap. 0 = all replies, stopping when the continuation token is exhausted. YouTube serves roughly 9-10 on the first reply page and 44-49 afterwards. |
| `maxReplyDepth` | integer | no | 1 | 0 = top-level comments only, 1 = direct replies (the shape observed publicly). Values above 1 are reserved for nested sub-threads, which YouTube has not exposed in the samples… |
| `maxTotalRows` | integer | no | 5000 | Global budget for emitted comment + reply rows. 0 = unlimited. Status rows are never counted and are not billable data rows. |
| `sortBy` | string | no | top | top = YouTube relevance order; newest = chronological, recommended for date cutoffs and complete windows. A date cutoff forces newest automatically. |
| `commentsSince` | string | no |  | Optional cutoff as an ISO date/datetime (2026-10-16) or relative duration (7d, 24h, 30m). Forces newest sort. |

5 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "videoUrls": [
    "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
  ],
  "maxComments": 25,
  "maxRepliesPerComment": 3,
  "maxTotalRows": 20
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxComments` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.3:

| Field | Label |
|---|---|
| `commentId` | Comment ID |
| `authorName` | Author |
| `text` | Text |
| `likeCount` | Likes |
| `replyCount` | Replies |
| `isHearted` | Hearted |
| `videoTitle` | Video |

The full dataset has 17 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `videoId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/youtube-video-comment-and-reply-thread-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
