# Apartments.com Rental Listing & Floor Plan Scraper: free n8n workflow

A free n8n workflow that runs the [Apartments.com Rental Listing & Floor Plan Scraper](https://apify.com/dataspryva/apartments-com-rental-listing-and-floor-plan) Apify Actor and returns `name`, `address`, `priceMin`, `priceMax`, `priceCurrency` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Apartments.com rental listing scraper
- Platform: Apartments.com
- Workflow file: [workflows/apartments-com-rental-listing-and-floor-plan-scraper.json](../workflows/apartments-com-rental-listing-and-floor-plan-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/apartments-com-rental-listing-and-floor-plan-scraper.json`)
- Actor: https://apify.com/dataspryva/apartments-com-rental-listing-and-floor-plan
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/apartments-com-rental-listing-and-floor-plan-scraper/SKILL.md

## What it does

Search Apartments.com rentals by city, bedroom count, price, property type, pet policy, and amenities, or scrape specific listing URLs directly. Returns rent ranges, per-unit floor plans, walkability scores, amenities, and leasing contact details.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | search | How to find listings: `search` uses a city or ZIP plus filters; `urls` uses the Apartments.com URLs you paste; `listingKeys` looks up the listing keys you paste. |
| `searchLocation` | string | no |  | US city and state (`New York, NY`) or 5-digit ZIP (`10001`). Used only in search mode. |
| `bedrooms` | string | no | any | Match listings with at least one floor plan of this bedroom count. |
| `bathrooms` | string | no | any | Match listings with a floor plan at or above this bathroom count. |
| `priceMin` | integer | no |  | Lowest monthly rent to include. Leave unset for no minimum. |
| `priceMax` | integer | no |  | Highest monthly rent to include. Leave unset for no maximum. |
| `sqftMin` | integer | no |  | Smallest floor plan to include. Leave unset for no minimum. |
| `sqftMax` | integer | no |  | Largest floor plan to include. Leave unset for no maximum. |
| `propertyType` | string | no | any | Restrict results to one property type. |
| `petPolicy` | string | no | any | Require listings that allow dogs, cats, or both. |
| `amenities` | array | no | [] | Only return listings that publish every selected amenity. |
| `rentSpecials` | boolean | no | false | Only return listings advertising a current move-in deal. |

11 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchLocation": "New York, NY",
  "maxItems": 25,
  "maxPages": 1
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 2.0.1:

| Field | Label |
|---|---|
| `name` | Name |
| `address` | Address |
| `city` | City |
| `state` | State |
| `zipCode` | Zip Code |
| `priceMin` | Price Min |
| `priceMax` | Price Max |
| `priceCurrency` | Price Currency |
| `bedsMin` | Beds Min |
| `bedsMax` | Beds Max |
| `propertyType` | Property Type |
| `rating` | Rating |
| `photoCount` | Photo Count |
| `propertyManager` | Property Manager |
| `url` | Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `url` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/apartments-com-rental-listing-and-floor-plan-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
