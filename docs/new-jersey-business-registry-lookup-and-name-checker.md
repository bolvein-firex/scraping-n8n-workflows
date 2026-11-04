# New Jersey Business Registry Lookup & Name Checker: free n8n workflow

A free n8n workflow that runs the [New Jersey Business Registry Lookup & Name Checker](https://apify.com/vexaloom-labs/new-jersey-business-registry-lookup-and-name) Apify Actor and returns `businessName`, `entityTypeAbbr`, `entityTypeFull`, `city`, `incorporatedDate` and more as clean, deduped rows for Google Sheets or your next node.

- Job: New Jersey business entity search
- Platform: NJ business registry
- Workflow file: [workflows/new-jersey-business-registry-lookup-and-name-checker.json](../workflows/new-jersey-business-registry-lookup-and-name-checker.json) (raw: `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/new-jersey-business-registry-lookup-and-name-checker.json`)
- Actor: https://apify.com/vexaloom-labs/new-jersey-business-registry-lookup-and-name
- Agent skill for the same Actor: https://github.com/bolvein-firex/scraping-skills/blob/main/skills/new-jersey-business-registry-lookup-and-name-checker/SKILL.md

## Watch the Short

- [Stop checking business filings one name at a time](https://www.youtube.com/shorts/tGV77V4rMqk)

## What it does

Look up New Jersey registered businesses by name, keyword or entity ID, and check whether a candidate business name is available for a new filing. Returns entity ID, entity type, city and incorporation date.

## Inputs

| Field | Type | Required | Default | Notes |
|---|---|---|---|---|
| `mode` | string | yes | byName | What to fetch. |
| `businessNames` | array | no | ["Amazon"] | One or more names (mode=byName, availability). Name search is a prefix match: 'Amazon' finds names starting with Amazon, and a leading 'The' is ignored. |
| `keywordSearches` | array | no | [] | One or more keyword phrases (mode=byKeyword). Each phrase is split into words, and every word must appear in the business name; up to 5 words per phrase and 20 phrases. |
| `entityIds` | array | no | [] | Exact 10-digit New Jersey entity IDs (mode=byEntityId, documents). Invalid IDs are reported in the run status instead of being dropped silently. Up to 200 IDs. |
| `linkType` | string | no | principal | Which free Business Records Service search to use (mode=byLinkedName). |
| `linkedName` | string | no |  | Last name, business name, registered-agent name, or previous/alternate name to search (mode=byLinkedName). |
| `linkedFirstName` | string | no |  | Optional first name when linkType=principal (mode=byLinkedName). |
| `linkedMiddleName` | string | no |  | Optional middle name when linkType=principal (mode=byLinkedName). |
| `linkedCity` | string | no |  | Optional city filter for principal or registered-agent searches (mode=byLinkedName). |
| `entityTypes` | array | no | [] | Keep only these New Jersey entity types. Empty means no filter. Filters run on every page, not only after the 500-row display cap. |
| `cityFilter` | string | no |  | Keep only businesses whose on-file city matches exactly (case-insensitive). Leave blank for all cities. |
| `maxItems` | integer | no | 100 | Hard cap on emitted records (1-500, the source's display limit). Applied exactly, including when it is above 200. |

Starter input (edit it in **Configure input**):

```json
{
  "mode": "byKeyword",
  "keywordSearches": [
    "roofing"
  ],
  "maxItems": 25
}
```

The input passes the Actor's input schema (checked at every publish). First run: `maxItems` = 25, small enough for the 300-second sync wait; raise it once the rows look right.

## Output fields

Columns from the Actor's dataset schema, build 1.1.1:

| Field | Label |
|---|---|
| `businessName` | Business Name |
| `entityId` | Entity Id |
| `entityTypeAbbr` | Entity Type Abbr |
| `entityTypeFull` | Entity Type Full |
| `city` | City |
| `incorporatedDate` | Incorporated Date |
| `incorporatedMonth` | Incorporated Month |
| `isAvailable` | Is Available |
| `documentCount` | Document Count |

The full dataset has 1 more field; open the Actor's Output tab for all of them.

## Nodes

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

**Normalize + dedupe** keeps one row per `entityId` (per record type when the Actor mixes them).

## Import

1. In n8n: **⋯ → Import from URL** and paste `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/new-jersey-business-registry-lookup-and-name-checker.json`.
2. Create a **Query Auth** credential (name `token`, value your Apify API token) and select it in **Run Apify Actor**.
3. Edit **Configure input**, then **Execute workflow**.

Public data only. Respect the target site's terms and local law.
