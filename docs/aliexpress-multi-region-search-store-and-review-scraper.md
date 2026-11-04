# AliExpress Multi-Region Search, Store & Review Scraper: free n8n workflow

A free n8n workflow that runs the [AliExpress Multi-Region Search, Store & Review Scraper](https://apify.com/vexaloom-labs/aliexpress-multi-region-search-store-and-review) Apify Actor and returns `title`, `salePrice`, `originalPrice`, `discountPercent`, `rating` and more as clean, deduped rows for Google Sheets or your next node.

- Job: AliExpress product search export
- Platform: AliExpress
- Workflow file: [workflows/aliexpress-multi-region-search-store-and-review-scraper.json](../workflows/aliexpress-multi-region-search-store-and-review-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/aliexpress-multi-region-search-store-and-review-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/aliexpress-multi-region-search-store-and-review
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/aliexpress-multi-region-search-store-and-review-scraper/SKILL.md

## What it does

Search AliExpress or fetch product, store, and review records by ID or URL across 18 regional storefronts and 42 currencies, with price, rating, and ship-from/ship-to filters.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to collect. search: keyword results. byProduct: product lookup by ID or URL. byStore: store lookup. byReviews: customer reviews. |
| `searchQueries` | array | no |  | One or more keywords, e.g. "phone case" or "wireless earbuds". Each query is scraped up to maxPages pages. |
| `productIds` | array | no |  | Numeric AliExpress product IDs or item URLs. Both 1005… and 3256… ID formats are accepted. |
| `storeIds` | array | no |  | Numeric store IDs or /store/… URLs. |
| `urls` | array | no |  | Any mix of search, item, store and review URLs. The mode is detected per URL. |
| `region` | string | no | US | Country used for prices, availability and the storefront locale. Global leaves the region to the requesting IP. |
| `currency` | string | no |  | Optional ISO-4217 currency. Leave blank to use the region's usual currency. The currency actually returned is recorded in every record. |
| `language` | string | no | en_US | Storefront language and the language used to translate review text. |
| `sortBy` | string | no | default | How keyword results are ordered. AliExpress does not expose a newest sort. |
| `priceMin` | number | no | 0 | Minimum price in the selected currency. 0 disables the lower bound. |
| `priceMax` | number | no | 0 | Maximum price in the selected currency. 0 disables the upper bound. |
| `ratingMin` | number | no | 0 | Minimum star rating from 0 to 5. Products without a rating are skipped when a threshold is set. |

12 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "search",
  "region": "US",
  "language": "en_US",
  "sortBy": "default",
  "priceMin": 0,
  "priceMax": 0,
  "ratingMin": 0,
  "freeShippingOnly": false,
  "choiceOnly": false,
  "fourStarPlus": false,
  "includeSponsored": true,
  "includeWelcomeGifts": false,
  "maxItems": 100,
  "maxPages": 3,
  "includeReviews": false,
  "maxReviewsPerProduct": 20,
  "reviewFilter": "all",
  "includeProductStats": true,
  "searchQueries": [
    "keyword"
  ]
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `productId` | Product Id |
| `salePrice` | Sale Price |
| `originalPrice` | Original Price |
| `currencyCode` | Currency Code |
| `discountPercent` | Discount Percent |
| `rating` | Rating |
| `ordersCount` | Orders Count |
| `shipFromCountry` | Ship From Country |
| `productUrl` | Product Url |
| `isSponsored` | Is Sponsored |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/aliexpress-multi-region-search-store-and-review-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
