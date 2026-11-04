# startup.jobs Category & Keyword Job Scraper: free n8n workflow

A free n8n workflow that runs the [startup.jobs Category & Keyword Job Scraper](https://apify.com/vexaloom-labs/startup-jobs-category-and-keyword-job-scraper) Apify Actor and returns `title`, `company`, `location`, `salary`, `postedAt` and more as clean, deduped rows for Google Sheets or your next node.

- Job: startup.jobs category scraper
- Platform: startup.jobs
- Workflow file: [workflows/startup-jobs-category-and-keyword-job-scraper.json](../workflows/startup-jobs-category-and-keyword-job-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/startup-jobs-category-and-keyword-job-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/startup-jobs-category-and-keyword-job-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/startup-jobs-category-and-keyword-job-scraper/SKILL.md

## What it does

Collect startup job listings from startup.jobs by category and keyword, with title, company, work mode, salary, job type, listing text, tags, and the listing link.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `category` | string | no | remote | Broad job category. Choose All categories to search everything, or Remote jobs for remote-only listings. |
| `role` | string | no |  | Specific role from the startup.jobs role taxonomy. When set, the category is ignored. |
| `keyword` | string | no |  | Matches job titles, company names and tags on startup.jobs. It does not search full description text. |
| `company` | string | no |  | Company name, slug or startup.jobs company URL (e.g. stripe or `https://startup.jobs/company/stripe`). |
| `location` | string | no |  | City or country name, or a startup.jobs location URL (e.g. United States, London, `https://startup.jobs/locations/germany`). Use Remote for remote jobs. |
| `workplaceType` | string | no |  | Filter by remote, hybrid or on-site work. |
| `employmentType` | string | no |  | Filter by full-time, part-time, contract or internship roles. |
| `experienceLevel` | string | no |  | Filter by the experience range published on the listing. Jobs without an experience level are excluded when this is set. |
| `minSalaryUsd` | integer | no |  | Only jobs whose published maximum salary is at least this amount in USD. Jobs without a published salary are excluded. |
| `maxSalaryUsd` | integer | no |  | Only jobs whose published minimum salary is at most this amount in USD. Jobs without a published salary are excluded. |
| `postedWithin` | string | no |  | Only include jobs published within this period. |
| `maxItems` | integer | no | 50 | Maximum number of jobs to return (1-500). |

Starter input (edit it in **Configure input**):

```json
{
  "maxItems": 25,
  "location": "New York, NY",
  "keyword": "coffee shop"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.3:

| Field | Label |
|---|---|
| `title` | Title |
| `company` | Company |
| `location` | Location |
| `workplaceType` | Workplace Type |
| `salary` | Salary |
| `postedAt` | Posted At |
| `url` | Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `url` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/startup-jobs-category-and-keyword-job-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
