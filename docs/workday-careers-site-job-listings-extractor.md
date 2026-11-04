# Workday Careers Site Job Listings Extractor: free n8n workflow

A free n8n workflow that runs the [Workday Careers Site Job Listings Extractor](https://apify.com/nimbryxo-studio/workday-careers-site-job-listings-extractor) Apify Actor and returns `title`, `tenant`, `location`, `postedOn` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Workday careers site job listings scraper
- Platform: Workday
- Workflow file: [workflows/workday-careers-site-job-listings-extractor.json](../workflows/workday-careers-site-job-listings-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/workday-careers-site-job-listings-extractor.json`)
- Actor: https://apify.com/nimbryxo-studio/workday-careers-site-job-listings-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/workday-careers-site-job-listings-extractor/SKILL.md

## What it does

Pull job postings from any company's Workday careers site: title, location, requisition ID, posting and start dates, time type, remote status and full description. Filter by keyword, location or posting date.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | careerSite | How to find jobs. 'Scrape career site URLs' accepts careers pages or job URLs. 'Scrape a tenant by name' uses tenant + site. 'Scrape specific job URLs' requires /job/... |
| `startUrls` | array | no | ["`https://salesforce.wd12.myworkdayjobs.com/External_Career_Site"]` | Public Workday careers-site or job URLs (mode=careerSite or jobDetail). Paste the URL from your browser; both myworkdayjobs.com and myworkdaysite.com are supported. |
| `tenant` | string | no |  | Workday tenant name, for example 'nvidia' or 'capitalone' (mode=tenant). You can also paste the full careers URL here or use 'tenant/site'. |
| `site` | string | no |  | Optional career site identifier shown in the URL after the tenant host, for example 'NVIDIAExternalCareerSite' or 'External_Career_Site' (mode=tenant). It is case-sensitive. |
| `region` | string | no | auto | Workday data-center region. Leave 'auto' to detect it, or set wd1, wd3, wd5, wd12, wd103, and similar when you already know it (mode=tenant). |
| `searchText` | string | no |  | Optional keyword passed to the site's own job search, for example 'engineer' or 'marketing'. Workday searches titles and descriptions. |
| `locations` | array | no | [] | Optional locations to keep. Use names such as 'United States', 'New York', 'Remote' or 'US, CA, Santa Clara'; the actor matches them against the site's own location filters. |
| `jobFamilies` | array | no | [] | Optional job families or categories to keep, for example 'Engineering', 'Sales' or 'Finance'. Names come from the site's own Job Category filter; IDs are also accepted. |
| `remoteOnly` | boolean | no | false | Keep only postings the employer explicitly marks as remote. Hybrid and onsite postings are excluded. This turns on full detail fetching. |
| `postedWithin` | string | no | any | Keep jobs posted within this window. 'Any time' applies no date filter. Use Posted After for an exact cutoff date. |
| `postedAfter` | string | no |  | Optional exact cutoff date in YYYY-MM-DD form. When both Posted Within and Posted After are set, the stricter cutoff wins. |
| `startDateFrom` | string | no |  | Optional YYYY-MM-DD cutoff for the role's start date. Only applies when the posting publishes a start date. This turns on full detail fetching. |

4 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "careerSite",
  "startUrls": [
    "https://salesforce.wd12.myworkdayjobs.com/External_Career_Site"
  ],
  "region": "auto",
  "locations": [],
  "jobFamilies": [],
  "remoteOnly": false,
  "postedWithin": "any",
  "scrapeDetails": true,
  "includeJobFamily": true,
  "maxItems": 50,
  "proxyConfiguration": {
    "useApifyProxy": false
  }
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `title` | Title |
| `tenant` | Tenant |
| `location` | Location |
| `postedOn` | Posted On |
| `timeType` | Time Type |
| `workplaceType` | Workplace Type |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/workday-careers-site-job-listings-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
