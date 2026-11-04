# Google Maps Business Lead & Email Finder: free n8n workflow

A free n8n workflow that runs the [Google Maps Business Lead & Email Finder](https://apify.com/dataspryva/google-maps-business-lead-and-email-finder) Apify Actor and returns `name`, `googleBusinessCategories`, `phoneNumber`, `email`, `reviewScore` and more as clean, deduped rows for Google Sheets or your next node.

- Job: Google Maps leads with emails
- Platform: Google Maps
- Workflow file: [workflows/google-maps-business-lead-and-email-finder.json](../workflows/google-maps-business-lead-and-email-finder.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-maps-business-lead-and-email-finder.json`)
- Actor: https://apify.com/dataspryva/google-maps-business-lead-and-email-finder
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/google-maps-business-lead-and-email-finder/SKILL.md

## Watch the Short

- [Watch the Short](https://www.youtube.com/shorts/ofD2844kDPQ)

## What it does

Find business leads on Google Maps by category, keyword, or location and collect name, address, phone, website, rating, review count, and coordinates. Optionally adds emails and social links found on each business's own website.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | no | searchPlaces | Search Google Maps, look up specific places, or enrich a list of websites you already have. |
| `searchQueries` | array | no |  | Natural-language searches such as 'coffee shops in Austin TX'. Include the place in each phrase, or use the location field below. |
| `locationQuery` | string | no |  | Adds a shared location to every search phrase, for example 'Austin, TX, USA'. Leave empty when your phrases already name the place. |
| `category` | string | no | bakery | Business category such as bakery, dentist or plumber. Used when keyword and search phrases are empty. |
| `keyword` | string | no |  | Custom search term such as 'boutique coffee' or 'pet grooming'. Takes priority over category. |
| `state` | string | no | All | US state for the search. Choose 'All' for nationwide. Ignored for non-US countries. |
| `country` | string | no | US | Country for the search. Other countries can be named directly in a search phrase. |
| `websites` | array | no |  | Websites to read for contact details, one per line. Bare domains such as example.com are accepted. |
| `placeUrls` | array | no |  | Google Maps place links copied from the address bar or a previous export. |
| `placeIds` | array | no |  | Canonical Google Place IDs starting with 'ChIJ'. |
| `max_results` | integer | no | 100 | Maximum number of leads to save. Google returns a ranked window of roughly 150-220 businesses per search phrase, so a larger request may end when that window ends. |
| `minRating` | number | no |  | Keep only businesses rated at least this value (1.0-5.0). Leave empty for any rating. |

8 more optional fields on the Actor's Input tab.

Starter input (edit it in **Configure input**):

```json
{
  "mode": "searchPlaces",
  "searchQueries": [
    "restaurants in New York, NY"
  ],
  "max_results": 20,
  "extractEmails": true,
  "onlySaveResults": "onlyWithContacts"
}
```

The input passes the Actor's input schema (checked at every publish). First run: `max_results` = 20, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.0.2:

| Field | Label |
|---|---|
| `name` | Business |
| `googleBusinessCategories` | Categories |
| `street` | Street |
| `city` | City |
| `state` | State / region |
| `zip` | Postal code |
| `country` | Country |
| `countryCode` | Country code |
| `phoneNumber` | Phone |
| `url` | Website |
| `email` | Email |
| `emails` | Emails |
| `reviewScore` | Rating |
| `reviewsNumber` | Reviews |
| `placeId` | Place ID |
| `featureId` | Feature ID |
| `googleMapsUrl` | Google Maps |
| `priceLevel` | Price level |
| `plusCode` | Plus Code |
| `location` | Coordinates |
| `facebook` | Facebook |
| `instagram` | Instagram |
| `linkedin` | LinkedIn |
| `twitter` | X / Twitter |
| `youtube` | YouTube |
| `tiktok` | TikTok |
| `websitePhones` | Website phones |
| `contactPageUrl` | Contact page |
| `websitePagesCrawled` | Website pages crawled |
| `emailsMxValid` | MX-valid emails |
| `emailProvenance` | Email sources |
| `pinterest` | Pinterest |
| `threads` | Threads |
| `whatsapp` | WhatsApp |
| `telegram` | Telegram |
| `websiteType` | Website type |

The full dataset has 3 more fields; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `placeId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/google-maps-business-lead-and-email-finder.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
