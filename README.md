# Scraping n8n Workflows

Runnable n8n workflows for the **Scraper Finder** channel. Each workflow calls a public Apify actor, normalizes the rows, dedupes, and hands you a clean export.

**Watch the 45-second breakdown:** https://www.youtube.com/@ScraperFinder

New public-data workflow every day. Free. No email. No course.

- Skills repo: https://github.com/bolvein-firex/scraping-skills
- Channel: https://www.youtube.com/@ScraperFinder

## Start here

1. Watch the short on the channel: https://www.youtube.com/@ScraperFinder
2. Pick the workflow for the job you need below.
3. Import the JSON into n8n.
4. Run it on your own Apify account.

## Workflows

| # | Workflow | Platform | Object | Output |
|---|---|---|---|---|
| 1 | [Amazon Customer Review & Rating Summary Scraper](workflows/amazon-customer-review-and-rating-summary-scraper.json) | Amazon | review data | author, rating, text, verified |
| 2 | [Amazon Review Aggregates & Extended History Scraper](workflows/amazon-review-aggregates-and-extended-history-scraper.json) | Amazon | review data | author, business, rating, text |
| 3 | [Booking.com Hotel Price & Amenity Search Scraper](workflows/booking-com-hotel-price-and-amenity-search-scraper.json) | Booking.com | products | title, price, rating, reviews |
| 4 | [Facebook Marketplace Listing & Price Extractor](workflows/facebook-marketplace-listing-and-price-extractor.json) | Facebook | products | symbol, change, market cap, price |
| 5 | [Google Maps Grid-Based Market Saturation Scanner](workflows/google-maps-grid-based-market-saturation-scanner.json) | Google Maps | competitors | business, rating, reviews, Grid Point |
| 6 | [Google Shopping Price Comparison & Deal Finder](workflows/google-shopping-price-comparison-and-deal-finder.json) | Google Shopping | products | title, price, rating, reviews |
| 7 | [New Jersey Business Registry Lookup & Name Checker](workflows/new-jersey-business-registry-lookup-and-name-checker.json) | the state registry | business entities | entity name, agent, status, formed date |
| 8 | [Shopify Store Catalog & Pricing Extractor](workflows/shopify-store-catalog-and-pricing-extractor.json) | Shopify | stores | title, price, stock, compare-at |
| 9 | [TikTok Hashtag Momentum & Top Creator Tracker](workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json) | TikTok | trends | hashtag, views, momentum, top creator |
| 10 | [US Walkability, Transit & Bike Score Extractor](workflows/us-walkability-transit-and-bike-score-extractor.json) | the public web | location scores | walk score, transit score, bike score, address |
| 11 | [Google Maps Business Lead & Email Finder](workflows/google-maps-business-lead-and-email-finder.json) | Google Maps | restaurants | name, email, rating, phone |
| 12 | [Zillow For-Sale, Rent & Sold Listing Extractor](workflows/zillow-for-sale-rent-and-sold-listing-extractor.json) | Zillow | listings | address, price, beds, price cut |
| 13 | [Amazon Multi-Domain Product Price & Detail Scraper](workflows/amazon-multi-domain-product-price-and-detail-scraper.json) | Amazon | products | title, price, rating, reviews |
| 14 | [Website Contact Page Email & Phone Crawler](workflows/website-contact-page-email-and-phone-crawler.json) | the web | contact pages | domain, email, phone, status |
| 15 | [Indeed Global Job Scraper with Company Salary Reports](workflows/indeed-global-job-scraper-with-company-salary-reports.json) | Indeed | jobs | title, salary, company, location |
| 16 | [Airbnb Listing Price & Location Finder](workflows/airbnb-listing-price-and-location-finder.json) | Airbnb | listings | name, price, rating, reviews |
| 17 | [Google Trends Interest & Related Query Scraper](workflows/google-trends-interest-and-related-query-scraper.json) | Google Trends | search trends | Term, Interest, Breakout, Related Query |
| 18 | [Reddit Multi-Mode Scraper for Posts, Comments & Profiles](workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json) | Reddit | conversations | score, author, title, Subreddit |

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
