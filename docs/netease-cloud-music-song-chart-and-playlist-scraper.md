# NetEase Cloud Music Song, Chart & Playlist Scraper: free n8n workflow

A free n8n workflow that runs the [NetEase Cloud Music Song, Chart & Playlist Scraper](https://apify.com/dataspryva/netease-cloud-music-song-chart-and-playlist) Apify Actor and returns `name`, `artist`, `album`, `rankPosition`, `playlistName` and more as clean, deduped rows for Google Sheets or your next node.

- Job: NetEase Cloud Music song, chart scraper
- Platform: NetEase Cloud Music
- Workflow file: [workflows/netease-cloud-music-song-chart-and-playlist-scraper.json](../workflows/netease-cloud-music-song-chart-and-playlist-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/netease-cloud-music-song-chart-and-playlist-scraper.json`)
- Actor: https://apify.com/dataspryva/netease-cloud-music-song-chart-and-playlist
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/netease-cloud-music-song-chart-and-playlist-scraper/SKILL.md

## What it does

Search NetEase Cloud Music songs, fetch song details by URL, pull an artist's top songs or album list, browse playlists by genre, or get any top-100 chart. Returns artist, album, duration, cover art, and popularity for each track.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | search | What to fetch. Each mode reads its own list field. |
| `searchQueries` | array | no | ["周杰伦"] | Free-text queries (mode=search). One or more artist, song, album or playlist names. |
| `searchType` | string | no | song | Which catalog entity to search for (mode=search). |
| `songUrls` | array | no | [] | music.163.com song URLs or bare song IDs, e.g. 186016. |
| `artistIds` | array | no | [] | Artist IDs, music.163.com artist URLs, or exact artist names. |
| `artistOrder` | string | no | hot | Order the artist's song catalogue by popularity or release time (mode=byArtist). |
| `albumUrls` | array | no | [] | music.163.com album URLs or bare album IDs. |
| `playlistUrls` | array | no | [] | music.163.com playlist URLs or bare playlist IDs. Full tracklists are read. |
| `playlistCat` | string | no | 华语 | NetEase playlist genre, scene or mood to browse (mode=byPlaylist). |
| `toplistIds` | array | no | [] | Chart IDs, music.163.com toplist URLs, or Chinese/English chart names. Use `all` or leave empty for every current chart. |
| `maxTracksPerChart` | integer | no | 0 | Limit tracks read from each chart before the global max items cap (mode=byToplist). 0 reads every track. |
| `commentUrls` | array | no | [] | Song, album, playlist or chart URLs/IDs. A bare ID is treated as a song; use `album:123`, `playlist:123` or `chart:123` to be explicit. |

16 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "maxItems": 25,
  "mode": "search",
  "maxCommentsPerItem": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `name` | Name |
| `artist` | Artist |
| `album` | Album |
| `rankPosition` | Rank Position |
| `chartName` | Chart Name |
| `playlistName` | Playlist Name |
| `durationSec` | Duration Sec |

The full dataset has 2 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/netease-cloud-music-song-chart-and-playlist-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
