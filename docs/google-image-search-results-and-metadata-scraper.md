# Google Image Search Results & Metadata Scraper: free n8n workflow

A free n8n workflow that runs the [Google Image Search Results & Metadata Scraper](https://apify.com/nimbryxo-studio/google-image-search-results-and-metadata-scraper) Apify Actor and returns `engine`, `title`, `sourceDomain`, `imageUrl`, `imageWidth` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google image Search results scraper
- Platform: Google Search
- Workflow file: [workflows/google-image-search-results-and-metadata-scraper.json](../workflows/google-image-search-results-and-metadata-scraper.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-image-search-results-and-metadata-scraper.json`)
- Actor: https://apify.com/nimbryxo-studio/google-image-search-results-and-metadata-scraper
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-image-search-results-and-metadata-scraper/SKILL.md

## What it does

Run a Google Images search and get back full-resolution image URLs with dimensions, thumbnails, source page titles, and the web page each image came from.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `queries` | array | no |  | One or more image search queries. Each query is searched independently. Google operators such as site:, quoted phrases and -exclusions are passed through. |
| `maxResults` | integer | no | 100 | Maximum number of image rows to return for each query. Google Images usually runs out around 300-400 results for a query; this is a ceiling, not a guarantee. |
| `minWidth` | integer | no | 0 | Drop images narrower than this many pixels. Rows without published dimensions are dropped when this is set. 0 disables the filter. |
| `minHeight` | integer | no | 0 | Drop images shorter than this many pixels. Rows without published dimensions are dropped when this is set. 0 disables the filter. |
| `country` | string | no | US | Two-letter country used for Google's gl parameter (and Bing's cc parameter). Local sites rank higher in local results. |
| `language` | string | no | en | Interface and result language used for Google's hl parameter (and Bing's setlang parameter). |
| `safeSearch` | string | no | active | Google SafeSearch level. 'active' filters explicit images; 'off' does not. |
| `imageSize` | string | no |  | Google Images size filter. The MP values are minimum megapixels. Bing fallback applies the nearest size category and enforces the exact MP floor locally when dimensions are known. |
| `imageColor` | string | no |  | Google Images color filter. 'black_and_white' is grayscale; 'transparent' looks for a transparent background. |
| `imageType` | string | no |  | Google Images type filter: photographs, faces, clip art, line drawings or animated images. |
| `fileType` | string | no |  | Only images in this format. Google applies this server-side; Bing fallback applies it to the image URL extension locally. |
| `timeRange` | string | no |  | Only images Google found within this period. Bing fallback maps 'hour' to its 24-hour window. |

3 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "queries": [
    "Alfons Mucha"
  ],
  "maxResults": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxResults` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 2.1.1:

| Field | Label |
|---|---|
| `engine` | Engine |
| `imageUrlType` | URL type |
| `title` | Title |
| `sourceDomain` | Source domain |
| `imageUrl` | Image URL |
| `imageWidth` | Width |
| `imageHeight` | Height |

The full dataset has 22 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** drops identical rows (this output has no stable row ID).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-image-search-results-and-metadata-scraper.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
