# Airbnb Listing Price & Location Finder: free n8n workflow

A free n8n workflow that runs the [Airbnb Listing Price & Location Finder](https://apify.com/nimbryxo-studio/airbnb-listing-price-and-location-finder) Apify Actor and returns `name`, `nightlyPrice`, `totalPrice`, `rating`, `reviewCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Airbnb price scraper
- Platform: Airbnb
- Workflow file: [workflows/airbnb-listing-price-and-location-finder.json](../workflows/airbnb-listing-price-and-location-finder.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/airbnb-listing-price-and-location-finder.json`)
- Actor: https://apify.com/nimbryxo-studio/airbnb-listing-price-and-location-finder
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/airbnb-listing-price-and-location-finder/SKILL.md

## Watch the Short

- [Price the market, not the gut](https://www.youtube.com/shorts/aVEDRMB3vsU)

## What it does

Search Airbnb by location and stay dates for listing price, rating, Superhost and verification status, GPS coordinates, and photos per property.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | search | Search discovers listings by location or map area. Details loads the listing URLs or IDs you provide. |
| `location` | string | no |  | City, region, country or neighborhood, e.g. New York, Paris, SoHo. Airbnb's own location lookup validates the name before searching (mode=search). |
| `placeId` | string | no |  | Optional Google/Airbnb place ID (e.g. ChIJOwg_06VPwokRYv534QaPC8g). Takes precedence over the resolved location and skips text matching (mode=search). |
| `neighborhood` | string | no |  | Optional neighborhood to combine with Location, e.g. SoHo + New York (mode=search). |
| `bbox` | object | no |  | Search inside a map rectangle instead of a named location. Use decimal degrees: swLat, swLng (south-west corner) and neLat, neLng (north-east corner), plus an optional zoom… |
| `listingUrls` | array | no |  | Airbnb room URLs, e.g. `https://www.airbnb.com/rooms/23222680` (mode=details). |
| `listingIds` | array | no |  | Numeric Airbnb listing IDs, e.g. 23222680. You can mix these with listing URLs (mode=details). |
| `checkIn` | string | no |  | Stay start date in YYYY-MM-DD format. Leave both dates empty to use Airbnb's displayed quote (search) or to skip the price quote (details). |
| `checkOut` | string | no |  | Stay end date in YYYY-MM-DD format. Must be after the check-in date. |
| `adults` | integer | no | 1 | Number of adult guests (1-16). |
| `children` | integer | no | 0 | Number of children aged 2-12 (0-15). |
| `infants` | integer | no | 0 | Number of infants under 2 (0-5). |

17 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "location": "Miami, FL",
  "checkIn": "2026-11-14",
  "checkOut": "2026-11-16",
  "maxListings": 500
}
```

## Output fields

Columns from the Actor's dataset schema, build 2.0.1:

| Field | Label |
|---|---|
| `name` | Name |
| `nightlyPrice` | Nightly price |
| `totalPrice` | Stay total |
| `currency` | Currency |
| `rating` | Rating |
| `reviewCount` | Reviews |
| `location` | Location |
| `roomType` | Room type |
| `url` | URL |

The full dataset has 21 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/airbnb-listing-price-and-location-finder.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
