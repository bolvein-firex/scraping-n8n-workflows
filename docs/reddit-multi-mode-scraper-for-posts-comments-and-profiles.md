# Reddit Multi-Mode Scraper for Posts, Comments & Profiles: free n8n workflow

A free n8n workflow that runs the [Reddit Multi-Mode Scraper for Posts, Comments & Profiles](https://apify.com/nimbryxo-studio/reddit-multi-mode-scraper-for-posts-comments) Apify Actor and returns `subreddit_prefixed`, `title`, `author`, `score`, `commentCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Reddit posts and comments scraper
- Platform: Reddit
- Workflow file: [workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json](../workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json`)
- Actor: https://apify.com/nimbryxo-studio/reddit-multi-mode-scraper-for-posts-comments
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/reddit-multi-mode-scraper-for-posts-comments-and-profiles/SKILL.md

## Watch the Short

- [Your customers are describing the problem for free](https://www.youtube.com/shorts/3TmxkUNaB0U)

## What it does

Pick one of five modes to pull subreddit posts, full comment threads, user profiles, keyword search results or curated community listings from Reddit, each with deep post/comment filters. No account or API key needed.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | subreddit | What to scrape: a subreddit listing, post URLs with comments, a user profile, or keyword search. |
| `source` | string | no | auto | auto uses live Reddit first and the Arctic Shift archive for depth/bulk or as a fallback. archive is faster and cheaper but lags live Reddit by several hours; live never uses… |
| `subreddits` | array | no | ["programming"] | Subreddits to scrape (mode=subreddit). Accepts names, r/ names or URLs. |
| `postUrls` | array | no | [] | Post URLs, comment URLs, share links or bare post IDs (mode=post). |
| `usernames` | array | no | [] | Reddit usernames to scrape (mode=profile). Accepts names, u/ names or profile URLs. |
| `searchQuery` | string | no |  | Keyword or phrase to search for (mode=search). Reddit search syntax such as "exact phrase", author:name, subreddit:name and -exclude is supported by live search. |
| `maxItems` | integer | no | 50 | Hard cap on all records pushed by the run, across every target. |
| `maxPosts` | integer | no | 25 | Posts per subreddit, keyword or profile section. |
| `maxComments` | integer | no | 100 | Comments per post, keyword, or profile comment section. 0 disables comment records. |
| `maxDepth` | integer | no | 6 | Deepest reply level to emit (0 = top-level comments only). |
| `includeComments` | boolean | no | true | Emit comment records for each post. Disable to fetch only the parent post. |
| `includePost` | boolean | no | true | Emit the post record before its comments. |

55 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "subreddits": [
    "smallbusiness",
    "SaaS"
  ],
  "searchQuery": "lead generation",
  "maxItems": 1000,
  "includeComments": true
}
```

## Output fields

Columns from the Actor's dataset schema, build 2.0.1:

| Field | Label |
|---|---|
| `subreddit_prefixed` | Subreddit prefixed |
| `title` | Title |
| `author` | Author |
| `score` | Score |
| `commentCount` | Comment Count |
| `source` | Source |
| `createdAt` | Created At |
| `permalink` | Permalink |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
