# Google Scholar Paper & Citation Search Scraper: free n8n workflow

A free n8n workflow that runs the [Google Scholar Paper & Citation Search Scraper](https://apify.com/dataspryva/google-scholar-paper-and-citation-search-scraper) Apify Actor and returns `title`, `name`, `authors`, `year`, `publication` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google Scholar paper scraper
- Platform: Google Scholar
- Workflow file: [workflows/google-scholar-paper-and-citation-search-scraper.json](../workflows/google-scholar-paper-and-citation-search-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-scholar-paper-and-citation-search-scraper.json`)
- Actor: https://apify.com/dataspryva/google-scholar-paper-and-citation-search-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-scholar-paper-and-citation-search-scraper/SKILL.md

## What it does

Search Google Scholar by keyword and get structured records for papers and citations, with author, venue, year, citation counts, and links to PDFs and related work. Filter by year range, document format, and article type.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | search | What to fetch: paper search, citing papers, or public author profiles. |
| `queries` | array | no |  | Keywords or paper titles to search on Google Scholar (mode=search). Each query runs separately. |
| `clusterIds` | array | no |  | Paper cluster IDs or Google Scholar 'cites=' URLs to list citing papers for (mode=citations). |
| `authorIds` | array | no |  | Google Scholar author IDs or profile URLs to export (mode=authorProfile). |
| `maxItems` | integer | no | 100 | Maximum papers per query or cluster, or papers per author. Google Scholar serves about 10 search results per page. |
| `sortBy` | string | no | relevance | Sort search results by relevance or date (mode=search). |
| `filter` | string | no | all | Keep only PDF or HTML results; applied to returned rows (mode=search). |
| `articleType` | string | no | any | Return all articles or review articles only (mode=search). |
| `newerThan` | integer | no |  | Only include papers published in this year or later (mode=search). |
| `olderThan` | integer | no |  | Only include papers published in this year or earlier (mode=search). |
| `author` | string | no |  | Return papers written by this author, e.g. 'Geoffrey Hinton' (mode=search). |
| `publication` | string | no |  | Return papers from this journal or venue, e.g. 'Nature' (mode=search). |

3 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "queries": [
    "attention is all you need"
  ],
  "maxItems": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `name` | Author |
| `authors` | Authors |
| `year` | Year |
| `publication` | Publication |
| `citations` | Citations |
| `documentType` | Type |
| `documentLink` | PDF/HTML |
| `link` | Link |
| `clusterId` | Cluster |
| `scholarUrl` | Scholar URL |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-scholar-paper-and-citation-search-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
