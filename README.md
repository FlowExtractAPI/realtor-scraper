**[Realtor.com Scraper](https://apify.com/dz_omar/realtor-scraper?fpr=smcx63)** extracts **US property data from Realtor.com** — homes **for sale, for rent, sold and off market** — from a pasted search link, a typed place or a list of addresses. Every property comes back as one complete record: **price history, taxes, value estimates, schools, climate risk, local market statistics and agent contacts**.

Perfect for **real estate investors**, **agents and brokers**, **analysts and researchers** and **proptech teams** who need Realtor.com data in a spreadsheet, a database or an API, without copying listings by hand.

## What does Realtor.com Scraper do?

- **Three ways to search** — paste Realtor.com **links**, type **locations** (cities, ZIP codes, counties, neighborhoods, whole states) or give **addresses, property IDs and listing links**.
- **Every listing type** — for sale (including builder "to be built" plans, exactly as on realtor.com), for rent, recently sold and off market.
- **30+ filters** — property type, price, bedrooms, bathrooms, living area, lot size, year built, HOA, listing age, price reductions, open houses, keywords, 50+ features, new construction, foreclosures, 55+ communities, pending / contingent, virtual and 3D tours, pet policy, radius or a drawn area.
- **Go beyond 10,000 results** — Realtor.com stops a single search at 10,000 properties; large searches are read in parts so you can reach every match in a state or a metro area.
- **Full or summary** — the complete property record, or just what the search results show for fast, small exports.
- **Sorted your way** — newest, recently updated, price, bedrooms, lot size, photos or sale date.
- **Resumable** — an interrupted run continues where it left off instead of starting over.

### What data can you extract from Realtor.com?

| Category | Fields |
|---|---|
| Listing | property ID, listing ID, status, link, list date, last update, price changes, days on market |
| Price | list price, price per sqft, last sold price and date, HOA fee, monthly fees (rentals) |
| Property | type and sub-type, bedrooms, full / half / three-quarter baths, living area, lot, stories, garage, year built and renovated, construction, exterior, roofing, zoning, heating, cooling, categorized feature lists |
| Location | address parts, coordinates, county and FIPS code, neighborhoods, ZIP, street view |
| Local market | median listing price, median sold price, days on market, price per sqft, median rent and hotness for the **city, county, neighborhood, ZIP and state** |
| Value estimates | current values from several providers with low / high range, value history and a **12-month forecast** |
| History and taxes | every listing, price-change and sale event, tax history with assessed and market values, building permits |
| Mortgage | monthly payment estimate and its parts, rates, property tax rate, **insurance rate, FHA loan limit**, FHA and down-payment-assistance eligibility |
| Schools | assigned and nearby schools with rating, grades, district, enrollment, student-teacher ratio, parent rating, reviews and IDs; optional test scores |
| **Climate and environment risk** | flood, wildfire, heat, wind and air-quality scores and severity with trend notes, FEMA zone, flood insurance requirement, noise score |
| Agents and offices | listing agents, offices and brokers with phones, emails, license, MLS IDs and addresses; buyer side on sold properties |
| Media | photos with machine-read labels (kitchen, exterior…), virtual and 3D tours, videos, floor plans, open houses |
| Rentals | units and floor plans with availability, fees, pet policy, application link, lease terms |

Records keep Realtor.com's own field names and structure, and empty values stay as `null`.

### Why use Realtor.com Scraper on Apify?

Running it on Apify gives you **API access**, **scheduling**, **monitoring**, **webhooks**, **integrations** (Make, Zapier, n8n, Google Sheets) and **proxy rotation** without managing infrastructure. Export the dataset as JSON, CSV, Excel or HTML, or read it over the API while the run is still going — properties are saved the moment they are collected.

## How to scrape Realtor.com

1. Open **Realtor.com Scraper** in Apify Console.
2. Choose **Search by**: **Links**, **Locations** or **Properties**.
3. Fill in the matching section — paste links, type places and pick a **Listing type**, or list addresses and property IDs. Add filters if you want to narrow the search.
4. Set **Max results per search** (start small: `10`) and, for a first look, **Detail level** `Summary`.
5. Click **Start**, wait for the run to finish, then download the results as JSON, CSV or Excel, or fetch them over the API.

## How much does it cost to scrape Realtor.com?

Pay per result. Accounts without a paid Apify plan pay the Bronze price.

| Event | Bronze | Silver | Gold |
|---|---|---|---|
| **Property** — full record | $0.0015 | $0.0012 | $0.0009 |
| **Property (summary)** — search-result record | $0.0006 | $0.0005 | $0.0004 |
| Run start (per GB of memory; this Actor runs at 1 GB) | $0.003 | $0.003 | $0.003 |

- **1,000 full records** cost **$1.50** (Bronze), **$1.20** (Silver) or **$0.90** (Gold), plus the run start.
- **1,000 summary records** cost **$0.60**, **$0.50** or **$0.40**.
- A property that could not be loaded in full is delivered without a charge.
- Set a **maximum cost per run** and the Actor stops at that limit, keeping everything collected so far.

## Input and output examples

### Input

Search a city for houses under a price, newest first:

```json
{
    "searchBy": "locations",
    "locations": ["Austin, TX"],
    "listingType": "for_sale",
    "propertyTypes": ["single_family"],
    "maxPrice": 600000,
    "minBeds": 3,
    "sortBy": "newest",
    "maxResults": 100
}
```

Paste links from realtor.com (filters you set are applied on top of each link):

```json
{
    "searchBy": "links",
    "startUrls": [
        { "url": "https://www.realtor.com/realestateandhomes-search/Las-Vegas_NV/type-single-family-home/beds-2-3/price-200000-400000" }
    ],
    "maxResults": 500
}
```

Look up exact properties:

```json
{
    "searchBy": "properties",
    "properties": ["3808 Warm Meadows St, Las Vegas", "1634334368"]
}
```

| Input | What it does |
|---|---|
| **Search by** | `links`, `locations` or `properties` — one mode per run; the other sections are ignored |
| **Links** | search or property links copied from realtor.com |
| **Locations** + **Listing type** | cities, ZIP codes, counties, neighborhoods or states; for sale (with builder plans, like realtor.com), for sale (existing listings only), for rent, sold or off market |
| **Properties** | street addresses, property IDs or property links |
| **Filters** | property types, price, bedrooms, bathrooms, living area, lot size, year built, HOA, listed / price-reduced / open-house / sold windows, keywords, features, new construction, foreclosure, 55+, pending / contingent, coming soon, tours, pets, radius, drawn area, sort |
| **Max results per search** | `0` = every match |
| **Go beyond 10,000 results** | read very large searches in parts |
| **Detail level** | `full` or `summary` |
| **All photos in the sales history**, **School test scores** | optional extras that make records larger |

### Output

Each property is one record. An excerpt of a real result (the full record has several hundred fields):

```json
{
  "property_id": "1404642873",
  "status": "for_sale",
  "list_price": 490000,
  "price_per_sqft": 321,
  "list_date": "2026-11-02T20:55:37Z",
  "last_sold_price": 276500,
  "last_sold_date": "2015-01-29",
  "description": {
    "type": "single_family",
    "beds": 3,
    "baths_consolidated": "2.5",
    "sqft": 1528,
    "lot_sqft": 2160,
    "stories": 2,
    "garage": 2,
    "year_built": 2009,
    "heating": null,
    "cooling": null
  },
  "estimates": {
    "current_values": [
      {
        "source": { "type": "collateral", "name": "Collateral Analytics" },
        "estimate": 520000,
        "estimate_high": 556400,
        "estimate_low": 483600,
        "date": "2026-10-14",
        "isbest_homevalue": true
      }
    ]
  },
  "mortgage": {
    "property_tax_rate": 0.00555306,
    "insurance_rate": 0.0053,
    "county_fha_loan_limit": 557750,
    "estimate": { "monthly_payment": 3401, "down_payment": 98000 }
  },
  "local": {
    "flood": { "flood_factor_score": 1, "flood_factor_severity": "minimal" },
    "wildfire": { "fire_factor_score": 6, "fire_factor_severity": "Major" },
    "heat": { "heat_factor_score": 8, "heat_factor_severity": "Severe" }
  },
  "location": {
    "county": {
      "name": "Maricopa",
      "fips_code": "04013",
      "geo_statistics": {
        "housing_market": {
          "median_listing_price": 463000,
          "median_sold_price": 465000,
          "median_days_on_market": 65,
          "median_price_per_sqft": 265
        }
      }
    }
  },
  "nearby_schools": {
    "schools": [
      {
        "name": "Explorer Middle School",
        "rating": 7,
        "distance_in_miles": 0.4,
        "funding_type": "public",
        "student_count": 607,
        "parent_rating": 3,
        "review_count": 30
      }
    ]
  },
  "_meta": { "level": "full", "rank": 1 }
}
```

Every record also carries `source_url` (the property page), `_source` and `_meta` (which search found it, its position, whether it is a full or summary record, and when it was collected).

## Other Actors you might need

| Actor | What it adds |
|---|---|
| **[Zillow Scraper](https://apify.com/dz_omar/zillow-scraper?fpr=smcx63)** | The same US market from Zillow — listings, prices and property details to compare with Realtor.com |

## Frequently asked questions

### Is it legal to scrape Realtor.com?

Realtor.com Scraper collects **publicly available** listing information. You are responsible for using the data in line with Realtor.com's terms, the rules for MLS data and applicable privacy laws such as GDPR and CCPA. This is not legal advice.

### Do I need a Realtor.com account?

No. Links, places and addresses are all it needs.

### How many properties can I get from one search?

Realtor.com itself cuts any single search at 10,000 properties. With **Go beyond 10,000 results** on (the default) and **Max results per search** above 10,000 or `0`, the Actor reads a larger search in parts so you can reach every match. Properties without a listed price cannot be placed in those parts and are not included in a very large search. For the most complete coverage of a huge area, run it by state or county.

### Can I scrape sold, rental and off-market listings?

Yes. In **Locations** choose the **Listing type**; in **Links** paste the matching realtor.com link (sold, rentals and so on). Sold searches can be limited to the last N days, and **Price** then means the sold price.

### Does it include new-construction (builder) plans?

Yes. Realtor.com shows builder "to be built" plans in sale searches, and so does this Actor: pasted links return exactly what the link shows on realtor.com, and **Listing type: For sale** includes them. Choose **For sale: existing listings only** to leave them out.

### Can I look up one address or property ID?

Yes — use **Search by: Properties**. Addresses are matched with Realtor.com's own address lookup; anything that does not match is skipped and listed in the log.

### What is the difference between full and summary?

**Full** returns the complete record described above. **Summary** returns only what the search results show (address, price, status, size, photo, agent): several times smaller, much faster, and priced lower.

### Can I get agent contact details?

Records include the business contact details published with the listing: listing agent and office names, phones, emails, license numbers and addresses. They are the details Realtor.com shows on the listing, nothing more.

### What happens if a run is interrupted?

It saves its progress and continues where it left off instead of starting over.

### Why did my run return fewer results than I asked for?

| Situation | What you see | What to do |
|---|---|---|
| The search has fewer matches | fewer properties than **Max results per search** | loosen the filters or widen the place |
| An option does not apply to the search | the log lists what was not used | for example *cats allowed* only applies to rentals |
| A typed place was not found | `Skipping "…" — no matching place found` | add the state, e.g. `Springfield, IL` |
| The maximum cost per run was reached | the status message says the limit was reached | raise the limit |
| Nothing matches | one row (`no_results`) and a log line list your filters and which single filter, left out, would bring properties back | loosen that filter; nothing is charged |
| Wrong or empty input | one row in the dataset explains what to change | follow the row; nothing is charged |

### I used an earlier version. What changed?

Field names are unchanged and the earlier fields are still there; records now carry many more (see the table above), plus `source_url` and `_meta`. Two differences: `_source` is now `realtor_scraper`, and each sales-history event carries one photo by default (turn on **All photos in the sales history** for the full set). Saved tasks and API calls with `startUrls` and `maxResults` keep working as they were.

### Can I use Realtor.com Scraper in Make, Zapier, n8n or my own code?

Yes. Use the Apify integrations, webhooks, the REST API or the JavaScript and Python client libraries — start a run, wait for it and read the dataset.

## Support

- 🌐 **Website:** [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email:** [flowextractapi@outlook.com](mailto:flowextractapi@outlook.com)
- 💬 **GitHub:** [FlowExtractAPI](https://github.com/FlowExtractAPI)
- 💼 **LinkedIn:** [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **X (Twitter):** [@FlowExtractAPI](https://x.com/FlowExtractAPI)
- 📱 **Facebook:** [flowextractapi](https://www.facebook.com/flowextractapi)
- 🎵 **TikTok:** [@flowextractapi](https://www.tiktok.com/@flowextractapi)

## Legal & compliance

- **Public data only** — processes publicly available data.
- **Rate limiting** — respects source-service limits and terms of use.
- **Data protection** — no storage of personal information or unauthorized data collection.
- **Commercial use** — suitable for business intelligence and research.
- No affiliation with or endorsement by Realtor.com is implied.

---

*Realtor.com Scraper — by FlowExtract API. Turn any website into structured data.*
