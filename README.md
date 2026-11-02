# Scraping n8n Workflows

Runnable n8n workflows for the **Scraper Finder** channel. Each workflow calls a public Apify actor, normalizes the rows, dedupes, and hands you a clean export.

- Actor catalog: https://bolvein-firex.github.io/scraper-finder-site/
- Skills repo: https://github.com/bolvein-firex/scraping-skills
- Channel: @scraperfinder

## Workflows

| # | Workflow | Platform | Object | Output |
|---|---|---|---|---|
| 1 | [Google Maps Business Lead & Email Finder](workflows/google-maps-business-lead-and-email-finder.json) | Google Maps | records | name, phone, website, rating |
| 2 | [Zillow For-Sale, Rent & Sold Listing Extractor](workflows/zillow-for-sale-rent-and-sold-listing-extractor.json) | Zillow | listings | address, price, beds, baths |
| 3 | [TikTok Hashtag Momentum & Top Creator Tracker](workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json) | TikTok | trends | hashtag, posts, views, momentum |
| 4 | [Amazon Multi-Domain Product Price & Detail Scraper](workflows/amazon-multi-domain-product-price-and-detail-scraper.json) | Amazon | products | title, price, coupon, rating |
| 5 | [Google Maps Grid-Based Market Saturation Scanner](workflows/google-maps-grid-based-market-saturation-scanner.json) | Google Maps | competitors | Grid Point, rank, business, rating |
| 6 | [Website Contact Page Email & Phone Crawler](workflows/website-contact-page-email-and-phone-crawler.json) | the web | records | domain, email, phone, source page |
| 7 | [Shopify Store Catalog & Pricing Extractor](workflows/shopify-store-catalog-and-pricing-extractor.json) | Shopify | records | title, price, compare-at, variant |
| 8 | [Indeed Global Job Scraper with Company Salary Reports](workflows/indeed-global-job-scraper-with-company-salary-reports.json) | Indeed | jobs | title, company, location, salary |
| 9 | [Airbnb Listing Price & Location Finder](workflows/airbnb-listing-price-and-location-finder.json) | Airbnb | listings | name, price, rating, reviews |
| 10 | [Google Trends Interest & Related Query Scraper](workflows/google-trends-interest-and-related-query-scraper.json) | Google Trends | records | Term, Interest, Breakout, Related Query |
| 11 | [Reddit Multi-Mode Scraper for Posts, Comments & Profiles](workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json) | Reddit | records | Subreddit, title, score, author |
| 12 | [New Jersey Business Registry Lookup & Name Checker](workflows/new-jersey-business-registry-lookup-and-name-checker.json) | the state registry | records | entity name, status, formed date, agent |

## Setup

1. Create an Apify account and copy an API token from https://console.apify.com/account#/integrations.
2. In n8n, create a **Query Auth** credential:
   - Name: `Apify API Token`
   - Query parameter name: `token`
   - Value: your token
3. Import a workflow JSON file.
4. Open **Run Scraper Finder actor** and select the credential.
5. Edit **Configure input** for your city, keyword, or category.
6. Click **Execute workflow**.
7. Optional: enable **Google Sheets** and set your sheet.

## Why these workflows

- No org token. You run the actor on your own Apify account.
- No custom scraper to maintain.
- Rows are normalized and deduped before they reach your sheet.
- Each workflow is tied to a short video and a public actor page.

## Structure

```
workflows/
  <actor-slug>.json
docs/
  setup-apify.md
  import.md
```

## Guardrails

Public data only. Do not use these workflows for private, login-protected, or paywalled data. Respect robots.txt, site terms, and local law.

## License

MIT
