# Facebook Marketplace Listing & Price Extractor: free n8n workflow

A free n8n workflow that runs the [Facebook Marketplace Listing & Price Extractor](https://apify.com/nimbryxo-studio/facebook-marketplace-listing-and-price-extractor) Apify Actor and returns `title`, `price`, `city`, `state`, `locationText` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Facebook Marketplace scraper
- Platform: Facebook Marketplace
- Workflow file: [workflows/facebook-marketplace-listing-and-price-extractor.json](../workflows/facebook-marketplace-listing-and-price-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/facebook-marketplace-listing-and-price-extractor.json`)
- Actor: https://apify.com/nimbryxo-studio/facebook-marketplace-listing-and-price-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/facebook-marketplace-listing-and-price-extractor/SKILL.md

## What it does

Extract public Facebook Marketplace listings by city feed, category, keyword search, or direct item URL, with price, location, photos, delivery method, seller, and listing status per item.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | auto | What to scrape. auto uses startUrls when present and otherwise builds a keyword search. search builds a search from searchQueries plus location. |
| `startUrls` | array | no | [] | Marketplace search, city-category, global-category, city-feed, or /marketplace/item/ URLs. In mode=items, a bare numeric listing ID is also accepted. |
| `searchQueries` | array | no | [] | One to 20 keywords or phrases (mode=search or mode=auto without URLs). Each query becomes one source. |
| `location` | string | no |  | Marketplace location slug, city, postal code, or address used by keyword search (mode=search or mode=auto without URLs). Examples: nyc, Austin, Texas, 90210, London. |
| `country` | string | no | US | ISO 3166-1 alpha-2 country used when resolving a human location. Use GB for London, CA for Toronto, and so on. |
| `latitude` | number | no |  | Optional search center latitude. Provide longitude too. |
| `longitude` | number | no |  | Optional search center longitude. Provide latitude too. |
| `radiusKm` | integer | no | 65 | Search radius in kilometres for keyword or category search. URL mode keeps the radius in the URL unless you set this explicitly. |
| `category` | string | no | all | Marketplace category. If searchQueries is empty, the actor opens the city category feed (or the global category feed for a human location). |
| `categoryId` | string | no |  | Advanced numeric Facebook category ID. Takes precedence over category when set. |
| `sortBy` | string | no | relevance | Server-side sort where Marketplace supports it, plus a client-side re-sort by price or posting time. Rows without a price sort last. |
| `minPrice` | number | no |  | Only listings at or above this price. Rows without a price are dropped. |

15 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "search",
  "searchQueries": [
    "office chair"
  ],
  "location": "Austin, Texas",
  "maxItems": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `price` | Price |
| `city` | City |
| `state` | State |
| `locationText` | Location |
| `condition` | Condition |
| `deliveryTypes` | Delivery |
| `seller` | Seller |
| `primaryPhotoUrl` | Photo |
| `listingUrl` | Listing URL |

The full dataset has 65 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `listingUrl` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/facebook-marketplace-listing-and-price-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
