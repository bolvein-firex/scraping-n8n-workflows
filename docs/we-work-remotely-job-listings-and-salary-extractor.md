# We Work Remotely Job Listings & Salary Extractor: free n8n workflow

A free n8n workflow that runs the [We Work Remotely Job Listings & Salary Extractor](https://apify.com/dataspryva/we-work-remotely-job-listings-and-salary-extractor) Apify Actor and returns `title`, `company`, `category`, `salary`, `postedAt` and more as clean, deduped rows for Google Sheets or your next node.

- Job: We Work Remotely job listings scraper
- Platform: We Work Remotely
- Workflow file: [workflows/we-work-remotely-job-listings-and-salary-extractor.json](../workflows/we-work-remotely-job-listings-and-salary-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/we-work-remotely-job-listings-and-salary-extractor.json`)
- Actor: https://apify.com/dataspryva/we-work-remotely-job-listings-and-salary-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/we-work-remotely-job-listings-and-salary-extractor/SKILL.md

## What it does

Reads We Work Remotely category pages or keyword search results and follows each listing for salary range, employment type, skills, applicant region requirements, and company details.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | browse | What to scrape. browse reads category feeds, search filters the full current inventory, byUrls accepts We Work Remotely links. |
| `categories` | array | no | [] | One or more categories. Leave empty to collect every category (recommended for the full inventory). |
| `searchTerm` | string | no |  | Words to match in the title, company, category or description. All words must match. Required in search mode. |
| `startUrls` | array | no | [] | Job, category, search, company or listing URLs. Mix freely. (mode=byUrls) |
| `employmentTypes` | array | no | [] | Employment types to keep. Leave empty for all. We Work Remotely publishes Full-Time and Contract roles. |
| `regions` | array | no | [] | Keep jobs open to one or more regions. Jobs open worldwide always match. Leave empty for all. |
| `countries` | array | no | [] | Keep jobs open to one or more countries (ISO-2 codes). Jobs open worldwide always match. Leave empty for all. |
| `postedWithin` | string | no | any | Keep jobs listed within this window. The listing date is the current (renewed) date, not the original post date. |
| `minSalary` | integer | no |  | Minimum annualized salary in USD. Jobs without a disclosed salary are kept unless requireSalary is on. Published currencies are not converted. |
| `maxSalary` | integer | no |  | Maximum annualized salary in USD. Jobs without a disclosed salary are kept unless requireSalary is on. Published currencies are not converted. |
| `requireSalary` | boolean | no | false | Only keep jobs with a confidently parsed salary range. Off by default so jobs that do not disclose pay are not lost. |
| `includeDescription` | boolean | no | true | Include the full description HTML and text. Salary is parsed even when this is off. |

6 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "browse",
  "categories": [],
  "startUrls": [],
  "employmentTypes": [],
  "regions": [],
  "countries": [],
  "postedWithin": "any",
  "requireSalary": false,
  "includeDescription": true,
  "cleanHtml": true,
  "includeDetails": false,
  "includeCompanyProfile": true,
  "incremental": false,
  "maxItems": 200
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.3.1:

| Field | Label |
|---|---|
| `title` | Title |
| `company` | Company |
| `category` | Category |
| `salary` | Salary |
| `postedAt` | Posted At |
| `url` | Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/we-work-remotely-job-listings-and-salary-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
