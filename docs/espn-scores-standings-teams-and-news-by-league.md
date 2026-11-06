# ESPN Scores, Standings, Teams & News by League: free n8n workflow

A free n8n workflow that runs the [ESPN Scores, Standings, Teams & News by League](https://apify.com/vexaloom-labs/espn-scores-standings-teams-and-news-by-league) Apify Actor and returns `mode`, `sport`, `league`, `homeScore`, `awayScore` and more as clean, deduped rows for Google Sheets or your next node.

- Job: ESPN scores, standings, teams
- Platform: ESPN
- Workflow file: [workflows/espn-scores-standings-teams-and-news-by-league.json](../workflows/espn-scores-standings-teams-and-news-by-league.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/espn-scores-standings-teams-and-news-by-league.json`)
- Actor: https://apify.com/vexaloom-labs/espn-scores-standings-teams-and-news-by-league
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/espn-scores-standings-teams-and-news-by-league/SKILL.md

## What it does

Pull live and recent scores, league standings, team rosters, news headlines, and full game boxscores for NFL, NBA, MLB, NHL, MLS, Premier League, La Liga, F1, UFC, PGA Golf, ATP Tennis, and more.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | news | What to fetch from ESPN. |
| `league` | string | no | nba | League slug. The sport is derived automatically. |
| `leagues` | array | no |  | Optional multi-league override for modes that iterate leagues (scoreboard, odds, standings, teams, teamDetail, news, players, schedule, rankings), e.g. ["nba","nfl"]. |
| `datePreset` | string | no | today | Date window for scoreboard and odds. ESPN accepts one date per request, so ranges are fetched one day at a time. |
| `startDate` | string | no |  | First date for datePreset=custom, in YYYYMMDD or YYYY-MM-DD. |
| `endDate` | string | no |  | Last date for datePreset=custom (inclusive), in YYYYMMDD or YYYY-MM-DD. Maximum 366 days. |
| `season` | integer | no |  | ESPN season year for standings, schedule, players and rankings (e.g. 2025). Leave blank for the current season. |
| `seasonType` | string | no |  | Filter a team schedule by season phase (ignored for soccer schedules, which ESPN reports as one league season). |
| `teamIds` | array | no |  | Teams for teams/teamDetail/schedule/players. Accepts 2, BOS or nba/BOS. Get IDs from mode=teams. |
| `eventIds` | array | no |  | Games for gameDetail/odds. Accepts 401909904 or nba/401909904. Get IDs from mode=scoreboard. |
| `athleteQueries` | array | no |  | Player names to search, e.g. ["LeBron James", "Jannik Sinner"]. |
| `athleteIds` | array | no |  | ESPN athlete IDs for direct profiles, e.g. ["1966"]. |

10 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "includeTeamDetails": false,
  "maxItems": 25,
  "mode": "news"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `mode` | Mode |
| `sport` | Sport |
| `league` | League |
| `name` | Name |
| `status` | Status |
| `homeTeam` | Home Team |
| `awayTeam` | Away Team |
| `homeScore` | Home Score |
| `awayScore` | Away Score |
| `date` | Date |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/espn-scores-standings-teams-and-news-by-league.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
