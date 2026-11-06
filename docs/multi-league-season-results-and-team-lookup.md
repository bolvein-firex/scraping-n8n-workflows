# Multi-League Season Results & Team Lookup: free n8n workflow

A free n8n workflow that runs the [Multi-League Season Results & Team Lookup](https://apify.com/dataspryva/multi-league-season-results-and-team-lookup) Apify Actor and returns `homeTeam`, `awayTeam`, `homeScore`, `awayScore`, `matchDate` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Multi-League season results
- Platform: Multi-League
- Workflow file: [workflows/multi-league-season-results-and-team-lookup.json](../workflows/multi-league-season-results-and-team-lookup.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/multi-league-season-results-and-team-lookup.json`)
- Actor: https://apify.com/dataspryva/multi-league-season-results-and-team-lookup
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/multi-league-season-results-and-team-lookup/SKILL.md

## What it does

Get final scores for a season across 10 major soccer, football, basketball, baseball, and hockey leagues, or look up every team's roster details for a league in one run.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | results | Season results with odds, a league's team roster, or a team lookup by name. |
| `sport` | string | no | epl | Which competition to fetch. Ignored when leagueUrls is set. |
| `season` | string | no | 2024-2025 | Season to fetch. Soccer-style seasons use YYYY-YYYY (a plain YYYY expands to YYYY-YYYY); calendar-year leagues (MLB, MLS, NPB, J1, K League) use YYYY; 'current' is the live… |
| `leagueUrls` | array | no |  | Optional: one or more OddsPortal league or season-results URLs (any sport or league, e.g. `https://www.oddsportal.com/football/england/premier-league-2024-2025/results/`). |
| `teamQuery` | string | no |  | Team to look up by name (teamSearch mode), e.g. Arsenal or Real Madrid. |
| `includeOdds` | boolean | no | true | Add 1X2 average and maximum odds, bookmaker count and per-bookmaker prices to each result. |
| `includeUpcoming` | boolean | no | true | Keep scheduled and in-progress matches; turn off to get only finished results. |
| `enrichTeams` | boolean | no | true | In teams and teamSearch modes, open each team's page for its full name, venue, city, country and coach. Adds one request per team. |
| `regionalFallback` | boolean | no | true | When a league-season is empty on the main domain, retry it on the same site's regional edition (a few competitions, e.g. ACB, only publish older seasons there). |
| `maxItems` | integer | no | 20 | Maximum records to return (1-10000). The run also stops when the source runs out of pages. |

Starter input (edit it in **Configure input**):

```json
{
  "teamQuery": "Arsenal",
  "enrichTeams": false,
  "mode": "results"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 20, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `homeTeam` | Home Team |
| `awayTeam` | Away Team |
| `homeScore` | Home Score |
| `awayScore` | Away Score |
| `matchDate` | Match Date |
| `status` | Status |
| `oddsHome` | Odds Home |
| `oddsDraw` | Odds Draw |
| `oddsAway` | Odds Away |
| `bookmakerCount` | Bookmaker Count |

The full dataset has 15 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/multi-league-season-results-and-team-lookup.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
