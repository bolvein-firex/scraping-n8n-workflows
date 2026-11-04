# Amazon Multi-Domain Product Price & Detail Scraper: free n8n workflow

A free n8n workflow that runs the [Amazon Multi-Domain Product Price & Detail Scraper](https://apify.com/nimbryxo-studio/amazon-multi-domain-product-price-and-detail) Apify Actor and returns `title`, `asin`, `price`, `stars`, `reviewsCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Amazon price tracking
- Platform: Amazon
- Workflow file: [workflows/amazon-multi-domain-product-price-and-detail-scraper.json](../workflows/amazon-multi-domain-product-price-and-detail-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-multi-domain-product-price-and-detail-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/amazon-multi-domain-product-price-and-detail
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/amazon-multi-domain-product-price-and-detail-scraper/SKILL.md

## Watch the Short

- [The buy box moved while you slept](https://www.youtube.com/shorts/SqsDoB0jyD8)

## What it does

Pull pricing, ratings, seller, variant and technical detail for Amazon products by URL or ASIN, across 21 country domains, with optional delivery postal-code targeting.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `productUrls` | array | no | [] | Amazon product URLs to scrape. Any mix of the 21 supported country domains is allowed, e.g. `https://www.amazon.com/dp/B0B8PD8TTP.` |
| `asins` | array | no | [] | Bare 10-character Amazon ASINs. Builds /dp/{ASIN} URLs on the selected marketplace, or on every domain listed in `domains` for cross-marketplace runs. |
| `searchTerms` | array | no | [] | Keyword queries to run on Amazon search pages. Price/rating/deal/condition/sort filters are applied as URL parameters. |
| `searchUrls` | array | no | [] | Full Amazon search URLs to pass through, including your own `i=`, `rh=`, `low-price`, and `s=` parameters. Pagination is added automatically. |
| `bestsellerUrls` | array | no | [] | Amazon bestseller /zgbs/ or /gp/bestsellers/ list URLs. Returns the ranked product cards, optionally enriched with product-detail fields. |
| `marketplace` | string | no | auto | Marketplace used for bare ASINs and keyword search terms. `auto` uses the first product URL's domain, or amazon.com. |
| `domains` | array | no | [] | Optional list of marketplaces (e.g. amazon.com, amazon.de) to run bare ASINs and search terms across. Leave empty to use `marketplace` only. |
| `language` | string | no | auto | Page language. `auto` uses the marketplace's own default. Explicit values set `?language=` and the matching Accept-Language header. |
| `currency` | string | no | auto | ISO currency for the displayed price. `auto` uses the marketplace currency. Note: Amazon converts display currency; it is not guaranteed local retail pricing. |
| `deliveryCountry` | string | no | auto | Optional country hint. When `postalCode` is empty, a representative local ZIP for that country is used. A country alone is not sent to Amazon. |
| `postalCode` | string | no |  | Local ZIP/postal code for the delivery location. The actor validates it against the marketplace format and skips the location change if it does not match. |
| `minPrice` | number | no |  | Minimum price for discovery (search) results. Leave empty for no lower bound. |

19 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchTerms": [
    "wireless earbuds"
  ],
  "marketplace": "amazon.com",
  "maxItems": 25,
  "includeDetails": true,
  "dealsOnly": false
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.4:

| Field | Label |
|---|---|
| `title` | Product Title |
| `asin` | ASIN |
| `price` | Price |
| `stars` | Rating |
| `reviewsCount` | Reviews |
| `inStock` | In Stock |
| `brand` | Brand |
| `url` | URL |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `asin` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/amazon-multi-domain-product-price-and-detail-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
