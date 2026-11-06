# Scraping n8n Workflows

A collection of free, runnable n8n workflows that pull public web data from Google Maps, Amazon, Shopify, Zillow, Airbnb, Indeed, TikTok, Reddit and 22 more sources through Apify Actors, then clean, dedupe and send the rows to Google Sheets or the next node.

**36 workflows** · 23 with a YouTube Short · last updated 2026-11-06 · MIT licence

## Quick start

1. Pick a workflow below and copy its raw JSON link, for example `https://raw.githubusercontent.com/bolvein-firex/scraping-n8n-workflows/main/workflows/aliexpress-multi-region-search-store-and-review-scraper.json`.
2. In n8n, open a new workflow, then **⋯ → Import from URL** (or **Import from file** with the downloaded JSON).
3. Create a **Query Auth** credential: name `token`, value your Apify API token ([where to find it](https://console.apify.com/settings/integrations)). Select it in the **Run Apify Actor** node.
4. Edit **Configure input** (city, keyword, URLs, limit) and click **Execute workflow**. The rows appear in **Rows ready**.
5. Optional: enable **Google Sheets (optional)**, pick your sheet, and keep the daily trigger on for a scheduled refresh.

## Find a workflow by job

### Lead generation

| Job | Workflow | Returns |
|---|---|---|
| Google Maps leads with emails | [Google Maps Business Lead & Email Finder](docs/google-maps-business-lead-and-email-finder.md) | `name`, `googleBusinessCategories`, `phoneNumber`, `email`, `reviewScore` |
| Google Maps search beyond 120 results | [Google Maps Grid-Based Market Saturation Scanner](docs/google-maps-grid-based-market-saturation-scanner.md) | `name`, `categoryName`, `totalScore`, `reviewsCount`, `phone` |
| New Jersey business entity search | [New Jersey Business Registry Lookup & Name Checker](docs/new-jersey-business-registry-lookup-and-name-checker.md) | `businessName`, `entityTypeAbbr`, `entityTypeFull`, `city`, `incorporatedDate` |
| Find emails and phone numbers from a list of websites | [Website Contact Page Email & Phone Crawler](docs/website-contact-page-email-and-phone-crawler.md) | `websiteUrl`, `status`, `emails`, `primaryEmail`, `phones` |

### E-commerce and price tracking

| Job | Workflow | Returns |
|---|---|---|
| AliExpress product search export | [AliExpress Multi-Region Search, Store & Review Scraper](docs/aliexpress-multi-region-search-store-and-review-scraper.md) | `title`, `salePrice`, `originalPrice`, `discountPercent`, `rating` |
| Amazon deals grid | [Amazon Deals Grid Tracker by Category & Discount](docs/amazon-deals-grid-tracker-by-category-and-discount.md) | `asin`, `title`, `dealPrice`, `savingsPercent`, `averageRating` |
| Amazon price tracking | [Amazon Multi-Domain Product Price & Detail Scraper](docs/amazon-multi-domain-product-price-and-detail-scraper.md) | `title`, `asin`, `price`, `stars`, `reviewsCount` |
| Facebook Marketplace scraper | [Facebook Marketplace Listing & Price Extractor](docs/facebook-marketplace-listing-and-price-extractor.md) | `title`, `price`, `city`, `state`, `locationText` |
| Google Shopping price comparison | [Google Shopping Price Comparison & Deal Finder](docs/google-shopping-price-comparison-and-deal-finder.md) | `title`, `price`, `merchant`, `rating`, `reviewCount` |
| Scrape a Shopify store's products and prices | [Shopify Store Catalog & Pricing Extractor](docs/shopify-store-catalog-and-pricing-extractor.md) | `title`, `price`, `compareAtPrice`, `available`, `vendor` |

### Real estate

| Job | Workflow | Returns |
|---|---|---|
| Walk Score for a list of addresses | [US Walkability, Transit & Bike Score Extractor](docs/us-walkability-transit-and-bike-score-extractor.md) | `address`, `city`, `walkScore`, `transitScore`, `bikeScore` |
| Zillow for-sale, rental and sold listings | [Zillow For-Sale, Rent & Sold Listing Extractor](docs/zillow-for-sale-rent-and-sold-listing-extractor.md) | `address`, `price`, `soldPrice`, `beds`, `baths` |

### Travel and short-term rentals

| Job | Workflow | Returns |
|---|---|---|
| Airbnb price scraper | [Airbnb Listing Price & Location Finder](docs/airbnb-listing-price-and-location-finder.md) | `name`, `nightlyPrice`, `totalPrice`, `rating`, `reviewCount` |
| Booking.com hotel prices for your dates | [Booking.com Hotel Price & Amenity Search Scraper](docs/booking-com-hotel-price-and-amenity-search-scraper.md) | `name`, `price`, `pricePerNight`, `rating`, `reviewCount` |
| Google Flights fare scraper | [Google Flights Fare & Itinerary Filter Scraper](docs/google-flights-fare-and-itinerary-filter-scraper.md) | `price`, `airline`, `departureAirport`, `departureTime`, `arrivalAirport` |

### Jobs and salaries

| Job | Workflow | Returns |
|---|---|---|
| Fiverr gig scraper | [Fiverr Gig & Seller Sitemap Directory Scraper](docs/fiverr-gig-and-seller-sitemap-directory-scraper.md) | `title`, `gigUrl`, `priceMin`, `priceMax`, `rating` |
| Greenhouse ATS job board | [Greenhouse ATS Job Board Lookup by Company](docs/greenhouse-ats-job-board-lookup-by-company.md) | `title`, `companySlug`, `companyName`, `location`, `departments` |
| Himalayas remote job | [Himalayas Remote Job Finder with Salary & Tech Stack](docs/himalayas-remote-job-finder-with-salary-and-tech-stack.md) | `title`, `company`, `salaryMin`, `salaryMax`, `salaryPeriod` |
| Indeed job scraper with salaries | [Indeed Global Job Scraper with Company Salary Reports](docs/indeed-global-job-scraper-with-company-salary-reports.md) | `positionName`, `displayTitle`, `company`, `rating`, `salary` |
| Lever job board postings | [Lever Job Board Postings by Company Slug](docs/lever-job-board-postings-by-company-slug.md) | `title`, `companySlug`, `location`, `salaryText`, `createdAt` |
| startup.jobs category scraper | [startup.jobs Category & Keyword Job Scraper](docs/startup-jobs-category-and-keyword-job-scraper.md) | `title`, `company`, `location`, `salary`, `postedAt` |
| We Work Remotely job listings scraper | [We Work Remotely Job Listings & Salary Extractor](docs/we-work-remotely-job-listings-and-salary-extractor.md) | `title`, `company`, `category`, `salary`, `postedAt` |
| Workday careers site job listings scraper | [Workday Careers Site Job Listings Extractor](docs/workday-careers-site-job-listings-extractor.md) | `title`, `tenant`, `location`, `postedOn` |

### Social media and trends

| Job | Workflow | Returns |
|---|---|---|
| Dailymotion video discovery | [Dailymotion Video Discovery by Topic & Channel](docs/dailymotion-video-discovery-by-topic-and-channel.md) | `title`, `ownerUsername`, `views`, `likes`, `duration` |
| Export Google Trends data | [Google Trends Interest & Related Query Scraper](docs/google-trends-interest-and-related-query-scraper.md) | `searchTerms`, `title`, `geoName`, `averageInterest`, `growthPercent` |
| NetEase Cloud Music song, chart scraper | [NetEase Cloud Music Song, Chart & Playlist Scraper](docs/netease-cloud-music-song-chart-and-playlist-scraper.md) | `name`, `artist`, `album`, `rankPosition`, `playlistName` |
| Reddit posts and comments scraper | [Reddit Multi-Mode Scraper for Posts, Comments & Profiles](docs/reddit-multi-mode-scraper-for-posts-comments-and-profiles.md) | `subreddit_prefixed`, `title`, `author`, `score`, `commentCount` |
| TikTok trending hashtags | [TikTok Hashtag Momentum & Top Creator Tracker](docs/tiktok-hashtag-momentum-and-top-creator-tracker.md) | `rankIndex`, `hashtagName`, `publishCnt`, `vv` |
| TikTok keyword search scraper | [TikTok Keyword Search & Discovery Scraper](docs/tiktok-keyword-search-and-discovery-scraper.md) | `rank`, `caption`, `playCount`, `likeCount`, `commentCount` |
| TikTok verified mention | [TikTok Verified Mention Tracker](docs/tiktok-verified-mention-tracker.md) | `targetUsername`, `postUrl`, `author.followerCount`, `playCount`, `likeCount` |
| YouTube video comment scraper | [YouTube Video Comment & Reply Thread Scraper](docs/youtube-video-comment-and-reply-thread-scraper.md) | `authorName`, `text`, `likeCount`, `replyCount`, `isHearted` |

### Reviews

| Job | Workflow | Returns |
|---|---|---|
| Amazon review scraper | [Amazon Customer Review & Rating Summary Scraper](docs/amazon-customer-review-and-rating-summary-scraper.md) | `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` |
| Amazon reviews across marketplaces | [Amazon Review Aggregates & Extended History Scraper](docs/amazon-review-aggregates-and-extended-history-scraper.md) | `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` |

### Other public data

| Job | Workflow | Returns |
|---|---|---|
| MLB teams, player search | [MLB Teams, Player Search & Season Schedule Lookup](docs/mlb-teams-player-search-and-season-schedule-lookup.md) | `teamName`, `playerName`, `eventName`, `homeTeam`, `awayTeam` |
| Multi-League season results | [Multi-League Season Results & Team Lookup](docs/multi-league-season-results-and-team-lookup.md) | `homeTeam`, `awayTeam`, `homeScore`, `awayScore`, `matchDate` |
| SofaScore live scores, standings | [SofaScore Live Scores, Standings & Team Search Data](docs/sofascore-live-scores-standings-and-team-search-data.md) | `name`, `homeTeam`, `awayTeam`, `homeScore`, `awayScore` |

## All workflows

Output fields are the Actor's own column names, read from its dataset schema at publish time.

| # | Workflow | Platform | Output fields | File | Short |
|---|---|---|---|---|---|
| 1 | [Airbnb Listing Price & Location Finder](docs/airbnb-listing-price-and-location-finder.md) | Airbnb | `name`, `nightlyPrice`, `totalPrice`, `rating`, `reviewCount` | [JSON](workflows/airbnb-listing-price-and-location-finder.json) | [Watch](https://www.youtube.com/shorts/aVEDRMB3vsU) |
| 2 | [AliExpress Multi-Region Search, Store & Review Scraper](docs/aliexpress-multi-region-search-store-and-review-scraper.md) | AliExpress | `title`, `salePrice`, `originalPrice`, `discountPercent`, `rating` | [JSON](workflows/aliexpress-multi-region-search-store-and-review-scraper.json) | [Watch](https://www.youtube.com/shorts/lY2MQAk6oJA) |
| 3 | [Amazon Customer Review & Rating Summary Scraper](docs/amazon-customer-review-and-rating-summary-scraper.md) | Amazon | `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` | [JSON](workflows/amazon-customer-review-and-rating-summary-scraper.json) | [Watch](https://www.youtube.com/shorts/WhVOks5q4MU) |
| 4 | [Amazon Deals Grid Tracker by Category & Discount](docs/amazon-deals-grid-tracker-by-category-and-discount.md) | Amazon | `asin`, `title`, `dealPrice`, `savingsPercent`, `averageRating` | [JSON](workflows/amazon-deals-grid-tracker-by-category-and-discount.json) |  |
| 5 | [Amazon Multi-Domain Product Price & Detail Scraper](docs/amazon-multi-domain-product-price-and-detail-scraper.md) | Amazon | `title`, `asin`, `price`, `stars`, `reviewsCount` | [JSON](workflows/amazon-multi-domain-product-price-and-detail-scraper.json) | [Watch](https://www.youtube.com/shorts/SqsDoB0jyD8) |
| 6 | [Amazon Review Aggregates & Extended History Scraper](docs/amazon-review-aggregates-and-extended-history-scraper.md) | Amazon | `productAsin`, `ratingScore`, `reviewTitle`, `reviewDescription`, `isVerified` | [JSON](workflows/amazon-review-aggregates-and-extended-history-scraper.json) |  |
| 7 | [Booking.com Hotel Price & Amenity Search Scraper](docs/booking-com-hotel-price-and-amenity-search-scraper.md) | Booking.com | `name`, `price`, `pricePerNight`, `rating`, `reviewCount` | [JSON](workflows/booking-com-hotel-price-and-amenity-search-scraper.json) | [Watch](https://www.youtube.com/shorts/jQWhZPI54SI) |
| 8 | [Dailymotion Video Discovery by Topic & Channel](docs/dailymotion-video-discovery-by-topic-and-channel.md) | Dailymotion | `title`, `ownerUsername`, `views`, `likes`, `duration` | [JSON](workflows/dailymotion-video-discovery-by-topic-and-channel.json) |  |
| 9 | [Facebook Marketplace Listing & Price Extractor](docs/facebook-marketplace-listing-and-price-extractor.md) | Facebook Marketplace | `title`, `price`, `city`, `state`, `locationText` | [JSON](workflows/facebook-marketplace-listing-and-price-extractor.json) |  |
| 10 | [Fiverr Gig & Seller Sitemap Directory Scraper](docs/fiverr-gig-and-seller-sitemap-directory-scraper.md) | Fiverr | `title`, `gigUrl`, `priceMin`, `priceMax`, `rating` | [JSON](workflows/fiverr-gig-and-seller-sitemap-directory-scraper.json) | [Watch](https://www.youtube.com/shorts/JsVKl5TOvJE) |
| 11 | [Google Flights Fare & Itinerary Filter Scraper](docs/google-flights-fare-and-itinerary-filter-scraper.md) | Google Flights | `price`, `airline`, `departureAirport`, `departureTime`, `arrivalAirport` | [JSON](workflows/google-flights-fare-and-itinerary-filter-scraper.json) |  |
| 12 | [Google Maps Business Lead & Email Finder](docs/google-maps-business-lead-and-email-finder.md) | Google Maps | `name`, `googleBusinessCategories`, `phoneNumber`, `email`, `reviewScore` | [JSON](workflows/google-maps-business-lead-and-email-finder.json) | [Watch](https://www.youtube.com/shorts/ofD2844kDPQ) |
| 13 | [Google Maps Grid-Based Market Saturation Scanner](docs/google-maps-grid-based-market-saturation-scanner.md) | Google Maps | `name`, `categoryName`, `totalScore`, `reviewsCount`, `phone` | [JSON](workflows/google-maps-grid-based-market-saturation-scanner.json) | [Watch](https://www.youtube.com/shorts/uom3-Fy_xFk) |
| 14 | [Google Shopping Price Comparison & Deal Finder](docs/google-shopping-price-comparison-and-deal-finder.md) | Google Shopping | `title`, `price`, `merchant`, `rating`, `reviewCount` | [JSON](workflows/google-shopping-price-comparison-and-deal-finder.json) |  |
| 15 | [Google Trends Interest & Related Query Scraper](docs/google-trends-interest-and-related-query-scraper.md) | Google Trends | `searchTerms`, `title`, `geoName`, `averageInterest`, `growthPercent` | [JSON](workflows/google-trends-interest-and-related-query-scraper.json) | [Watch](https://www.youtube.com/shorts/gDZBpA25UB8) |
| 16 | [Greenhouse ATS Job Board Lookup by Company](docs/greenhouse-ats-job-board-lookup-by-company.md) | Greenhouse | `title`, `companySlug`, `companyName`, `location`, `departments` | [JSON](workflows/greenhouse-ats-job-board-lookup-by-company.json) |  |
| 17 | [Himalayas Remote Job Finder with Salary & Tech Stack](docs/himalayas-remote-job-finder-with-salary-and-tech-stack.md) | Himalayas | `title`, `company`, `salaryMin`, `salaryMax`, `salaryPeriod` | [JSON](workflows/himalayas-remote-job-finder-with-salary-and-tech-stack.json) | [Watch](https://www.youtube.com/shorts/OwuknGY8obI) |
| 18 | [Indeed Global Job Scraper with Company Salary Reports](docs/indeed-global-job-scraper-with-company-salary-reports.md) | Indeed | `positionName`, `displayTitle`, `company`, `rating`, `salary` | [JSON](workflows/indeed-global-job-scraper-with-company-salary-reports.json) | [Watch](https://www.youtube.com/shorts/33f3pNEO6Oc) |
| 19 | [Lever Job Board Postings by Company Slug](docs/lever-job-board-postings-by-company-slug.md) | Lever | `title`, `companySlug`, `location`, `salaryText`, `createdAt` | [JSON](workflows/lever-job-board-postings-by-company-slug.json) | [Watch](https://www.youtube.com/shorts/Fj8lsPbASu0) |
| 20 | [MLB Teams, Player Search & Season Schedule Lookup](docs/mlb-teams-player-search-and-season-schedule-lookup.md) | MLB | `teamName`, `playerName`, `eventName`, `homeTeam`, `awayTeam` | [JSON](workflows/mlb-teams-player-search-and-season-schedule-lookup.json) |  |
| 21 | [Multi-League Season Results & Team Lookup](docs/multi-league-season-results-and-team-lookup.md) | Multi-League | `homeTeam`, `awayTeam`, `homeScore`, `awayScore`, `matchDate` | [JSON](workflows/multi-league-season-results-and-team-lookup.json) |  |
| 22 | [NetEase Cloud Music Song, Chart & Playlist Scraper](docs/netease-cloud-music-song-chart-and-playlist-scraper.md) | NetEase Cloud Music | `name`, `artist`, `album`, `rankPosition`, `playlistName` | [JSON](workflows/netease-cloud-music-song-chart-and-playlist-scraper.json) | [Watch](https://www.youtube.com/shorts/k3LbS3Z4Eqc) |
| 23 | [New Jersey Business Registry Lookup & Name Checker](docs/new-jersey-business-registry-lookup-and-name-checker.md) | NJ business registry | `businessName`, `entityTypeAbbr`, `entityTypeFull`, `city`, `incorporatedDate` | [JSON](workflows/new-jersey-business-registry-lookup-and-name-checker.json) | [Watch](https://www.youtube.com/shorts/tGV77V4rMqk) |
| 24 | [Reddit Multi-Mode Scraper for Posts, Comments & Profiles](docs/reddit-multi-mode-scraper-for-posts-comments-and-profiles.md) | Reddit | `subreddit_prefixed`, `title`, `author`, `score`, `commentCount` | [JSON](workflows/reddit-multi-mode-scraper-for-posts-comments-and-profiles.json) | [Watch](https://www.youtube.com/shorts/3TmxkUNaB0U) |
| 25 | [Shopify Store Catalog & Pricing Extractor](docs/shopify-store-catalog-and-pricing-extractor.md) | Shopify | `title`, `price`, `compareAtPrice`, `available`, `vendor` | [JSON](workflows/shopify-store-catalog-and-pricing-extractor.json) | [Watch](https://www.youtube.com/shorts/398NV7q-K6w) |
| 26 | [SofaScore Live Scores, Standings & Team Search Data](docs/sofascore-live-scores-standings-and-team-search-data.md) | SofaScore | `name`, `homeTeam`, `awayTeam`, `homeScore`, `awayScore` | [JSON](workflows/sofascore-live-scores-standings-and-team-search-data.json) |  |
| 27 | [startup.jobs Category & Keyword Job Scraper](docs/startup-jobs-category-and-keyword-job-scraper.md) | startup.jobs | `title`, `company`, `location`, `salary`, `postedAt` | [JSON](workflows/startup-jobs-category-and-keyword-job-scraper.json) | [Watch](https://www.youtube.com/shorts/SOMB7J9-Iak) |
| 28 | [TikTok Hashtag Momentum & Top Creator Tracker](docs/tiktok-hashtag-momentum-and-top-creator-tracker.md) | TikTok | `rankIndex`, `hashtagName`, `publishCnt`, `vv` | [JSON](workflows/tiktok-hashtag-momentum-and-top-creator-tracker.json) | [Watch](https://www.youtube.com/shorts/C3buLaYtlGg) |
| 29 | [TikTok Keyword Search & Discovery Scraper](docs/tiktok-keyword-search-and-discovery-scraper.md) | TikTok | `rank`, `caption`, `playCount`, `likeCount`, `commentCount` | [JSON](workflows/tiktok-keyword-search-and-discovery-scraper.json) |  |
| 30 | [TikTok Verified Mention Tracker](docs/tiktok-verified-mention-tracker.md) | TikTok | `targetUsername`, `postUrl`, `author.followerCount`, `playCount`, `likeCount` | [JSON](workflows/tiktok-verified-mention-tracker.json) |  |
| 31 | [US Walkability, Transit & Bike Score Extractor](docs/us-walkability-transit-and-bike-score-extractor.md) | Walk Score | `address`, `city`, `walkScore`, `transitScore`, `bikeScore` | [JSON](workflows/us-walkability-transit-and-bike-score-extractor.json) | [Watch](https://www.youtube.com/shorts/yCT9c3LRopU) |
| 32 | [We Work Remotely Job Listings & Salary Extractor](docs/we-work-remotely-job-listings-and-salary-extractor.md) | We Work Remotely | `title`, `company`, `category`, `salary`, `postedAt` | [JSON](workflows/we-work-remotely-job-listings-and-salary-extractor.json) | [Watch](https://www.youtube.com/shorts/aJWSYR7WvXE) |
| 33 | [Website Contact Page Email & Phone Crawler](docs/website-contact-page-email-and-phone-crawler.md) | Any website | `websiteUrl`, `status`, `emails`, `primaryEmail`, `phones` | [JSON](workflows/website-contact-page-email-and-phone-crawler.json) | [Watch](https://www.youtube.com/shorts/MHdeuiVwMZA) |
| 34 | [Workday Careers Site Job Listings Extractor](docs/workday-careers-site-job-listings-extractor.md) | Workday | `title`, `tenant`, `location`, `postedOn` | [JSON](workflows/workday-careers-site-job-listings-extractor.json) | [Watch](https://www.youtube.com/shorts/cP29fxKOpvM) |
| 35 | [YouTube Video Comment & Reply Thread Scraper](docs/youtube-video-comment-and-reply-thread-scraper.md) | YouTube | `authorName`, `text`, `likeCount`, `replyCount`, `isHearted` | [JSON](workflows/youtube-video-comment-and-reply-thread-scraper.json) |  |
| 36 | [Zillow For-Sale, Rent & Sold Listing Extractor](docs/zillow-for-sale-rent-and-sold-listing-extractor.md) | Zillow | `address`, `price`, `soldPrice`, `beds`, `baths` | [JSON](workflows/zillow-for-sale-rent-and-sold-listing-extractor.json) | [Watch](https://www.youtube.com/shorts/bNjKOMdRlSY) |

## FAQ

### Are these n8n workflows free?
Yes. The workflow files are MIT-licensed. Each one calls a public Apify Actor on your own Apify account, so the only cost is that Actor's usage.

### Do I need an Apify account?
Yes. The **Run Apify Actor** node sends your Apify API token as a Query Auth credential. Apify's free plan includes a monthly usage credit, which is enough for small test runs. No token is stored in the JSON files.

### How much does a run cost?
It depends on the Actor's pricing (per result, per event or per compute unit) and on how many rows you ask for. Each workflow page links its Actor; the Actor's Pricing tab shows the current price. Start with a small limit in **Configure input**.

### Can I export the rows to Google Sheets or CSV?
Yes. Every workflow ends in a disabled **Google Sheets** node set to append rows with automatic column mapping; enable it after adding your Google credential and sheet ID. For CSV, add n8n's **Convert to File** node after **Rows ready**.

### How do I import a workflow into n8n?
Use **Import from URL** with the raw GitHub link of the JSON file, or download the file and use **Import from file**. Both are in the workflow editor's **⋯** menu. Then select your Apify credential in **Run Apify Actor**.

### Does it work on n8n Cloud and self-hosted n8n?
Yes. The workflows only use core nodes (Schedule Trigger, Code, HTTP Request, No Operation, Google Sheets), which ship with both.

### How long can a run take?
The **Run Apify Actor** node calls `run-sync-get-dataset-items`, which waits up to 300 seconds for the run and returns the rows. For larger jobs, start the run with `/runs` and read its dataset when it finishes.

### What data do these workflows collect?
Only public pages: no logins, cookies or private accounts. Check the target site's terms and your local law before running at scale.

## How every workflow is built

Daily trigger → Configure input → Run Apify Actor → Normalize + dedupe → Rows ready → Google Sheets (optional, disabled)

- **Configure input** holds the Actor input as a plain object; the Actor's input schema is listed on each workflow page.
- **Normalize + dedupe** trims strings, drops empty values, adds `_source` and `_scrapedAt`, and removes duplicate rows on a stable ID or URL the Actor returns (never an email or phone: chain locations share those).
- Every starter input is checked against the Actor's input schema when the repo is published, and the first run stays small (at most 50 rows) so it fits n8n's 300-second wait.

## Related

- Agent skills (SKILL.md) for the same Actors: https://github.com/bolvein-firex/scraping-skills
- Short video breakdowns: https://www.youtube.com/@ScraperFinder
- Step-by-step tutorials (dev.to series "Free n8n scraping workflows"): https://dev.to/scraperfinder/series/46235
- Setup notes: [docs/setup-apify.md](docs/setup-apify.md), [docs/import.md](docs/import.md)

## Contributing

Missing a site? [Request a workflow](https://github.com/bolvein-firex/scraping-n8n-workflows/issues/new/choose). Questions go to [Discussions](https://github.com/bolvein-firex/scraping-n8n-workflows/discussions). See [CONTRIBUTING.md](CONTRIBUTING.md).

## Guardrails

Public data only. Do not use these workflows for private, login-protected or paywalled data. Respect robots.txt, site terms and local law.

## License

MIT
