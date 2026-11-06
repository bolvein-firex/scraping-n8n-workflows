# Google News Keyword & Full-Text Article Scraper: free n8n workflow

A free n8n workflow that runs the [Google News Keyword & Full-Text Article Scraper](https://apify.com/nimbryxo-studio/google-news-keyword-and-full-text-article-scraper) Apify Actor and returns `title`, `source`, `domain`, `publishedAt`, `url` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google News keyword scraper
- Platform: Google News
- Workflow file: [workflows/google-news-keyword-and-full-text-article-scraper.json](../workflows/google-news-keyword-and-full-text-article-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-news-keyword-and-full-text-article-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/google-news-keyword-and-full-text-article-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-news-keyword-and-full-text-article-scraper/SKILL.md

## What it does

Search Google News by keyword with real resolved article links, headlines, sources, and dates, plus optional full article text and image extraction, filterable by date, language, and publisher.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | keyword | What to scrape. Each mode reads its own list field below. |
| `queries` | array | no | [] | One or more keyword queries. Google operators such as site:, intitle: and OR are supported. Results are deduplicated across queries. |
| `topics` | array | no | [] | Topic names (WORLD, NATION, BUSINESS, TECHNOLOGY, ENTERTAINMENT, SPORTS, SCIENCE, HEALTH), TOP for top stories, Google News topic hashes/section URLs, or topic URLs. |
| `newsUrls` | array | no | [] | Google News search URLs, topic URLs, RSS search/topic URLs, or RSS/Atom feed URLs to convert into a feed. |
| `rssUrls` | array | no | [] | Any public RSS or Atom feed. Google News links inside the feed are resolved to publisher URLs automatically. |
| `articleUrls` | array | no | [] | Publisher article URLs or Google News article URLs. Every page is fetched and full text is extracted, with a per-record status when a publisher blocks or paywalls it. |
| `language` | string | no | en | Language of the Google News edition. Combined with country in the edition token (for example US:en, DE:de, JP:ja). |
| `country` | string | no | US | Country edition for Google News. The actor always pins the edition so results do not change with the machine's IP. |
| `dateRange` | string | no | any | Recency window. Every item is post-filtered by its real publication time, so items newer than the window never leak. 'custom' uses startDate/endDate. |
| `startDate` | string | no |  | Custom range start (YYYY-MM-DD, inclusive). Also used when dateRange=custom. |
| `endDate` | string | no |  | Custom range end (YYYY-MM-DD, inclusive). Items published after the end are dropped client-side. |
| `maxResultsPerQuery` | integer | no | 20 | Maximum records taken from each Google News feed request (1-100, Google's own cap is about 100). |

4 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "queries": [
    "artificial intelligence"
  ],
  "maxResultsPerQuery": 3,
  "maxItems": 25,
  "mode": "keyword"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 2.0.1:

| Field | Label |
|---|---|
| `title` | Title |
| `source` | Source |
| `domain` | Domain |
| `publishedAt` | Published |
| `url` | URL |
| `fullTextStatus` | Status |

The full dataset has 5 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `url` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-news-keyword-and-full-text-article-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
