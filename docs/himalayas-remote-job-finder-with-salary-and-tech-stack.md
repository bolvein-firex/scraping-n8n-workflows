# Himalayas Remote Job Finder with Salary & Tech Stack: free n8n workflow

A free n8n workflow that runs the [Himalayas Remote Job Finder with Salary & Tech Stack](https://apify.com/vexaloom-labs/himalayas-remote-job-finder-with-salary-and-tech) Apify Actor and returns `title`, `company`, `salaryMin`, `salaryMax`, `salaryPeriod` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Himalayas remote job
- Platform: Himalayas
- Workflow file: [workflows/himalayas-remote-job-finder-with-salary-and-tech-stack.json](../workflows/himalayas-remote-job-finder-with-salary-and-tech-stack.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/himalayas-remote-job-finder-with-salary-and-tech-stack.json`)
- Actor: https://apify.com/vexaloom-labs/himalayas-remote-job-finder-with-salary-and-tech
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/himalayas-remote-job-finder-with-salary-and-tech-stack/SKILL.md

## What it does

Search Himalayas remote job listings by keyword or company and get salary range, employment type, tech stack and job page link for each role.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | searchJobs | What to scrape. `searchJobs` runs a keyword search with filters. `browseAll` walks the newest-updated feed. `byCompany` returns a company's open roles. |
| `searchQuery` | string | no |  | Free-text keyword search (mode=searchJobs). Leave blank to page through the newest searchable listings. Himalayas caps keyword searches at 5,000 results. |
| `companySlug` | string | no |  | Canonical company slug or Himalayas company URL, e.g. `stripe` or `https://himalayas.app/companies/stripe`. Comma-separate several slugs, e.g. `stripe,vercel`. |
| `jobUrls` | array | no | [] | Himalayas job page URLs, e.g. `https://himalayas.app/companies/stripe/jobs/senior-engineer`. Closed or invalid URLs are skipped. |
| `country` | string | no |  | Only jobs open to this country. Leave blank for any country. Worldwide jobs are included unless Exclude worldwide is on. |
| `worldwide` | boolean | no | false | Only jobs with no country restrictions. Overrides the country filter. |
| `excludeWorldwide` | boolean | no | false | When a country is set, exclude jobs that are open worldwide. Requires country. |
| `seniority` | array | no | [] | Keep jobs at any of these seniority levels. Leave empty for all levels. |
| `employmentType` | string | no |  | Keep jobs of this employment type. Leave blank for all types. |
| `timezone` | string | no |  | Keep jobs that accept this UTC offset, e.g. `-5`, `UTC-5` or `UTC+05:30`. Leave blank for any timezone. |
| `categories` | array | no | [] | Keep jobs whose categories, parent categories or tech tags contain any of these terms (case-insensitive), e.g. `python`, `react`, `developer`. |
| `minSalary` | integer | no |  | Annualised salary floor. Hourly, weekly and monthly pay is converted to a yearly figure before comparison. Use salaryCurrency to compare in a specific currency. |

6 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQuery": "software engineer",
  "maxItems": 25,
  "mode": "searchJobs"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `title` | Title |
| `company` | Company |
| `employmentType` | Employment Type |
| `seniority` | Seniority |
| `salaryMin` | Salary Min |
| `salaryMax` | Salary Max |
| `salaryPeriod` | Salary Period |
| `salaryCurrency` | Salary Currency |
| `salaryAnnualMin` | Salary Annual Min |
| `salaryAnnualMax` | Salary Annual Max |
| `location` | Location |
| `skills` | Skills |
| `postedAt` | Posted At |
| `jobUrl` | Job Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/himalayas-remote-job-finder-with-salary-and-tech-stack.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
