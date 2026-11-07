# Zillow Research County Home Value Trend Scraper: free n8n workflow

A free n8n workflow that runs the [Zillow Research County Home Value Trend Scraper](https://apify.com/dataspryva/zillow-research-county-home-value-trend-scraper) Apify Actor and returns `countyName`, `stateCode`, `stateName`, `metro`, `latestValue` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Zillow research county home value trend scraper
- Platform: Zillow
- Workflow file: [workflows/zillow-research-county-home-value-trend-scraper.json](../workflows/zillow-research-county-home-value-trend-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/zillow-research-county-home-value-trend-scraper.json`)
- Actor: https://apify.com/dataspryva/zillow-research-county-home-value-trend-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/zillow-research-county-home-value-trend-scraper/SKILL.md

## What it does

Get US county-level home value trends with 6- and 12-month comparisons and year-over-year percent change, plus a state-by-state home value comparison, from Zillow's published research files. Filter by state and county.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | countyTrends | What to return: one trend row per county, per state, per metro, or one history row per region per month. |
| `homeType` | string | no | allHomesMidTier | Which Zillow Home Value Index series to read. All ten cuts are available at county, state, and metro level. |
| `state` | string | no | all | Filter counties, metros, or history to one state, or pick a single state in stateTrends. Choose 'all' to include every state. Two-letter codes are accepted by the API. |
| `county` | string | no |  | Case-insensitive county-name substring, e.g. 'Gallatin' or 'Los Angeles'. Works in countyTrends and county history. Use regionIds for exact matching. |
| `regionIds` | array | no | [] | Exact Zillow RegionIDs, e.g. ['3101', '1090']. Works in every mode. When combined with state or county filters, a region must match all of them. |
| `asOfDate` | string | no |  | Compute the trend from the latest observation on or before this date (YYYY-MM-DD). Leave empty for the newest published month. Trend modes only. |
| `historyGeography` | string | no | county | Which ZHVI level the monthly history rows come from. Used only in history mode. |
| `startDate` | string | no |  | First month to include in history mode (YYYY-MM-DD). Leave empty to start at the oldest published month. |
| `endDate` | string | no |  | Last month to include in history mode (YYYY-MM-DD). Leave empty to end at the newest published month. |
| `sortBy` | string | no | sizeRank | Order trend rows and assign ranks across all matching regions before the row cap is applied. Missing metrics sort last without a rank. |
| `maxItems` | integer | no | 100 | Hard cap on emitted records. The default county file has 3,071 rows; history usually needs a date or region filter to stay under the cap. |

Starter input (edit it in **Configure input**):

```json
{
  "mode": "stateTrends",
  "maxItems": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `countyName` | County Name |
| `stateCode` | State Code |
| `stateName` | State Name |
| `metro` | Metro |
| `homeType` | Home Type |
| `latestValue` | Latest Value |
| `latestDate` | Latest Date |
| `change6mPct` | Change6m Pct |
| `change12mPct` | Change12m Pct |
| `vsBenchmark6mPct` | Vs Benchmark6m Pct |
| `rank` | Rank |

The full dataset has 5 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/zillow-research-county-home-value-trend-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
