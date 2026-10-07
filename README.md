# CMS Hospital Quality Scraper: Star Ratings & HCAHPS

Pull CMS hospital quality data: overall star ratings, patient survey (HCAHPS) scores, and complication rates for 4,500+ US hospitals by state or city. The official CMS quality dataset, no API key required.

**Run it on Apify:** [apify.com/themineworks/cms-hospital-quality](https://apify.com/themineworks/cms-hospital-quality)
**Docs, FAQ and pricing:** [themineworks.com/actors/cms-hospital-quality](https://themineworks.com/actors/cms-hospital-quality/)

**Price:** From $0.60 per 1,000 hospitals on Apify's higher plans ($1.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged.

## What it returns

* Overall star ratings for 4,500+ US hospitals
* HCAHPS patient survey scores
* Complication and readmission rates
* Filter by state or city
* Empty results are never charged

## Quick start

You need a free [Apify account](https://console.apify.com/sign-up) and its API token (Settings, API & Integrations).

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("themineworks/cms-hospital-quality").call(run_input={
    "state": "CA",
    "city": "Los Angeles",
    "hospitalName": "Mayo Clinic",
    "maxResults": 25
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });
const run = await client.actor('themineworks/cms-hospital-quality').call({
    "state": "CA",
    "city": "Los Angeles",
    "hospitalName": "Mayo Clinic",
    "maxResults": 25
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL

One request that runs the actor and returns the results in the response (for runs under 5 minutes):

```bash
curl -X POST "https://api.apify.com/v2/acts/themineworks~cms-hospital-quality/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"state": "CA", "city": "Los Angeles", "hospitalName": "Mayo Clinic", "maxResults": 25}'
```

### Command line

This repo includes ready-made clients that save results to JSON and CSV:

```bash
python3 cms_hospital_quality_scraper.py --token YOUR_APIFY_TOKEN --state "CA" --city "Los Angeles" --hospital-name "Mayo Clinic" --max-results "25"
node cms_hospital_quality_scraper.mjs --token YOUR_APIFY_TOKEN --state "CA" --city "Los Angeles" --hospital-name "Mayo Clinic" --max-results "25"
```

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `state` | string |  | Filter by US state code (for example CA, NY, TX) |
| `city` | string |  | Filter results to hospitals in this city, for example "Los Angeles" or "Houston" |
| `hospitalName` | string |  | Filter by hospital name, partial matches work, for example "Mayo Clinic" or "General Hospital" |
| `maxResults` | integer | `200` | Maximum number of hospital records to return in this run |
| `minStars` | integer |  | Return only hospitals with this overall star rating or higher (1-5) |

## Output

One row per result, as JSON, CSV, Excel or through the API.

| Field | Type | Description |
|---|---|---|
| `hospital_name` | string | Hospital facility name |
| `facility_id` | string | CMS facility identifier |
| `address` | string | Street address |
| `city` | string | City |
| `state` | string | State abbreviation |
| `zip_code` | string | ZIP code |
| `county_name` | string | County name |
| `phone_number` | string | Hospital phone number |
| `hospital_type` | string | Type of hospital (Acute Care, Critical Access, etc.) |
| `hospital_ownership` | string | Ownership type (Government, Proprietary, Non-profit, etc.) |
| `overall_star_rating` | string | Overall CMS star rating (1-5) |
| `emergency_services` | string | Whether emergency services are available |
| `scraped_at` | string | Timestamp when the record was scraped |

## Use it from an AI agent

The actor works as a tool in Claude, Cursor or any MCP client through Apify's MCP server:

```
https://mcp.apify.com/?tools=themineworks/cms-hospital-quality
```

## FAQ

### How much does the CMS Hospital Quality Scraper cost?

From $0.60 per 1,000 hospitals on Apify's higher plans ($1.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged. You can cap what a single run may spend with the maximum cost setting on Apify.

### Can I export the results to CSV or Excel?

Yes. Every run saves to an Apify dataset you can download as JSON, CSV, Excel or XML, or read through the API. The Python and Node clients in this repo also write the results to local files.

### Can I run it on a schedule?

Yes. Save your input as a task on Apify and attach a schedule, or call the API from your own cron job. Scheduled runs are billed the same way as manual ones.

## Related scrapers

* [India Gov Data](https://themineworks.com/actors/india-data-gov-scraper/): Trade, prices, and thousands of datasets from data.gov.in
* [CourtListener Scraper](https://themineworks.com/actors/courtlistener-court-records/): US court opinions, dockets, and case law as structured JSON
* [Socrata Open Data](https://themineworks.com/actors/socrata-open-data/): Any government data portal: CDC, HHS, NYC, Texas, and hundreds more

Part of [The Mine Works](https://themineworks.com/): 151 pay-per-result scrapers with no login and no browser setup on your side.

## License

MIT © The Mine Works
