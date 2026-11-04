# Google Shopping Price Comparison & Deal Finder: free n8n workflow

A free n8n workflow that runs the [Google Shopping Price Comparison & Deal Finder](https://apify.com/vexaloom-labs/google-shopping-price-comparison-and-deal-finder) Apify Actor and returns `title`, `price`, `merchant`, `rating`, `reviewCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google Shopping price comparison
- Platform: Google Shopping
- Workflow file: [workflows/google-shopping-price-comparison-and-deal-finder.json](../workflows/google-shopping-price-comparison-and-deal-finder.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-shopping-price-comparison-and-deal-finder.json`)
- Actor: https://apify.com/vexaloom-labs/google-shopping-price-comparison-and-deal-finder
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-shopping-price-comparison-and-deal-finder/SKILL.md

## What it does

Search Google Shopping by keyword and collect product prices, discounts, merchant names, ratings, and delivery info across 48 countries for price monitoring and deal tracking.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | search | What to collect: keyword search, product lookup by ID/viewer URL, deals, or a department category. |
| `queries` | array | no |  | Product keywords for search/deals mode. Ignored in product mode; optional in category mode. |
| `productIds` | array | no |  | Google Shopping catalog IDs, product IDs, product viewer URLs, or legacy /shopping/product/ URLs. Used in product mode. |
| `category` | string | no |  | Google Shopping department for category mode. |
| `countryCode` | string | no | us | Country used for the Google domain, UULE location and price hint. The actual currency is always detected from the response, never relabelled. |
| `languageCode` | string | no | en | Interface and result language (hl parameter). |
| `sortBy` | string | no |  | Client-side sort of the collected rows. Google ignores server-side sort on this page. |
| `condition` | string | no |  | Condition hint sent to Google and verified when the result card shows a condition. |
| `minPrice` | integer | no |  | Minimum price in the detected local currency. Applied through a shoprs filter and verified on every output row. |
| `maxPrice` | integer | no |  | Maximum price in the detected local currency. Applied through a shoprs filter and verified on every output row. |
| `onSale` | boolean | no | false | Ask Google for discounted products and keep rows with an observed original price or discount. |
| `freeShipping` | boolean | no | false | Ask Google for free-shipping products and keep rows whose delivery text says free. |

5 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "search",
  "countryCode": "us",
  "languageCode": "en",
  "onSale": false,
  "freeShipping": false,
  "minRating": "0",
  "maxResultsPerQuery": 20,
  "includePriceHistory": true,
  "includeProductDetails": false
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `title` | Product |
| `price` | Price |
| `currency` | Currency |
| `merchant` | Merchant |
| `rating` | Rating |
| `reviewCount` | Reviews |

The full dataset has 40 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-shopping-price-comparison-and-deal-finder.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
