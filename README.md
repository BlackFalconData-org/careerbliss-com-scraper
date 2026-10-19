# CareerBliss Reviews Scraper [Just 💰$0.59]

Extract structured data from [careerbliss.com](https://careerbliss.com) — employee reviews from careerbliss.com by company name or company reviews URL. Each review carries the reviewer's job title and star rating with eight workplace category scores, plus the company's own average rating, review count and average salary figures.

**[CareerBliss Reviews Scraper [Just 💰$0.59] on Apify →](https://apify.com/blackfalcondata/careerbliss-com-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 📝 description format, and more.

**Incremental mode** — Only get new or changed reviews since your last run. Content hash per review — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how reviews evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N reviews (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every review returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured reviews from careerbliss.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor reviews, track trends, and analyze market dynamics with structured, deduplicated data from careerbliss.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Lead generation**
Extract contact details alongside ${NOUNS} to build targeted outreach lists for sales teams, partnerships, or B2B prospecting.

**AI / LLM training data**
Structured JSON per review is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "Best Buy",
  "maxResults": 100,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "emitUnchanged": false,
  "emitExpired": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Company name or careerbliss.com company slug (e.g. "best-buy"). Required if no startUrls provided. |
| `location` | string | — | Optional city filter, e.g. "Charlotte, NC". |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `enrichEmails` | boolean | `false` | Off by default. Looks up each company's own website and reads its homepage and a few contact pages for public contact emails. Adds contactWebsite, contactEmail and contactEmails to every review of that company. Checked once per company per run; adds a few seconds per company. |
| `startUrls` | array | `[]` | Paste careerbliss.com company review page URLs (e.g. https://www.careerbliss.com/best-buy/reviews/). Each URL becomes its own task; results are merged and deduped by review ID. When provided, startUrls REPLACE the company/location fields. |
| `descriptionMaxLength` | integer | `0` | Truncate review text to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, locations, startUrls) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `skipReposts` | boolean | `false` | When incremental, skip listings whose content matches an expired listing from a prior run (cross-run duplicate detection). |
| `emitUnchanged` | boolean | `false` | When incremental mode is on, also emit listings whose content has not changed since the last run. |
| `emitExpired` | boolean | `false` | When incremental mode is on, also emit listings that were seen before but are no longer found. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED listings. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of listings included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |

---

## Output fields

Every review returns the same 42-field schema. Missing values are `null` — never omitted.

- `listingId`
- `review_id`
- `company_name`
- `job_title`
- `rating`
- `review_text`
- `source_url`
- `aggregate_rating`
- `aggregate_review_count`
- `title`
- `entityName`
- `location`
- `reviewId`
- `reviewUrl`
- `companyName`
- `companySlug`
- `companyId`
- `jobTitle`
- `jobTitleId`
- `jobTitleSlug`
- `locationUrl`
- `reviewText`
- `reviewBody`
- `categoryRatings`
- `aggregateRating`
- `aggregateReviewCount`
- `averageSalary`
- `hourlyRate`
- `companyStats`
- `sourceUrl`
- `portalUrl`
- `contactWebsite`
- `contactEmail`
- `contactEmails`
- `page`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per review. Here is a real example from a production run:

```json
{
  "listingId": "2e38685e55c0d5325e3ac5b8b7fbf6be9eecd6cea77864b5575a1f8146504256",
  "review_id": "2092122",
  "company_name": "Starbucks",
  "job_title": "Starbucks Employee",
  "rating": 3.6,
  "review_text": "As a Shift Supervisor at Starbucks, I was responsible for overseeing a team of baristas and ensuring that daily operations were running smoothly. The salary for this position was f…",
  "source_url": "https://www.careerbliss.com/starbucks/reviews/anonymous-employee/#2092122",
  "aggregate_rating": 3.9,
  "aggregate_review_count": 204,
  "title": "Starbucks Employee",
  "entityName": "Starbucks",
  "location": ""
}
```

*Truncated — full records contain 42 fields. See Output fields for the complete schema.*

**[Try CareerBliss Reviews Scraper [Just 💰$0.59] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/careerbliss-com-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.000594 |

See the [actor on Apify](https://apify.com/blackfalcondata/careerbliss-com-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape careerbliss.com?**
Use this actor on Apify to extract structured data from careerbliss.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get careerbliss.com data as JSON, CSV, or Excel?**
The actor writes each review to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape careerbliss.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check careerbliss.com's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each review gets a content hash. On subsequent runs, only new or changed reviews are emitted — saving time, compute, and storage. Expired reviews can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [Djinni Scraper](https://apify.com/blackfalcondata/djinni-scraper?fpr=1h3gvi) — Ukraine & CEE tech jobs with salary and English level
- [Work.ua Scraper](https://apify.com/blackfalcondata/work-ua-scraper?fpr=1h3gvi) — Ukraine's work.ua job listings
- [NoFluffJobs Scraper](https://apify.com/blackfalcondata/nofluffjobs-scraper?fpr=1h3gvi) — Poland & CEE IT jobs with transparent salary ranges
- [OLX Jobs Scraper](https://apify.com/blackfalcondata/olx-jobs-scraper?fpr=1h3gvi) — OLX job listings across 7 CEE countries
- [Prace.cz Scraper](https://apify.com/blackfalcondata/prace-scraper?fpr=1h3gvi) — Czech Republic's prace.cz job board
- [Profession.hu Scraper](https://apify.com/blackfalcondata/profession-scraper?fpr=1h3gvi) — Hungary's profession.hu job board

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [CareerBliss Reviews Scraper [Just 💰$0.59]](https://apify.com/blackfalcondata/careerbliss-com-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
