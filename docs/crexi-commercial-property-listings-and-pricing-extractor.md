# Crexi Commercial Property Listings & Pricing Extractor: free n8n workflow

A free n8n workflow that runs the [Crexi Commercial Property Listings & Pricing Extractor](https://apify.com/dataspryva/crexi-commercial-property-listings-and-pricing) Apify Actor and returns `name`, `transaction_type`, `property_type`, `price`, `net_operating_income` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Crexi commercial property listings scraper
- Platform: Crexi
- Workflow file: [workflows/crexi-commercial-property-listings-and-pricing-extractor.json](../workflows/crexi-commercial-property-listings-and-pricing-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/crexi-commercial-property-listings-and-pricing-extractor.json`)
- Actor: https://apify.com/dataspryva/crexi-commercial-property-listings-and-pricing
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/crexi-commercial-property-listings-and-pricing-extractor/SKILL.md

## What it does

Collects active commercial real estate listings from Crexi across any US state and 14 property types, with asking price, square footage, location, and brokerage details.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `propertyUrls` | array | no | [] | Paste Crexi property links or IDs (e.g. `https://www.crexi.com/properties/123456/name,` /lease/properties/987/name, a bare ID, or a property-record link) to fetch those exact… |
| `transactionTypes` | array | no | [] | Which Crexi marketplaces to search. Empty = for-sale listings only. |
| `searchTerms` | array | no | [] | Free-text keywords matched against listing names, descriptions and addresses (e.g. warehouse, medical office). |
| `propertyTypes` | array | no | [] | One or more commercial property categories. Empty searches every type. |
| `subtypes` | array | no | [] | Narrow to specific subtypes (e.g. Shopping Center, Medical Office, Warehouse). Note: some subtypes exist only for sale or only for lease listings. |
| `locations` | array | no | [] | US states to search, by two-letter code or full name. Each state is searched and combined. Empty searches nationwide. |
| `cities` | array | no | [] | City names to filter by (e.g. Austin). Works alongside or instead of states. |
| `counties` | array | no | [] | County names to filter by, including the word County where Crexi uses it (e.g. Travis County). |
| `zipCodes` | array | no | [] | US ZIP codes to filter by (e.g. 78701). |
| `minPrice` | integer | no |  | Only return listings asking at least this much. Sale and auction listings only. |
| `maxPrice` | integer | no |  | Only return listings asking at most this much. Sale and auction listings only. |
| `minPricePerSqft` | number | no |  | Only return sale listings priced at or above this per square foot. |

15 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "maxProperties": 5
}
```

The input passes the Actor's input schema (checked at every publish). The run size follows the number of inputs you pass.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `name` | Property Name |
| `transaction_type` | Kind |
| `property_type` | Type |
| `city` | City |
| `state` | State |
| `price` | Price |
| `cap_rate` | Cap Rate % |
| `net_operating_income` | NOI |
| `building_sqft` | Building SqFt |
| `broker_names` | Brokers |
| `property_url` | URL |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/crexi-commercial-property-listings-and-pricing-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
