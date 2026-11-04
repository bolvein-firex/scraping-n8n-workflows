# Booking.com Hotel Price & Amenity Search Scraper: free n8n workflow

A free n8n workflow that runs the [Booking.com Hotel Price & Amenity Search Scraper](https://apify.com/nimbryxo-studio/booking-com-hotel-price-and-amenity-search-scraper) Apify Actor and returns `name`, `price`, `pricePerNight`, `rating`, `reviewCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Booking.com hotel prices for your dates
- Platform: Booking.com
- Workflow file: [workflows/booking-com-hotel-price-and-amenity-search-scraper.json](../workflows/booking-com-hotel-price-and-amenity-search-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/booking-com-hotel-price-and-amenity-search-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/booking-com-hotel-price-and-amenity-search-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/booking-com-hotel-price-and-amenity-search-scraper/SKILL.md

## Watch the Short

- [Compare hotel prices before your weekly check](https://www.youtube.com/shorts/jQWhZPI54SI)

## What it does

Search Booking.com for a destination and dates, and collect each property's price, rating, review count, amenities, and breakfast info for the stay you specify.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | search | Search a destination, or load specific Booking.com hotel URLs. |
| `destination` | string | no |  | City, region or landmark to search, e.g. Paris, New York or Tokyo. Required in search mode. |
| `startUrls` | array | no | [] | Booking.com hotel page URLs, used in details mode. Copy links from a search result or your browser. |
| `checkIn` | string | no |  | Check-in date as YYYY-MM-DD. Leave empty to use tomorrow. |
| `checkOut` | string | no |  | Check-out date as YYYY-MM-DD. Leave empty to use a 3-night stay. |
| `adults` | integer | no | 2 | Number of adult guests. |
| `rooms` | integer | no | 1 | Number of rooms needed. |
| `propertyType` | string | no | all | Keep only one Booking.com property type, or search all types. |
| `minReviewScore` | number | no | 0 | Minimum guest score from 0 to 10. The actor applies Booking.com's score filter and then keeps only properties at or above this exact score. |
| `stars` | string | no | 0 | Keep only properties with this star rating, or any star rating. |
| `freeCancellation` | boolean | no | false | Return properties with at least one free-cancellation rate. |
| `breakfast` | boolean | no | false | Return properties with a breakfast-included rate. |

9 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "search",
  "startUrls": [],
  "adults": 2,
  "rooms": 1,
  "propertyType": "all",
  "minReviewScore": 0,
  "stars": "0",
  "freeCancellation": false,
  "breakfast": false,
  "pool": false,
  "currency": "USD",
  "language": "en-us",
  "maxItems": 3,
  "includeRooms": true,
  "includeFullAmenities": false
}
```

## Output fields

Columns from the Actor's dataset schema, build 2.0.2:

| Field | Label |
|---|---|
| `name` | Hotel |
| `price` | Stay total |
| `pricePerNight` | Per night |
| `currency` | Currency |
| `rating` | Rating |
| `reviewCount` | Reviews |
| `reviewWord` | Score word |
| `stars` | Stars |
| `propertyType` | Type |
| `city` | City |
| `country` | Country |
| `freeCancellation` | Free cancellation |
| `breakfastIncluded` | Breakfast |
| `topAmenities` | Top amenities |
| `url` | URL |

The full dataset has 30 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/booking-com-hotel-price-and-amenity-search-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
