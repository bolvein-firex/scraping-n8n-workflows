# Washington Trails Association Hike & Trip Report Finder: free n8n workflow

A free n8n workflow that runs the [Washington Trails Association Hike & Trip Report Finder](https://apify.com/dataspryva/washington-trails-association-hike-and-trip-report) Apify Actor and returns `trailName`, `region`, `lengthMiles`, `rating`, `reviewCount` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Washington Trails Association hike
- Platform: Washington Trails Association
- Workflow file: [workflows/washington-trails-association-hike-and-trip-report-finder.json](../workflows/washington-trails-association-hike-and-trip-report-finder.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/washington-trails-association-hike-and-trip-report-finder.json`)
- Actor: https://apify.com/dataspryva/washington-trails-association-hike-and-trip-report
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/washington-trails-association-hike-and-trip-report-finder/SKILL.md

## What it does

Find Washington State hikes by region or keyword with length, elevation, rating and feature data, pull full trail stats and coordinates by hike URL, or check recent trip report activity.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | searchTrails | What to fetch from wta.org. |
| `searchQuery` | string | no |  | Free-text search of WTA hike descriptions (modes searchTrails, searchTripReports). |
| `nameQuery` | string | no |  | Match the hike name only (modes searchTrails, getTripReports, searchTripReports). |
| `region` | string | no |  | Washington region. Choose All Washington to search statewide (modes searchTrails, getTripReports, searchTripReports). |
| `subregion` | string | no | all | Optional sub-region. Selecting one also selects its parent region. |
| `features` | array | no | [] | Require all selected features (mode searchTrails). Empty = no feature filter. |
| `dogPolicy` | string | no | any | Filter by dog access (mode searchTrails). |
| `kidFriendly` | boolean | no | false | Only kid-friendly trails (mode searchTrails). |
| `wheelchairFriendly` | boolean | no | false | Only wheelchair-friendly trails (mode searchTrails). |
| `minRating` | number | no |  | Minimum average community rating, 0–5 (mode searchTrails). |
| `minVoteCount` | integer | no |  | Minimum number of rating votes (mode searchTrails; applied after the listing fetch). |
| `minLengthMiles` | number | no |  | Only trails at least this long (mode searchTrails). Trails with unknown length are excluded. |

27 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "region": "Snoqualmie Region",
  "tripReportsPerTrail": 3,
  "maxItems": 25,
  "mode": "searchTrails",
  "searchQuery": "head of growth"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.2:

| Field | Label |
|---|---|
| `trailName` | Trail Name |
| `region` | Region |
| `lengthMiles` | Length Miles |
| `elevationGainFeet` | Elevation Gain Feet |
| `difficulty` | Difficulty |
| `rating` | Rating |
| `reviewCount` | Review Count |
| `tripReportCount` | Trip Report Count |
| `latitude` | Latitude |
| `longitude` | Longitude |
| `trailUrl` | Trail Url |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/washington-trails-association-hike-and-trip-report-finder.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
