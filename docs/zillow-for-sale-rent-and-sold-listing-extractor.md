# Zillow For-Sale, Rent & Sold Listing Extractor: free n8n workflow

A free n8n workflow that runs the [Zillow For-Sale, Rent & Sold Listing Extractor](https://apify.com/nimbryxo-studio/zillow-for-sale-rent-and-sold-listing-extractor) Apify Actor and returns `address`, `price`, `soldPrice`, `beds`, `baths` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Zillow for-sale, rental and sold listings
- Platform: Zillow
- Workflow file: [workflows/zillow-for-sale-rent-and-sold-listing-extractor.json](../workflows/zillow-for-sale-rent-and-sold-listing-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/zillow-for-sale-rent-and-sold-listing-extractor.json`)
- Actor: https://apify.com/nimbryxo-studio/zillow-for-sale-rent-and-sold-listing-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/zillow-for-sale-rent-and-sold-listing-extractor/SKILL.md

## Watch the Short

- [The Listing Was Gone Before The Portal Email](https://www.youtube.com/shorts/bNjKOMdRlSY)

## What it does

Search Zillow by city, state or ZIP for active, rental or recently sold listings, with pricing, Zestimate, agent, school, tax and price history for each property.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | BUY | Search active for-sale listings, rentals, or recently sold listings. |
| `search` | string | no |  | City, ZIP, neighborhood, county or state to search (for example 'Houston, TX' or '77002'). |
| `maxItems` | integer | no | 50 | Maximum number of records for the whole run across all sources (1-5000). |
| `endPage` | integer | no | 5 | Maximum search result pages per search task (1-24). Zillow returns up to 41 listings per page. |
| `startUrls` | array | no | [] | Property detail URLs, /apartments/ building URLs, or Zillow search page URLs. Search URLs keep their own filters and mode. |
| `zpids` | array | no |  | Zillow property IDs or URLs containing _zpid. Each ZPID is resolved to its canonical detail page. |
| `addresses` | array | no |  | Full street addresses to resolve to Zillow property pages, for example '1306 Castle Ct, Houston, TX 77006'. |
| `priceMin` | integer | no |  | Minimum listing price in US dollars. |
| `priceMax` | integer | no |  | Maximum listing price in US dollars. |
| `bedsMin` | string | no | any | Minimum number of bedrooms. |
| `bathsMin` | string | no | any | Minimum number of bathrooms. |
| `sqftMin` | integer | no |  | Minimum living area in square feet. |

21 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "BUY",
  "search": "Austin, TX",
  "maxItems": 500,
  "scrapeDetails": true,
  "daysOnZillow": "1",
  "sortBy": "newest"
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `address` | Address |
| `price` | Price |
| `soldPrice` | Sold Price |
| `beds` | Beds |
| `baths` | Baths |
| `sqft` | Sqft |
| `propertyType` | Type |
| `status` | Status |
| `daysOnZillow` | Days |
| `url` | URL |

The full dataset has 48 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/zillow-for-sale-rent-and-sold-listing-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
