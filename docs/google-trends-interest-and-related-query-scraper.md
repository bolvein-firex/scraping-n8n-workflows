# Google Trends Interest & Related Query Scraper: free n8n workflow

A free n8n workflow that runs the [Google Trends Interest & Related Query Scraper](https://apify.com/vexaloom-labs/google-trends-interest-and-related-query-scraper) Apify Actor and returns `searchTerms`, `title`, `geoName`, `averageInterest`, `growthPercent` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Export Google Trends data
- Platform: Google Trends
- Workflow file: [workflows/google-trends-interest-and-related-query-scraper.json](../workflows/google-trends-interest-and-related-query-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-trends-interest-and-related-query-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/google-trends-interest-and-related-query-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-trends-interest-and-related-query-scraper/SKILL.md

## Watch the Short

- [See the demand curve before the keyword tool](https://www.youtube.com/shorts/gDZBpA25UB8)

## What it does

Get interest-over-time, interest-by-region, and related topics/queries for any keyword, location, time range and Google surface, with side-by-side comparison for up to five keywords.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | interest | What to scrape. 'Interest over time & related queries' is the Google Trends Explore view (keywords required). 'Trending now' lists what is spiking in a country right now. |
| `searchTerms` | array | no |  | One or more search terms to analyze (mode=interest). Each term becomes its own dataset row, or enable Comparison mode to compare up to 5 terms side by side. |
| `compareMode` | boolean | no | false | Compare all search terms on one shared 0-100 scale in a single row (Google Trends comparison view, maximum 5 terms). Off means each term is scraped independently. |
| `startUrls` | array | no |  | Paste Google Trends links to scrape them directly: explore links (trends.google.com/trends/explore?q=..., including www.google.com/trends/... |
| `geo` | string | no |  | Country, state/region or metro area to analyze. Leave empty for worldwide. Trending Now uses the country part of this location. |
| `timeRange` | string | no | today 12-m | Time window for the interest data (mode=interest). 'now' ranges return minute-level points; 'today' ranges return day/week points. Choose 'Custom range' to enter exact dates below. |
| `customDateRange` | string | no |  | Only used when 'Time range' = 'Custom range': 'YYYY-MM-DD YYYY-MM-DD' (e.g. '2024-01-01 2024-12-31') or 'YYYY-MM-DDTHH YYYY-MM-DDTHH' for hourly granularity. |
| `category` | string | no | 0 | Google Trends category filter (mode=interest). 0 = All categories. |
| `searchType` | string | no |  | Which Google surface to query (mode=interest). Web Search is the default. |
| `geoResolution` | string | no |  | Breakdown level for 'interest by region' (mode=interest). Auto lets Google pick the right level for the location; other levels are applied when the location supports them. |
| `trendingHours` | string | no | 24 | How far back the Trending Now list goes (mode=trending). |
| `trendingCategory` | string | no | all | Filter the Trending Now list to one of Google's trending categories (mode=trending). |

2 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "interest",
  "searchTerms": [
    "ai agents",
    "n8n"
  ],
  "geo": "US",
  "timeRange": "today 3-m",
  "maxItems": 50
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 50, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `searchTerms` | Terms |
| `title` | Trending term |
| `geoName` | Location |
| `timeRangeLabel` | Time label |
| `hoursLabel` | Window |
| `categoryName` | Category |
| `searchTypeLabel` | Type label |
| `averageInterest` | Avg |
| `volumeText` | Volume |
| `growthPercent` | Growth % |
| `exploreUrl` | URL |
| `trendingUrl` | Trends URL |

The full dataset has 24 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-trends-interest-and-related-query-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
