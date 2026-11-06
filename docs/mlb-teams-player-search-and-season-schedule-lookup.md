# MLB Teams, Player Search & Season Schedule Lookup: free n8n workflow

A free n8n workflow that runs the [MLB Teams, Player Search & Season Schedule Lookup](https://apify.com/vexaloom-labs/mlb-teams-player-search-and-season-schedule-lookup) Apify Actor and returns `teamName`, `playerName`, `eventName`, `homeTeam`, `awayTeam` and more as clean, deduped rows for Google Sheets or your next node.

- Job: MLB teams, player search
- Platform: MLB
- Workflow file: [workflows/mlb-teams-player-search-and-season-schedule-lookup.json](../workflows/mlb-teams-player-search-and-season-schedule-lookup.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/mlb-teams-player-search-and-season-schedule-lookup.json`)
- Actor: https://apify.com/vexaloom-labs/mlb-teams-player-search-and-season-schedule-lookup
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/mlb-teams-player-search-and-season-schedule-lookup/SKILL.md

## What it does

Look up every current MLB team, search for a player by name, or pull a full season's schedule and scores, with stadium, roster, and matchup details for each record.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | teams | What data to fetch. |
| `searchQuery` | string | no | Shohei Ohtani | Player name for players mode. |
| `season` | string | no | 2024 | MLB season year. |
| `maxItems` | integer | no | 20 | Maximum records to return. |

Starter input (edit it in **Configure input**):

```json
{
  "mode": "teams"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 20, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.3:

| Field | Label |
|---|---|
| `teamName` | Team Name |
| `playerName` | Player Name |
| `eventName` | Event Name |
| `homeTeam` | Home Team |
| `awayTeam` | Away Team |
| `matchDate` | Match Date |

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/mlb-teams-player-search-and-season-schedule-lookup.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
