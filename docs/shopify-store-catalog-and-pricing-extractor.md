# Shopify Store Catalog & Pricing Extractor: free n8n workflow

A free n8n workflow that runs the [Shopify Store Catalog & Pricing Extractor](https://apify.com/nimbryxo-studio/shopify-store-catalog-and-pricing-extractor) Apify Actor and returns `title`, `price`, `compareAtPrice`, `available`, `vendor` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Scrape a Shopify store's products and prices
- Platform: Shopify
- Workflow file: [workflows/shopify-store-catalog-and-pricing-extractor.json](../workflows/shopify-store-catalog-and-pricing-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/shopify-store-catalog-and-pricing-extractor.json`)
- Actor: https://apify.com/nimbryxo-studio/shopify-store-catalog-and-pricing-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/shopify-store-catalog-and-pricing-extractor/SKILL.md

## Watch the Short

- [See competitor prices before Monday's meeting](https://www.youtube.com/shorts/398NV7q-K6w)

## What it does

Extract a Shopify store's product catalog with titles, prices, compare-at prices, variants, SKUs, images and stock availability from any custom or myshopify.com domain.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | catalog | What to scrape. `catalog` walks the public product feed, `collection` walks specific collections, `product` fetches exact product handles, `search` uses the storefront search… |
| `storeUrls` | array | no |  | Store domains or URLs, e.g. `deathwishcoffee.com` or `https://www.allbirds.com`. Accepts custom domains and `*.myshopify.com`. |
| `startUrls` | array | no | [] | Store, collection or product URLs. In `auto` mode each URL selects its own job: `/products/` fetches one product, `/collections/` fetches a collection, any other store URL fetches… |
| `collectionHandles` | array | no | [] | Collection handles or collection URLs, e.g. `new-arrivals`, `sale`, or `https://store.com/collections/sale`. |
| `productHandles` | array | no | [] | Product handles or product URLs, e.g. `dark-roast-coffee` or `https://store.com/products/dark-roast-coffee`. |
| `searchQuery` | string | no |  | In-store search term. Shopify's public suggest endpoint returns at most 10 products per store and has no pagination. |
| `currency` | string | no | store | ISO 4217 code to pin prices to, e.g. `USD`, `EUR`, `GBP`. Use `store` to use the store's base currency from `/meta.json`. |
| `country` | string | no |  | Two-letter ISO country code passed as `?country=` to the storefront, e.g. `US`, `GB`, `DE`. |
| `vendor` | string | no |  | Keep products whose vendor contains this text (case-insensitive). |
| `productType` | string | no |  | Keep products whose product type contains this text (case-insensitive). |
| `tag` | string | no |  | Keep products with at least one tag containing this text (case-insensitive). |
| `minPrice` | number | no |  | Drop products whose lowest variant price is below this value. |

7 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "catalog",
  "storeUrls": [
    "https://deathwishcoffee.com"
  ],
  "maxItems": 50,
  "currency": "store",
  "available": "any",
  "includeDetails": false,
  "flattenVariants": false
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 50, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 2.0.2:

| Field | Label |
|---|---|
| `title` | Title |
| `price` | Price |
| `currency` | Currency |
| `compareAtPrice` | Compare at |
| `available` | Available |
| `vendor` | Vendor |
| `productType` | Type |
| `storeUrl` | Store |
| `url` | Product URL |

The full dataset has 33 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `url` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/shopify-store-catalog-and-pricing-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
