# EU Public Tenders Monitor - TED & BOAMP (Only New)

Monitor public procurement notices from TED (all EU countries) and BOAMP (France) by keyword, country, CPV code, deadline and value. One clean schema, official source links, optional mode that returns only notices you have not received before. No personal data.

**▶ Run it on Apify Store: https://apify.com/far003/eu-public-tenders**

> This repository hosts documentation and examples; the Actor runs on the Apify platform.

## What it does

- Finds public tenders across all EU countries (TED, the official EU procurement journal) and in France, including small contracts that never reach TED (BOAMP), in one clean schema.
- Filters by keyword, buyer country, CPV code, notice type, offer deadline and value.
- Each record has the buyer, the main CPV code, the estimated (and awarded) value, the deadline and a link to the official notice.
- Feed mode (`onlyNew`): every run returns only the tenders you have not seen before.
- Contact persons' names, e-mail addresses and phone numbers are never delivered.

## Who it is for

- Companies that bid for public contracts.
- Bid consultants and tender agencies watching many clients.
- Sales and market analysts looking at who buys what, where and for how much.
- Developers who need a tender API without writing a TED client.

## Example input

The prefilled input of the Actor: tenders published in the last 7 days that mention `cybersecurity`, at most 25 per source.

```json
{
    "keywords": [
        "cybersecurity"
    ],
    "noticeTypes": [
        "tender"
    ],
    "sources": [
        "ted",
        "boamp"
    ],
    "publishedLastDays": 7,
    "maxResultsPerSource": 25
}
```

## Example output

A TED contract notice (real run on 19 October 2026, description shortened):

```json
{
  "id": "ted:722163-2026",
  "source": "TED",
  "noticeId": "722163-2026",
  "procedureId": "c787190e-bcd5-4b10-9fb8-b46298a4d75e",
  "noticeType": "cn-standard",
  "noticeTypeLabel": "Contract or concession notice (standard regime)",
  "noticeCategory": "tender",
  "procedureType": "open",
  "procedureTypeLabel": "Open",
  "contractNature": "services",
  "title": "Maintenance et acquisition de licences BO SAP et prestations de montée de version",
  "titleLanguage": "fr",
  "englishHeadline": "France – Software development services – Maintenance et acquisition de licences BO SAP et prestations de montée de version",
  "description": "L'accord-cadre sera exécuté par l'émission de bons de commande. Les prestations sont réglées par des prix unitaires et forfaitaires. Les montants estimatifs sont...",
  "buyerName": "Région Hauts-de-France",
  "otherBuyers": [],
  "buyerCountry": "FR",
  "buyerCountryName": "France",
  "buyerCity": "Lille",
  "cpvCode": "72262000",
  "cpvDescription": "Software development services",
  "additionalCpvCodes": [],
  "estimatedValue": 600000,
  "estimatedValueCurrency": "EUR",
  "estimatedValueBasis": "procedure",
  "awardedValue": null,
  "awardedValueCurrency": null,
  "publicationDate": "2026-10-19",
  "dispatchDate": "2026-10-16",
  "deadlineDate": "2026-11-06",
  "deadline": "2026-11-06T12:00:00+01:00",
  "deadlineType": "tender",
  "deadlines": [{ "type": "tender", "deadline": "2026-11-06T12:00:00+01:00" }],
  "url": "https://ted.europa.eu/en/notice/-/detail/722163-2026",
  "alsoOnTed": null,
  "sourceLicense": "Free reuse, commercial included (European Commission Decision 2011/833/EU, TED legal notice)",
  "attribution": "Source: TED (Tenders Electronic Daily), Publications Office of the European Union, https://ted.europa.eu - (c) European Union. Notices can be freely reused, for commercial or non-commercial purposes.",
  "retrievedAt": "2026-10-19T12:36:28.530Z"
}
```

## Use it from code

Set your token in the `APIFY_TOKEN` environment variable.

**Node.js** ([`apify-client`](https://docs.apify.com/api/client/js/))

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('far003/eu-public-tenders').call({
    "keywords": [
        "cybersecurity"
    ],
    "noticeTypes": [
        "tender"
    ],
    "sources": [
        "ted",
        "boamp"
    ],
    "publishedLastDays": 7,
    "maxResultsPerSource": 25
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

**Python** ([`apify-client`](https://docs.apify.com/api/client/python/))

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("far003/eu-public-tenders").call(run_input={
    "keywords": ["cybersecurity"],
    "noticeTypes": ["tender"],
    "sources": ["ted", "boamp"],
    "publishedLastDays": 7,
    "maxResultsPerSource": 25
})
items = client.dataset(run["defaultDatasetId"]).list_items().items
print(items)
```

## Pricing

Pay per result — see the current price on the Store page.

## Data source & licence

Tender data: TED (Tenders Electronic Daily), Publications Office of the European Union, https://ted.europa.eu, © European Union, reused under Commission Decision 2011/833/EU. French data: BOAMP, Direction de l'information légale et administrative (Premier ministre), https://www.boamp.fr, Licence Ouverte / Open Licence. CPV names come from the official CPV 2008 list of the Publications Office of the European Union. This Actor is not affiliated with, or endorsed by, the European Union, the Publications Office, DILA or the French State.

## Support

Open an issue in this repository or use the Issues tab on the Store page.

## Licence

The documentation and examples in this repository are released under the MIT licence (see `LICENSE`). The Actor itself is proprietary and runs on the Apify platform.
