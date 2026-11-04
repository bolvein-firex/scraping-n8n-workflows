# US Walkability, Transit & Bike Score Extractor: free n8n workflow

A free n8n workflow that runs the [US Walkability, Transit & Bike Score Extractor](https://apify.com/dataspryva/us-walkability-transit-and-bike-score-extractor) Apify Actor and returns `address`, `city`, `walkScore`, `transitScore`, `bikeScore` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Walk Score for a list of addresses
- Platform: Walk Score
- Workflow file: [workflows/us-walkability-transit-and-bike-score-extractor.json](../workflows/us-walkability-transit-and-bike-score-extractor.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/us-walkability-transit-and-bike-score-extractor.json`)
- Actor: https://apify.com/dataspryva/us-walkability-transit-and-bike-score-extractor
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/us-walkability-transit-and-bike-score-extractor/SKILL.md

## Watch the Short

- [Compare walk, transit, and bike scores by listing](https://www.youtube.com/shorts/yCT9c3LRopU)

## What it does

Looks up Walk Score, Transit Score, and Bike Score for any US city or street address, returning each 0-100 score with its rating label and nearby amenity categories.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | byCity | What to look up. |
| `addresses` | array | no | [] | US street addresses, e.g. '1 Beach St, San Francisco, CA 94133'. walkscore.com/score/... URLs are also accepted. |
| `cities` | array | no | ["Seattle, WA"] | Cities as 'Seattle, WA', 'Seattle-WA', or a walkscore.com city URL. |
| `neighborhoods` | array | no | [] | Neighborhoods as 'Ballard, Seattle, WA' or a walkscore.com neighborhood URL. |
| `state` | string | no | WA | US state whose city table to read. |
| `includeNeighborhoods` | boolean | no | true | Add the city page's neighborhood ranking table to each city record. |
| `maxItems` | integer | no | 50 | Maximum records to emit (state summary counts as one). |

Starter input (edit it in **Configure input**):

```json
{
  "mode": "byCity",
  "addresses": [],
  "cities": [
    "Seattle, WA"
  ],
  "neighborhoods": [],
  "state": "WA",
  "includeNeighborhoods": true,
  "maxItems": 50
}
```

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `address` | Address |
| `locationType` | Location Type |
| `city` | City |
| `state` | State |
| `zipCode` | Zip Code |
| `walkScore` | Walk Score |
| `walkDescription` | Walk Description |
| `transitScore` | Transit Score |
| `transitDescription` | Transit Description |
| `bikeScore` | Bike Score |
| `bikeDescription` | Bike Description |
| `nearbyAmenities` | Nearby Amenities |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/us-walkability-transit-and-bike-score-extractor.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
