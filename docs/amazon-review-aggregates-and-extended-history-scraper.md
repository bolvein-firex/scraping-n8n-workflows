# Amazon Review Aggregates & Extended History Scraper: free n8n workflow

A free n8n workflow that runs the [Amazon Review Aggregates & Extended History Scraper](https://apify.com/dataspryva/amazon-review-aggregates-and-extended-history) Apify Actor and returns `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Amazon reviews across marketplaces
- Platform: Amazon
- Workflow file: [workflows/amazon-review-aggregates-and-extended-history-scraper.json](../workflows/amazon-review-aggregates-and-extended-history-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-review-aggregates-and-extended-history-scraper.json`)
- Actor: https://apify.com/dataspryva/amazon-review-aggregates-and-extended-history
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/amazon-review-aggregates-and-extended-history-scraper/SKILL.md

## What it does

Collect Amazon customer reviews and rating summaries by product URL, ASIN, or keyword across 19 marketplaces, with star-rating and sort filters, reviewer images, and an optional session for deeper review history.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `productUrls` | array | no |  | List of Amazon product URLs to scrape reviews from. Supports /dp/, /gp/product/, /gp/aw/d/ and /product/ URL formats across 19+ Amazon domains. A bare 10-character ASIN (e.g. |
| `keywords` | array | no | [] | Search keywords used to auto-discover products when `productUrls` is empty (e.g. "wireless earbuds"). |
| `categoryUrls` | array | no | [] | Advanced mode: supply your own Amazon `/s?...` or `/b?node=...` category/search URL(s) directly (used only when `productUrls` is empty). |
| `maxProductsToDiscover` | integer | no | 10 | Maximum number of products to discover per run from `keywords`/`categoryUrls`. Ignored when `productUrls` is supplied directly. |
| `extendedHistory` | boolean | no | true | Merge Amazon's public extended review feed for each ASIN (no login, no cookie): up to 100 reviews per star/sort bucket, and walking every bucket yields 100-850+ unique reviews for… |
| `mergeMarketplaces` | array | no | [] | Additional Amazon marketplaces whose product page is fetched for the same ASIN and whose reviews are merged (deduplicated by review ID and content). |
| `includeAggregates` | boolean | no | true | Emit one additional `amazon_review_aggregate` record per product with the product title, average rating, global ratings count, star histogram (plus derived per-star counts), and… |
| `country` | string | no | amazon.com | Amazon country domain to scrape from. URLs from a different domain are honored automatically. |
| `maxReviews` | integer | no | 100 | Hard cap on the number of reviews returned per product AFTER merging and deduplication (1-2000). |
| `sortBy` | string | no | helpful | How to sort the returned reviews: most helpful first, or most recent first. |
| `filterByStar` | string | no |  | Keep only reviews with this rating. `positive` keeps 4-5 star reviews; `critical` keeps 1-2 star reviews. |
| `verifiedPurchasesOnly` | boolean | no | false | Keep only reviews carrying Amazon's Verified Purchase badge. Applied server-side for the extended feed and client-side for product-page rows. |

5 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "productUrls": [
    "https://www.amazon.com/dp/B09X7MPX8L"
  ],
  "country": "amazon.com",
  "maxReviews": 30,
  "includeAggregates": true
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxProductsToDiscover` = 10, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.3:

| Field | Label |
|---|---|
| `productAsin` | ASIN |
| `reviewedProductAsin` | Reviewed Product Asin |
| `ratingScore` | Rating |
| `reviewTitle` | Title |
| `reviewDescription` | Review Description |
| `isVerified` | Verified |
| `isVineVoice` | Is Vine Voice |
| `reviewedIn` | Reviewed In |
| `reviewReaction` | Review Reaction |
| `variant` | Variant |
| `reviewImages` | Review Images |
| `reviewId` | Review ID |
| `reviewUrl` | Review Url |
| `helpfulCount` | Helpful |
| `reviewDate` | Date |
| `reviewLocation` | Location |
| `sentimentHint` | Sentiment |
| `wordCount` | Words |
| `hasImages` | Has Images |
| `imageCount` | Image Count |
| `hasVideos` | Has Videos |
| `videoCount` | Video Count |
| `reviewHash` | Review Hash |
| `source` | Source |
| `sourceMarketplace` | Marketplace |

The full dataset has 3 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `reviewId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-review-aggregates-and-extended-history-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
