# Amazon Customer Review & Rating Summary Scraper: free n8n workflow

A free n8n workflow that runs the [Amazon Customer Review & Rating Summary Scraper](https://apify.com/vexaloom-labs/amazon-customer-review-and-rating-summary-scraper) Apify Actor and returns `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Amazon review scraper
- Platform: Amazon
- Workflow file: [workflows/amazon-customer-review-and-rating-summary-scraper.json](../workflows/amazon-customer-review-and-rating-summary-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-customer-review-and-rating-summary-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/amazon-customer-review-and-rating-summary-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/amazon-customer-review-and-rating-summary-scraper/SKILL.md

## Watch the Short

- [Stop copying Amazon reviews; sort them in a sheet](https://www.youtube.com/shorts/WhVOks5q4MU)

## What it does

Get Amazon customer reviews and a product-level rating summary by product URL, keyword, or category, with star-rating and sort filters, across 23 Amazon domains.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `productUrls` | array | no |  | Amazon product URLs (/dp/, /gp/product/, /gp/aw/d/, /product/) or bare 10-character ASINs, on any supported Amazon domain. |
| `keywords` | array | no | [] | Search terms used to discover products when `productUrls` is empty (e.g. "wireless earbuds"). Each keyword contributes up to `maxProductsToDiscover` products. |
| `categoryUrls` | array | no | [] | Advanced discovery: Amazon `/s?...` search URLs or `/b?node=...` category URLs. Used only when `productUrls` is empty. |
| `maxProductsToDiscover` | integer | no | 5 | Maximum products discovered from each keyword or category URL (1-50). Ignored when `productUrls` is supplied. |
| `country` | string | no | amazon.com | Amazon storefront to use for bare ASINs, discovery, and products whose URL does not carry a domain. Product URLs keep their own domain. |
| `maxReviews` | integer | no | 100 | Hard cap per product after merging and deduplication (1-2000). The product-page sample alone yields about 8-13 rows; the optional extended feed can add 100-800+ for popular US… |
| `extendedHistory` | boolean | no | true | Merge Amazon's public extended review feed for each ASIN (no login): up to 100 rows per star/sort bucket, typically 100-800+ unique reviews for popular US products, deduplicated… |
| `mergeMarketplaces` | array | no | [] | Fetch the same product on these additional Amazon marketplaces and merge their deduplicated product-page reviews. Empty = the product's own marketplace only. |
| `sortBy` | string | no | helpful | Order of the returned reviews: most helpful first, or most recent first. |
| `filterByStar` | string | no |  | Keep only reviews with this rating. `positive` keeps 4-5 stars and `critical` keeps 1-2 stars. Applied after merging, so narrow filters can legitimately return few or no rows. |
| `verifiedPurchasesOnly` | boolean | no | false | Keep only reviews carrying Amazon's Verified Purchase badge. Applied server-side in the extended feed (and cookie mode) and client-side for product-page rows. |
| `filterKeywords` | array | no | [] | Keep only reviews whose title or text contains at least one of these keywords (case-insensitive). Empty = no keyword filter. |

6 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "keywords": [
    "wireless earbuds"
  ],
  "country": "amazon.com",
  "maxProductsToDiscover": 2,
  "maxReviews": 20,
  "includeAggregates": true
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxProductsToDiscover` = 2, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.3:

| Field | Label |
|---|---|
| `productAsin` | ASIN |
| `ratingScore` | Rating |
| `reviewTitle` | Title |
| `reviewDescription` | Review Description |
| `isVerified` | Verified |
| `reviewedIn` | Reviewed In |
| `reviewReaction` | Review Reaction |
| `variant` | Variant |
| `reviewImages` | Review Images |
| `reviewId` | Review ID |
| `helpfulCount` | Helpful |
| `reviewDate` | Date |
| `reviewLocation` | Location |
| `sentimentHint` | Sentiment |
| `wordCount` | Words |
| `hasImages` | Has Images |
| `imageCount` | Image Count |
| `reviewUrl` | Review URL |
| `isVineVoice` | Vine |
| `reviewVideos` | Review Videos |
| `hasVideos` | Has Videos |
| `reviewHash` | Review Hash |
| `source` | Source |
| `sourceMarketplace` | Marketplace |
| `reviewedProductAsin` | Reviewed Product Asin |

The full dataset has 3 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `reviewId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-customer-review-and-rating-summary-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
