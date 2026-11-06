# Google Flights Fare & Itinerary Filter Scraper: free n8n workflow

A free n8n workflow that runs the [Google Flights Fare & Itinerary Filter Scraper](https://apify.com/vexaloom-labs/google-flights-fare-and-itinerary-filter-scraper) Apify Actor and returns `price`, `airline`, `departureAirport`, `departureTime`, `arrivalAirport` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google Flights fare scraper
- Platform: Google Flights
- Workflow file: [workflows/google-flights-fare-and-itinerary-filter-scraper.json](../workflows/google-flights-fare-and-itinerary-filter-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-flights-fare-and-itinerary-filter-scraper.json`)
- Actor: https://apify.com/vexaloom-labs/google-flights-fare-and-itinerary-filter-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-flights-fare-and-itinerary-filter-scraper/SKILL.md

## What it does

Search Google Flights for one-way or round-trip fares across any cabin class, then narrow results by stops, total duration, airline, and price range, with an optional price-alert flag.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | Search flights, or collect the cheapest fare for each date around your departure date. |
| `originAirport` | string | no | JFK | Three-letter IATA airport or city code, e.g. JFK, LHR, NYC. One code per search; use `searches` for alternate airports. |
| `destinationAirport` | string | no | LHR | Three-letter IATA airport or city code, e.g. LHR, HND, LON. One code per search; use `searches` for alternate airports. |
| `outboundDate` | string | no |  | Departure date in YYYY-MM-DD format. Leave empty to use 30 days from today (UTC); the chosen date is logged. |
| `returnDate` | string | no |  | Return date in YYYY-MM-DD format. Leave empty for a one-way search. |
| `adults` | integer | no | 1 | Travellers aged 12 and over (1-9). |
| `children` | integer | no | 0 | Travellers aged 2-11 (0-8). |
| `infants` | integer | no | 0 | Infants under 2 travelling on an adult lap (0-8). Cannot exceed the number of adults. |
| `infantsInSeat` | integer | no | 0 | Infants under 2 travelling in their own seat (0-8). |
| `cabinClass` | string | no | economy | Cabin to search. |
| `currency` | string | no | USD | Currency for every price. |
| `language` | string | no | en | Language Google Flights uses for airport and airline names. |

18 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "outboundDate": "2026-12-10",
  "maxResults": 25,
  "includePriceInsights": false,
  "priceGraphDays": 1,
  "mode": "search"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxResults` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.2:

| Field | Label |
|---|---|
| `price` | Price |
| `currency` | Currency |
| `airline` | Airline |
| `departureAirport` | Departure Airport |
| `departureTime` | Departure Time |
| `arrivalAirport` | Arrival Airport |
| `arrivalTime` | Arrival Time |
| `durationMinutes` | Duration Minutes |
| `stops` | Stops |
| `emissionsGrams` | Emissions Grams |
| `bookingUrl` | Booking Url |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-flights-fare-and-itinerary-filter-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
