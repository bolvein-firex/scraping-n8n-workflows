# TikTok Verified Mention Tracker: free n8n workflow

A free n8n workflow that runs the [TikTok Verified Mention Tracker](https://apify.com/nimbryxo-studio/tiktok-profile-mention-scraper) Apify Actor and returns `targetUsername`, `postUrl`, `author.followerCount`, `playCount`, `likeCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: TikTok verified mention
- Platform: TikTok
- Workflow file: [workflows/tiktok-verified-mention-tracker.json](../workflows/tiktok-verified-mention-tracker.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-verified-mention-tracker.json`)
- Actor: https://apify.com/nimbryxo-studio/tiktok-profile-mention-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/tiktok-verified-mention-tracker/SKILL.md

## What it does

Find TikTok posts that tag a specific creator or brand handle, with each result checked against TikTok's own mention markup so you can tell a real @mention from a caption that merely contains the name.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `usernames` | array | yes |  | Brand or creator accounts whose mentions you want. Type a handle (nike), a handle with @ (@nike) or paste a profile link (`https://www.tiktok.com/@nike`). |
| `mentionFilter` | string | no | taggedOrCaption | Every saved post carries a mentionType label: 'tagged' (the caption contains TikTok's clickable tag of the account), 'captionText' (the caption types @handle without a working… |
| `excludeOwnPosts` | boolean | no | true | Leave out posts published by the tracked account itself, so you only see what other people say about it. |
| `datePosted` | string | no | anyTime | Only look at posts published in this period. |
| `postedAfter` | string | no |  | Exact cut-off date. Use a date (2026-10-01) or a relative age such as '3 days' or '2 weeks'. Works together with 'Posted within'; the stricter of the two applies. |
| `sortBy` | string | no | relevance | How saved posts are ordered for each account. 'Most liked' and 'Newest first' look at every post found before keeping the top ones. |
| `minPlayCount` | integer | no |  | Skip posts with fewer views than this. Leave empty to keep posts of any size. |
| `searchDepth` | string | no | standard | 'Standard' runs one search per account and reads every page TikTok returns. 'Deep' adds searches by plain handle, display name and #handle, a most-liked pass, several date ranges… |
| `searchCountry` | string | no | any | TikTok shows different posts in different countries. Pick a country to see the mentions people there get in their search results (for example Japan for Japanese posts). |
| `followRelatedVideos` | boolean | no | false | After searching, open TikTok's related videos for every post that tags the account and keep related posts that also mention it (repeating a few hops). |
| `maxResultsPerProfile` | integer | no | 50 | Stop after this many saved posts for each account. TikTok search usually yields tens to a few hundred posts per account, so very high values simply mean 'everything found'. |
| `maxItems` | integer | no |  | Optional limit across all accounts in this run. Leave empty for no overall limit. |

2 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "usernames": [
    "billieeilish"
  ],
  "maxResultsPerProfile": 3,
  "maxItems": 50
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 50, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.2:

| Field | Label |
|---|---|
| `targetUsername` | Tracked account |
| `mentionType` | Mention type |
| `postUrl` | Post |
| `caption` | Caption |
| `createdAt` | Posted |
| `author.username` | Posted by |
| `author.followerCount` | Author followers |
| `playCount` | Views |
| `likeCount` | Likes |
| `commentCount` | Comments |
| `shareCount` | Shares |
| `postType` | Type |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `postUrl` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/tiktok-verified-mention-tracker.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
