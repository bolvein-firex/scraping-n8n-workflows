# Indeed Global Job Scraper with Company Salary Reports: free n8n workflow

A free n8n workflow that runs the [Indeed Global Job Scraper with Company Salary Reports](https://apify.com/nimbryxo-studio/indeed-global-job-scraper-with-company-salary) Apify Actor and returns `positionName`, `displayTitle`, `company`, `rating`, `salary` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Indeed job scraper with salaries
- Platform: Indeed
- Workflow file: [workflows/indeed-global-job-scraper-with-company-salary-reports.json](../workflows/indeed-global-job-scraper-with-company-salary-reports.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/indeed-global-job-scraper-with-company-salary-reports.json`)
- Actor: https://apify.com/nimbryxo-studio/indeed-global-job-scraper-with-company-salary
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/indeed-global-job-scraper-with-company-salary-reports/SKILL.md

## Watch the Short

- [The salary data is already public](https://www.youtube.com/shorts/33f3pNEO6Oc)

## What it does

Search Indeed jobs across 62 countries by keyword, location, or filters for job type, remote status, experience, education, and salary. Returns full descriptions, structured salaries, and each employer's ratings and salary-by-title reports.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `position` | string | no |  | Job title, skill or keywords, e.g. `web developer`, `nurse`. Search one company's jobs with `company:Amazon`, titles only with `title:(data analyst)`; quotes, OR and -exclusions… |
| `location` | string | no |  | City, region or postal code, e.g. `San Francisco`, `Austin, TX`, `10001`, `London`. Leave empty to search the whole country. |
| `company` | string | no |  | Only jobs from one employer, e.g. `Amazon`, `Visa`, `DocuSign`. The name is resolved to Indeed's employer key so the company filter is applied by Indeed itself, then verified per… |
| `locationShards` | array | no |  | Optional list of extra locations to search separately with the same keywords and filters, e.g. `New York, NY`, `Chicago, IL`, `Remote`. |
| `country` | string | no | US | Indeed country site to search. Results come in the site's language and salaries in its currency. |
| `maxItemsPerSearch` | integer | no | 100 | Maximum number of jobs to save for each search (the keyword search and each search URL). Indeed's cursor stops at roughly 1,000 fetched rows, including duplicates; use… |
| `maxItems` | integer | no |  | Optional hard cap across every search and pasted job URL. The run stops as soon as this many jobs are saved. Leave empty for no global cap. |
| `shardByDate` | boolean | no | false | Run each keyword search five times, for the last 1, 3, 7, 14 and 30 days, and remove duplicates. Useful for freshness coverage when you need more than one cursor walk per search. |
| `jobType` | string | no |  | Employment type. |
| `workplaceType` | string | no |  | Where the work happens. |
| `datePosted` | string | no |  | Only jobs added to Indeed within this period. |
| `experienceLevel` | string | no |  | Required experience level. |

11 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQueries": [
    "account executive"
  ],
  "location": "United States",
  "maxItems": 1000,
  "includeSalary": true
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `positionName` | Job title |
| `displayTitle` | Display title |
| `company` | Company |
| `rating` | Rating |
| `location` | Location |
| `salary` | Salary |
| `jobType` | Job type |
| `remoteWorkType` | Workplace |
| `postedAt` | Posted |
| `isRepost` | Repost |
| `isSponsored` | Sponsored |
| `easyApply` | Easy apply |
| `url` | Indeed link |

The full dataset has 29 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/indeed-global-job-scraper-with-company-salary-reports.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
