# Threads Public Post, Reply & Profile Data Extractor: free n8n workflow

A free n8n workflow that runs the [Threads Public Post, Reply & Profile Data Extractor](https://apify.com/vexaloom-labs/threads-public-post-reply-and-profile-data) Apify Actor and returns `authorUsername`, `postText`, `likeCount`, `commentCount`, `shareCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Threads public post, reply scraper
- Platform: Threads
- Workflow file: [workflows/threads-public-post-reply-and-profile-data-extractor.json](../workflows/threads-public-post-reply-and-profile-data-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/threads-public-post-reply-and-profile-data-extractor.json`)
- Actor: https://apify.com/vexaloom-labs/threads-public-post-reply-and-profile-data
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/threads-public-post-reply-and-profile-data-extractor/SKILL.md

## What it does

Pull posts, replies, media, reposts, keyword search, hashtag search, or a post's reply thread from Threads, with real engagement counts, captions, media, and profile bios.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | profile | What to collect from Threads. |
| `usernames` | array | no |  | Threads usernames, with or without @, or full profile URLs. Used by mode=profile / profileReplies / profileMedia / profileReposts. |
| `searchQueries` | array | no |  | Keywords, phrases, or #hashtags. Used by mode=search and mode=profilesByKeyword. |
| `tag` | string | no |  | Hashtag or topic to search without the # sign, e.g. 'ai' or 'mma'. Used by mode=tag. |
| `postUrls` | array | no |  | Threads post links (threads.com or threads.net). Each returns the post and its reply thread. Used by mode=postReplies. |
| `sortBy` | string | no | top | Order for keyword search results: Top (relevance) or Recent (newest first). 'default' is accepted as an alias of Top. |
| `includeProfileInfo` | boolean | no | true | For profile modes, also output one profile record per username with bio, follower count, verification, links, and topics. |
| `postedAfter` | string | no |  | Optional lower date bound. Accepts ISO dates (2026-01-31) or relative windows such as 7d, 24h, or 2w. |
| `postedBefore` | string | no |  | Optional upper date bound. Accepts ISO dates or relative windows such as 7d, 24h, or 2w. |
| `includeMediaUrls` | boolean | no | true | Store photos and videos in the run's key-value store so their links keep working after Threads' signed CDN links expire. Turn off to keep the original links. |
| `maxItems` | integer | no | 100 | Maximum number of post, reply, or discovered-profile records to return. |

Starter input (edit it in **Configure input**):

```json
{
  "usernames": [
    "zuck"
  ],
  "searchQueries": [
    "openai"
  ],
  "tag": "ai",
  "postUrls": [
    "https://www.threads.com/@zuck/post/DZpPDXbCeTt"
  ],
  "includeMediaUrls": false,
  "maxItems": 25,
  "mode": "profile"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `authorUsername` | Author Username |
| `postText` | Post Text |
| `publishedAt` | Published At |
| `likeCount` | Like Count |
| `commentCount` | Comment Count |
| `repostCount` | Repost Count |
| `quoteCount` | Quote Count |
| `shareCount` | Share Count |
| `mediaType` | Media Type |
| `postUrl` | Post Url |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `postUrl` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/threads-public-post-reply-and-profile-data-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
