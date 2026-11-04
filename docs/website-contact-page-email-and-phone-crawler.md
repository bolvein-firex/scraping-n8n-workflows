# Website Contact Page Email & Phone Crawler: free n8n workflow

A free n8n workflow that runs the [Website Contact Page Email & Phone Crawler](https://apify.com/nimbryxo-studio/website-contact-page-email-and-phone-crawler) Apify Actor and returns `websiteUrl`, `status`, `emails`, `primaryEmail`, `phones` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Find emails and phone numbers from a list of websites
- Platform: Any website
- Workflow file: [workflows/website-contact-page-email-and-phone-crawler.json](../workflows/website-contact-page-email-and-phone-crawler.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/website-contact-page-email-and-phone-crawler.json`)
- Actor: https://apify.com/nimbryxo-studio/website-contact-page-email-and-phone-crawler
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/website-contact-page-email-and-phone-crawler/SKILL.md

## Watch the Short

- [The email is already on the website](https://www.youtube.com/shorts/MHdeuiVwMZA)

## What it does

Crawl a website's contact, about and team pages and collect its public emails, phone numbers, and social media profile links in one normalized record per site.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `urls` | array | yes |  | Websites to scan for public contact details. You can paste full URLs or bare domains; duplicates are removed. |
| `maxPagesPerSite` | integer | no | 20 | Maximum number of pages to fetch per website. Contact, about, team and imprint pages are prioritised. |
| `maxConcurrency` | integer | no | 5 | How many pages of the same website may be fetched in parallel. |
| `maxSitesConcurrency` | integer | no | 3 | How many websites are scanned in parallel. Lower this if you hit rate limits. |
| `requestTimeoutSecs` | integer | no | 15 | Maximum time to wait for one page before trying the next proxy tier. |
| `defaultCountry` | string | no |  | ISO 3166-1 alpha-2 country used to interpret phone numbers written without an international prefix. Leave empty to infer from the website domain. |
| `useProxy` | boolean | no | false | Start with the Apify proxy ladder instead of trying direct requests first. The actor always retries blocked requests through the proxy ladder automatically. |
| `smartPrioritise` | boolean | no | true | Try common contact, about, team, imprint and support paths first, and queue contact-like links ahead of other internal links. |
| `respectRobotsTxt` | boolean | no | true | Skip pages that the website's robots.txt disallows. Turn this off only when you own the site or have permission to crawl it. |
| `useSitemap` | boolean | no | true | Read sitemap.xml and robots.txt sitemap entries to find contact and about pages that are not linked from the homepage. |
| `renderFallback` | boolean | no | true | If plain HTML contains no email or phone, render up to two pages in a headless browser to capture contacts loaded by JavaScript. |
| `onlyWithContacts` | boolean | no | false | Drop records for websites where no email, phone, social profile or contact form was found. |

1 more optional field on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "urls": [
    "https://apify.com",
    "https://n8n.io"
  ],
  "maxPagesPerSite": 10
}
```

The input passes the Actor's input schema (checked at every publish). The run size follows the number of inputs you pass.

## Output fields

Columns from the Actor's README (Output section), build 1.1.1:

| Field | Label |
|---|---|
| `websiteUrl` | Website Url |
| `status` | Status |
| `companyName` | Company Name |
| `emails` | Emails |
| `primaryEmail` | Primary Email |
| `roleEmails` | Role Emails |
| `namedEmails` | Named Emails |
| `emailDetails` | Email Details |
| `phones` | Phones |
| `primaryPhone` | Primary Phone |
| `phoneDetails` | Phone Details |
| `socialLinks` | Social Links |
| `socialProfiles` | Social Profiles |
| `address` | Address |
| `contactPageUrl` | Contact Page Url |
| `contactForms` | Contact Forms |
| `pagesCrawled` | Pages Crawled |
| `pagesCrawledUrls` | Pages Crawled Urls |
| `maxDepthReached` | Max Depth Reached |
| `skippedByRobots` | Skipped By Robots |
| `browserUsed` | Browser Used |

The full dataset has 5 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `websiteUrl` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/website-contact-page-email-and-phone-crawler.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
