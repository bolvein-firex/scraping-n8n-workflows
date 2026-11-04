# Greenhouse ATS Job Board Lookup by Company: free n8n workflow

A free n8n workflow that runs the [Greenhouse ATS Job Board Lookup by Company](https://apify.com/dataspryva/greenhouse-ats-job-board-lookup-by-company) Apify Actor and returns `title`, `companySlug`, `companyName`, `location`, `departments` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Greenhouse ATS job board
- Platform: Greenhouse
- Workflow file: [workflows/greenhouse-ats-job-board-lookup-by-company.json](../workflows/greenhouse-ats-job-board-lookup-by-company.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/greenhouse-ats-job-board-lookup-by-company.json`)
- Actor: https://apify.com/dataspryva/greenhouse-ats-job-board-lookup-by-company
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/greenhouse-ats-job-board-lookup-by-company/SKILL.md

## What it does

Pull every open role from one or more Greenhouse company boards, or look up specific postings by job ID, with location, department, employment type, salary, and apply link for each.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | companyJobs | What to fetch: jobs from company boards, specific job URLs, or company board lookup. |
| `companies` | array | no |  | Board tokens, board URLs, embed URLs, job URLs, company names or domains. Examples: "stripe", "`https://job-boards.greenhouse.io/figma",` "Airbnb", "jobs.elastic.co". |
| `jobUrls` | array | no |  | Full Greenhouse job URLs to fetch one by one. A company board URL alone is not enough; include /jobs/. |
| `searchQuery` | string | no |  | Name or token text to match against the built-in company directory. Leave empty to resolve the Companies list instead. |
| `titleKeywords` | array | no |  | Keep jobs whose title contains any of these words (case-insensitive). |
| `excludeTitleKeywords` | array | no |  | Drop jobs whose title contains any of these words (case-insensitive). |
| `locations` | array | no |  | Keep jobs whose location or office contains any of these words, e.g. Remote, London, New York. |
| `departments` | array | no |  | Keep jobs in departments that contain any of these words, e.g. Engineering, Sales. |
| `workplaceType` | string | no | any | Keep remote, hybrid or on-site roles. Jobs without a stated arrangement are dropped when this is not Any. |
| `employmentType` | string | no | any | Keep full-time, part-time, contract, internship or temporary roles when the employer states it. |
| `publishedAfter` | string | no |  | Keep jobs first published on or after this date (YYYY-MM-DD). |
| `updatedAfter` | string | no |  | Keep jobs last updated on or after this date (YYYY-MM-DD). |

10 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "companyJobs",
  "workplaceType": "any",
  "employmentType": "any",
  "onlyWithSalary": false,
  "salaryCurrency": "any",
  "sortBy": "board",
  "content": false,
  "descriptionFormat": "html",
  "includeQuestions": false,
  "maxItems": 500,
  "maxJobsPerCompany": 0,
  "verifyCompanies": true,
  "searchQuery": "head of growth"
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `companySlug` | Company Slug |
| `companyName` | Company Name |
| `location` | Location |
| `departments` | Departments |
| `employmentType` | Employment Type |
| `publishedAt` | Published At |
| `updatedAt` | Updated At |
| `applyUrl` | Apply Url |
| `region` | Region |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/greenhouse-ats-job-board-lookup-by-company.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
