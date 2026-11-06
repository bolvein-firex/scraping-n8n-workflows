# Domain-Scoped Site Crawler for Markdown Datasets: free n8n workflow

A free n8n workflow that runs the [Domain-Scoped Site Crawler for Markdown Datasets](https://apify.com/vexaloom-labs/domain-scoped-site-crawler-for-markdown-datasets) Apify Actor and returns `url`, `title`, `depth`, `wordCount`, `httpStatusCode` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Domain-Scoped site scraper
- Platform: Domain-Scoped
- Workflow file: [workflows/domain-scoped-site-crawler-for-markdown-datasets.json](../workflows/domain-scoped-site-crawler-for-markdown-datasets.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/domain-scoped-site-crawler-for-markdown-datasets.json`)
- Actor: https://apify.com/vexaloom-labs/domain-scoped-site-crawler-for-markdown-datasets
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/domain-scoped-site-crawler-for-markdown-datasets/SKILL.md

## What it does

Crawl a website from one or more start URLs, staying on the same domain, and get back clean Markdown, text, or HTML per page with title, description, and crawl depth. Built for feeding LLM, RAG, or knowledge-base pipelines.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `startUrls` | array | yes |  | One or more URLs to start crawling from. The crawler follows links found on these pages and stays on the domain of the first start URL. |
| `maxCrawlDepth` | integer | no | 10 | How many links deep to follow from the start URLs. 0 means only the start URLs are crawled. |
| `maxCrawlPages` | integer | no | 20 | Maximum number of pages (and files) to store. The crawl stops when this limit is reached. |
| `useSitemaps` | boolean | no | false | Look for sitemaps (from robots.txt and /sitemap.xml) and enqueue the URLs they list. Finds pages that are not linked from the start URLs. |
| `useLlmsTxt` | boolean | no | false | Look for /llms.txt at the start URL domains and enqueue the files listed there (common on documentation sites). |
| `respectRobotsTxtFile` | boolean | no | true | Skip discovered pages that the site's robots.txt disallows. Start URLs are always crawled. |
| `crawlOnlyPagesChangedSince` | string | no |  | Optional date (YYYY-MM-DD or full ISO date-time). Crawls only pages that may have changed since then and outputs a delta. Leave empty to crawl everything. |
| `includeUrlGlobs` | array | no | [] | Only crawl discovered URLs matching these glob patterns (e.g. `https://example.com/docs/*`). Leave empty to allow everything on the domain. |
| `excludeUrlGlobs` | array | no | [] | Skip discovered URLs matching any of these glob patterns (e.g. *login*, *.pdf). |
| `includeUrlRegexps` | array | no | [] | Only crawl discovered URLs matching at least one of these regular expressions. Combined with glob patterns (both must pass when both are set). |
| `excludeUrlRegexps` | array | no | [] | Skip discovered URLs matching any of these regular expressions. |
| `keepUrlFragments` | boolean | no | false | Treat URLs that differ only in #fragment as different pages. Enable for single-page sites that use fragments as routes. |

14 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "startUrls": [
    {
      "url": "https://docs.apify.com"
    }
  ],
  "maxCrawlDepth": 1,
  "maxCrawlPages": 3
}
```

The input passes the Actor's input schema (checked at every publish). The run size follows the number of inputs you pass.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `url` | URL |
| `title` | Title |
| `depth` | Depth |
| `wordCount` | Words |
| `httpStatusCode` | Status |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `url` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/domain-scoped-site-crawler-for-markdown-datasets.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
