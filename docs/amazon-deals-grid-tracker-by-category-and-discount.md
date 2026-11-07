# Amazon Deals Grid Tracker by Category & Discount: free n8n workflow

A free n8n workflow that runs the [Amazon Deals Grid Tracker by Category & Discount](https://apify.com/dataspryva/amazon-deals-grid-tracker-by-category-and-discount) Apify Actor and returns `asin`, `title`, `dealPrice`, `savingsPercent`, `averageRating` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Amazon deals grid
- Platform: Amazon
- Workflow file: [workflows/amazon-deals-grid-tracker-by-category-and-discount.json](../workflows/amazon-deals-grid-tracker-by-category-and-discount.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-deals-grid-tracker-by-category-and-discount.json`)
- Actor: https://apify.com/dataspryva/amazon-deals-grid-tracker-by-category-and-discount
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/amazon-deals-grid-tracker-by-category-and-discount/SKILL.md

## Watch the Short

- [Catch Amazon deals before Monday's price check](https://www.youtube.com/shorts/rbaQJ__OtNg)

## What it does

Pull Amazon's Today's Deals grid across 23 marketplaces, with deal price, list price, savings amount/percent, deal type, brand, and department for each product. Filter by category, brand, price range, and discount range.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `marketplace` | string | yes | amazon.com | Which Amazon domain's Today's Deals page to scrape. |
| `categories` | array | no | [] | Amazon departments to scan. Common names: Electronics, Home & Kitchen, Kitchen, Beauty & Personal Care, Clothing Shoes & Jewelry, Toys & Games, Sports & Outdoors, Books, Pet… |
| `collection` | string | no |  | Restrict to one of Amazon's curated deal collections. The collection names differ by marketplace; unsupported collections return a clear status record instead of unfiltered data. |
| `brand` | string | no |  | Case-insensitive brand name substring (e.g. Anker, Samsung). Leave empty for all brands. |
| `minRating` | integer | no |  | Keep only deals whose product rating is at least this value. Deals without a rating are excluded when this is set. |
| `priceMin` | integer | no |  | Keep deals at or above this price in the marketplace's local currency. |
| `priceMax` | integer | no |  | Keep deals at or below this price in the marketplace's local currency. |
| `discountMin` | integer | no |  | Keep deals with at least this percentage off, filtered by Amazon itself. |
| `discountMax` | integer | no |  | Keep deals with at most this percentage off, filtered by Amazon itself. |
| `primeExclusiveOnly` | boolean | no | false | Only return deals in Amazon's Prime Exclusive collection. |
| `sortBy` | string | no | featured | Featured keeps Amazon's order. Other sorts read the fetched deal window before returning, so they may take longer. |
| `maxItems` | integer | no | 30 | Hard cap on emitted deal records. Amazon exposes up to 500 deals per category/collection query; add categories to partition the window. |

Starter input (edit it in **Configure input**):

```json
{
  "maxItems": 25,
  "marketplace": "amazon.com"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `asin` | Asin |
| `title` | Title |
| `dealPrice` | Deal Price |
| `savingsPercent` | Savings Percent |
| `averageRating` | Average Rating |
| `dealEndsAt` | Deal Ends At |
| `category` | Category |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `asin` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-deals-grid-tracker-by-category-and-discount.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
