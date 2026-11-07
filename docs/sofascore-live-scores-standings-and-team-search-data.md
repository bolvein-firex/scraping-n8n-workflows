# SofaScore Live Scores, Standings & Team Search Data: free n8n workflow

A free n8n workflow that runs the [SofaScore Live Scores, Standings & Team Search Data](https://apify.com/vexaloom-labs/sofascore-live-scores-standings-and-team-search) Apify Actor and returns `name`, `homeTeam`, `awayTeam`, `homeScore`, `awayScore` and more as clean, deduped rows for Google Sheets or your next node.

- Job: SofaScore live scores, standings
- Platform: SofaScore
- Workflow file: [workflows/sofascore-live-scores-standings-and-team-search-data.json](../workflows/sofascore-live-scores-standings-and-team-search-data.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/sofascore-live-scores-standings-and-team-search-data.json`)
- Actor: https://apify.com/vexaloom-labs/sofascore-live-scores-standings-and-team-search
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/sofascore-live-scores-standings-and-team-search-data/SKILL.md

## Watch the Short

- [Build a live football score sheet by matchday](https://www.youtube.com/shorts/qMmkq9VlH8k)

## What it does

Get SofaScore live scores, scheduled fixtures, league standings and team/player/tournament search results across 17 sports including football, basketball and tennis.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to fetch from SofaScore. |
| `searchQueries` | array | no |  | Team, player, tournament or match names to resolve (mode=search). |
| `searchType` | string | no | all | Restrict search results to one entity type (mode=search). |
| `sports` | array | no | ["football"] | Sports for live and scheduled modes. Supported: football, basketball, tennis, american-football, aussie-rules, ice-hockey, handball, rugby, futsal, minifootball, floorball… |
| `date` | string | no |  | Start date for fixtures (mode=scheduled), format YYYY-MM-DD. Defaults to today UTC. |
| `daysAhead` | integer | no | 0 | Number of extra days after Date to include (mode=scheduled). |
| `teamIds` | array | no |  | SofaScore team IDs or team page URLs (mode=team). |
| `playerIds` | array | no |  | SofaScore player IDs or player page URLs (mode=player). |
| `tournamentIds` | array | no |  | SofaScore unique-tournament IDs or tournament page URLs (modes tournament, standings). |
| `eventIds` | array | no |  | SofaScore match IDs or match page URLs (mode=event). |
| `seasonId` | integer | no |  | Optional season ID for standings or tournament mode. If omitted, the latest season with a table is used. |
| `tableType` | string | no | total | Standings table to fetch (modes standings, tournament). |

14 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "searchQueries": [
    "Real Madrid"
  ],
  "includeStatistics": false,
  "includeLineups": false,
  "includeIncidents": false,
  "maxItems": 25,
  "mode": "search"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `name` | Name |
| `eventId` | Event Id |
| `homeTeam` | Home Team |
| `awayTeam` | Away Team |
| `homeScore` | Home Score |
| `awayScore` | Away Score |
| `status` | Status |
| `startTime` | Start Time |
| `sport` | Sport |
| `tournamentName` | Tournament Name |
| `teamId` | Team Id |
| `playerId` | Player Id |
| `points` | Points |
| `rankingTypeName` | Ranking Type Name |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/sofascore-live-scores-standings-and-team-search-data.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
