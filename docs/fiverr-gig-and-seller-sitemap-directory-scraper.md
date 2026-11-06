# Fiverr Gig & Seller Sitemap Directory Scraper: free n8n workflow

A free n8n workflow that runs the [Fiverr Gig & Seller Sitemap Directory Scraper](https://apify.com/vexaloom-labs/fiverr-gig-and-seller-sitemap-directory-scraper) Apify Actor and returns `title`, `gigUrl`, `priceMin`, `priceMax`, `rating` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Fiverr gig scraper
- Platform: Fiverr
- Workflow file: [workflows/fiverr-gig-and-seller-sitemap-directory-scraper.json](../workflows/fiverr-gig-and-seller-sitemap-directory-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/fiverr-gig-and-seller-sitemap-directory-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/fiverr-gig-and-seller-sitemap-directory-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/fiverr-gig-and-seller-sitemap-directory-scraper/SKILL.md

## Watch the Short

- [Stop copying Fiverr profiles; build one shortlist](https://www.youtube.com/shorts/JsVKl5TOvJE)

## What it does

List live Fiverr gigs, seller profiles, categories, search tags and Logo Maker ideas straight from Fiverr's own directories, with best-effort full gig detail by URL.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | sitemapDirectory | What to run. `search` searches Fiverr by keyword or browses search/category URLs. `gigDetails` fetches full details for gig URLs. `sellerProfiles` fetches seller profiles. |
| `searchQueries` | array | no | [] | Keywords to search on Fiverr (mode=search), e.g. `logo design` or `voice over`. One search is run per query. |
| `searchUrls` | array | no | [] | Fiverr search or category URLs to browse (mode=search), e.g. `https://www.fiverr.com/search/gigs?query=logo%20design` or a `/categories/...` URL. |
| `gigUrls` | array | no | [] | Full Fiverr gig URLs to fetch, e.g. `https://www.fiverr.com/username/gig-slug` (mode=gigDetails). |
| `sellerUrls` | array | no | [] | Fiverr seller usernames or profile URLs, e.g. `michael7878` or `https://www.fiverr.com/michael7878` (mode=sellerProfiles). |
| `sitemapType` | string | no | gigs | Which Fiverr sitemap directory to list (mode=sitemapDirectory). |
| `searchKeyword` | string | no |  | Only keep sitemap entries whose URL or slug contains this keyword (mode=sitemapDirectory). Also filters gig titles in detail and search modes when set. Case-insensitive. |
| `maxShards` | integer | no | 1 | Number of sitemap shard files to scan for gigs (up to 7), sellers (up to 6) or tags (up to 2). Values above the available shard count are capped. |
| `categoryLevel` | string | no |  | Only keep category entries at this level (mode=sitemapDirectory, sitemapType=categories). |
| `ideaType` | string | no |  | Only keep Logo Maker entries of this type (mode=sitemapDirectory, sitemapType=logomakerIdeas). |
| `category` | string | no |  | Only keep results in this Fiverr category. Applies to category directory entries, and to gig details and enriched search results when the page reports that category slug. |
| `sortBy` | string | no | relevance | Sort live search results (mode=search). |

21 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQueries": [
    "logo design"
  ],
  "searchKeyword": "logo",
  "maxPagesPerQuery": 1,
  "maxItems": 25,
  "mode": "sitemapDirectory"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `gigUrl` | Gig Url |
| `sellerUsername` | Seller Username |
| `sellerLevel` | Seller Level |
| `category` | Category |
| `subCategory` | Sub Category |
| `priceMin` | Price Min |
| `priceMax` | Price Max |
| `currency` | Currency |
| `rating` | Rating |
| `reviewsCount` | Reviews Count |
| `sellerCountryCode` | Seller Country Code |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/fiverr-gig-and-seller-sitemap-directory-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
