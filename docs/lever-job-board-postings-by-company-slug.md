# Lever Job Board Postings by Company Slug: free n8n workflow

A free n8n workflow that runs the [Lever Job Board Postings by Company Slug](https://apify.com/vexaloom-labs/lever-job-board-postings-by-company-slug) Apify Actor and returns `title`, `companySlug`, `location`, `salaryText`, `createdAt` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Lever job board postings
- Platform: Lever
- Workflow file: [workflows/lever-job-board-postings-by-company-slug.json](../workflows/lever-job-board-postings-by-company-slug.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/lever-job-board-postings-by-company-slug.json`)
- Actor: https://apify.com/vexaloom-labs/lever-job-board-postings-by-company-slug
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/lever-job-board-postings-by-company-slug/SKILL.md

## Watch the Short

- [Weekly job board tracking in one sheet](https://www.youtube.com/shorts/Fj8lsPbASu0)

## What it does

Pull open job postings from one or more Lever.co company boards, or fetch specific postings by ID, with location, team, salary range, requirements, and apply links, filterable by team, location, and commitment type.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | getJobs | Fetch every open posting from one or more boards, or fetch specific postings by ID or URL. |
| `companySlugs` | array | no |  | Company slugs, board URLs, API URLs or posting URLs. Examples: "wealthfront", "`https://jobs.lever.co/wealthfront",` "`https://jobs.eu.lever.co/olx"…` |
| `companySlug` | string | no |  | Company slug, board URL, API URL or posting URL used with postingIds (mode=getJob). |
| `postingIds` | array | no |  | Posting UUIDs or posting/apply URLs (mode=getJob). |
| `boardRegion` | string | no | auto | Use auto to try the global board first and fall back to the EU board when global returns 404 or no postings. |
| `team` | string | no |  | Keep postings whose team contains this text (case-insensitive). |
| `department` | string | no |  | Keep postings whose department contains this text (case-insensitive). |
| `location` | string | no |  | Keep postings whose primary location or any additional location contains this text (case-insensitive), e.g. "London" or "Remote". |
| `commitment` | string | no |  | Keep postings whose commitment or normalized employment type matches this text, e.g. "Full-time", "Contract", "Internship". |
| `workplaceType` | string | no |  | Keep postings with this exact workplace arrangement. |
| `remoteOnly` | boolean | no | false | Keep only postings marked remote or with a remote location. |
| `country` | string | no |  | Keep postings for one ISO 3166-1 alpha-2 country code, e.g. "US", "DE" or "IN". |

10 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "companySlugs": [
    "wealthfront"
  ],
  "maxItems": 25,
  "mode": "getJobs",
  "location": "New York, NY"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 2.0.1:

| Field | Label |
|---|---|
| `title` | Title |
| `companySlug` | Company Slug |
| `location` | Location |
| `workplaceType` | Workplace Type |
| `employmentType` | Employment Type |
| `salaryText` | Salary Text |
| `createdAt` | Created At |
| `hostedUrl` | Hosted Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/lever-job-board-postings-by-company-slug.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
