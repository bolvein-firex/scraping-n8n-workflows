# Decrypt Crypto News Finder by Category & Keyword: free n8n workflow

A free n8n workflow that runs the [Decrypt Crypto News Finder by Category & Keyword](https://apify.com/dataspryva/decrypt-crypto-news-finder-by-category-and-keyword) Apify Actor and returns `title`, `authors`, `category`, `publishedAt`, `readingTimeMinutes` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Decrypt crypto news
- Platform: Decrypt
- Workflow file: [workflows/decrypt-crypto-news-finder-by-category-and-keyword.json](../workflows/decrypt-crypto-news-finder-by-category-and-keyword.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/decrypt-crypto-news-finder-by-category-and-keyword.json`)
- Actor: https://apify.com/dataspryva/decrypt-crypto-news-finder-by-category-and-keyword
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/decrypt-crypto-news-finder-by-category-and-keyword/SKILL.md

## What it does

Search Decrypt's crypto, Web3, and AI news by keyword or category, or look up specific articles, for full article text, authors, tags, mentioned coins, and featured images.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to fetch. Search matches titles, excerpts and article bodies. The latest mode returns the newest stories. |
| `searchQuery` | string | no |  | Keyword or phrase matched against article titles, excerpts and bodies (mode=search). E.g. bitcoin, ethereum, NFT. |
| `category` | string | no |  | One Decrypt category slug (mode=browseByCategory and as a filter in other modes). Leave empty for any category. |
| `categories` | array | no | [] | Filter by several category slugs at once. Applies to search, latest, tag, coin and author modes. |
| `tagSlugs` | array | no | [] | Filter by Decrypt tag slugs, e.g. bitcoin, ethereum, regulation. Tag names are not accepted; use the slugs returned in each record. |
| `coinSlugs` | array | no | [] | Filter by coin slugs, e.g. bitcoin, ethereum, solana. Names and ticker symbols are also accepted and mapped to slugs. |
| `authorSlugs` | array | no | [] | Filter by author slugs, e.g. jose, stephengraves. Author names are not accepted; use the slugs returned in each record. |
| `articleIds` | array | no | [] | Article IDs or decrypt.co URLs (mode=byId). Accepts bare IDs, /id/slug, localized /es/id/slug, ?p=id and /resources/slug URLs. |
| `locale` | string | no |  | Article language. Leave empty to include every locale. |
| `dateRangeFrom` | string | no |  | Only articles published on or after this date (YYYY-MM-DD). The date range is applied by the source. |
| `dateRangeTo` | string | no |  | Only articles published on or before this date (YYYY-MM-DD). The date range is applied by the source. |
| `sortBy` | string | no | newest | Newest first, oldest first, or best match. Best match needs a search query; otherwise newest is used. |

4 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQuery": "bitcoin",
  "category": "news",
  "articleIds": [
    "375656"
  ],
  "locale": "en",
  "maxItems": 25,
  "proxyConfiguration": {
    "useApifyProxy": false
  },
  "mode": "search"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `title` | Title |
| `authors` | Authors |
| `category` | Category |
| `publishedAt` | Published At |
| `readingTimeMinutes` | Reading Time Minutes |
| `wordCount` | Word Count |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/decrypt-crypto-news-finder-by-category-and-keyword.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
