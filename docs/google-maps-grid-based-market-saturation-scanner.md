# Google Maps Grid-Based Market Saturation Scanner: free n8n workflow

A free n8n workflow that runs the [Google Maps Grid-Based Market Saturation Scanner](https://apify.com/dataspryva/google-maps-grid-based-market-saturation-scanner) Apify Actor and returns `name`, `categoryName`, `totalScore`, `reviewsCount`, `phone` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google Maps search beyond 120 results
- Platform: Google Maps
- Workflow file: [workflows/google-maps-grid-based-market-saturation-scanner.json](../workflows/google-maps-grid-based-market-saturation-scanner.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-maps-grid-based-market-saturation-scanner.json`)
- Actor: https://apify.com/dataspryva/google-maps-grid-based-market-saturation-scanner
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-maps-grid-based-market-saturation-scanner/SKILL.md

## Watch the Short

- [Map HVAC competitors block by block](https://www.youtube.com/shorts/uom3-Fy_xFk)

## What it does

Cover a bounding box, circle, or custom polygon with a search grid to collect every business Google Maps exposes for a query, well beyond the usual 120-result cap on a single search.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `searchQuery` | string | yes |  | Type of business to search for (e.g., 'pharmacy', 'restaurant', 'dentist'). |
| `locationName` | string | no |  | Name of a public Google Maps location (e.g., 'Brooklyn, NY'). Google resolves its real center anonymously, then the actor scans the user-controlled radiusKm around it. |
| `boundingBox` | object | no |  | Geographic bounding box defining the scan area. Provide north/south/east/west coordinates. |
| `circleCenter` | object | no |  | Center point for a circular scan area. Use with radiusKm. |
| `radiusKm` | number | no | 5 | Radius in kilometers for circular scan area (used with circleCenter or locationName). |
| `customGeolocation` | object | no |  | Custom GeoJSON Polygon defining the scan boundary. |
| `zoomLevel` | integer | no | 15 | Controls grid cell granularity. Higher = smaller cells, more thorough coverage. |
| `maxPlacesPerCell` | integer | no | 120 | Maximum businesses to collect from each grid cell (1–260; Google's ranked window for one cell reaches roughly 136–213 places). |
| `maxPagesPerCell` | integer | no | 13 | How many 20-result pages to read per cell. Deeper pages surface more businesses — page 1 finds about 20% of a cell's places, page 9 finds all of them. |
| `maxTotalResults` | integer | no | 10000 | Maximum total businesses to extract across all cells. Stops scanning when reached. |
| `deduplicateResults` | boolean | no | true | Remove duplicate businesses that appear in multiple adjacent grid cells. |
| `enrichDetails` | boolean | no | false | Open each place's page for extra fields (price level, Plus Code, photo sample, rating histogram, open/closed status). |

2 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "keyword": "coffee shop",
  "location": "Denver, CO",
  "gridSize": 7,
  "radius": 5,
  "maxResultsPerPoint": 20
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `name` | Name |
| `categoryName` | Category |
| `totalScore` | Rating |
| `reviewsCount` | Reviews |
| `address` | Address |
| `phone` | Phone |
| `website` | Website |
| `placeId` | Place Id |
| `featureId` | Feature Id |
| `kgmid` | Kgmid |
| `googleMapsUrl` | Google Maps Url |
| `location` | Location |
| `rankInCell` | Rank In Cell |

The full dataset has 16 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-maps-grid-based-market-saturation-scanner.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
