# G2 and Capterra Review Lead Scoring for n8n - Free Apify to Google Sheets Workflow

A complete n8n workflow that fetches public G2 or Capterra reviews through the Apify actor you configure, normalizes the results, scores possible switching intent, and appends every scored review to Google Sheets.

Free to download and use. There are no disabled nodes or upgrade stubs; the workflow is complete on its own.

**Download:** [`workflow/g2-capterra-review-lead-scoring-free.json`](workflow/g2-capterra-review-lead-scoring-free.json)

## What it actually does

1. Runs every day at 7:00 in the workflow's configured timezone.
2. Calls the G2 or Capterra review actor you configure in Apify.
3. Normalizes the actor output, filters reviews by your star-rating limit, removes duplicates within the run, and caps the batch at 25.
4. Scores each retained review for possible switching intent and gives a short reason.
5. Appends every scored review to the `Reviews` tab in Google Sheets.

The workflow logs low scores too, which gives you a complete record of what was evaluated.

## What you need

Three credentials:

| # | Credential | Used for |
|---|---|---|
| 1 | Apify API token via Header Auth | Running the review actor and retrieving its dataset |
| 2 | OpenAI-compatible API key via Header Auth | Scoring the normalized reviews |
| 3 | Google Sheets OAuth account | Appending the scored review rows |

You also need an n8n Cloud or compatible self-hosted instance.

## Setup

1. Import `workflow/g2-capterra-review-lead-scoring-free.json` into n8n.
2. Open **Your settings (EDIT ME)** and enter the competitor URL, your ICP description, your switching-intent criteria, and the highest star rating you want to keep.
3. Open **Fetch G2 and Capterra reviews (Apify)**. Replace `YOUR-USERNAME~YOUR-ACTOR` with your actor ID.
4. Replace the empty `{}` request body with that actor's own documented input parameters.
5. Connect the three credentials listed above.
6. Create a Google Sheet with a tab named `Reviews`, add the exact header row below, and paste the sheet URL into **Log scored reviews (Google Sheets)**.
7. Run the workflow manually once, inspect the appended rows, then activate the daily schedule when you are satisfied.

Exact sheet headers:

```text
processedAt source reviewerName reviewText rating reviewDate reviewUrl competitorProductUrl switchingIntentScore reason
```

### Which Apify actor?

Use any suitable G2 or Capterra review actor, provided you supply that actor's own input parameters. Actor input bodies are not interchangeable, so the empty `{}` body is intentionally not presented as universal.

The output normalizer is actor-agnostic. It maps common review field aliases without depending on a specific actor ID. If your chosen actor uses different output names, extend the aliases in **Normalize, filter and dedupe reviews**.

## Paid edition

The [Competitive Intel Pack paid edition](https://willowridge7.gumroad.com/l/n8n-competitive-intel-pack) adds the Pipedrive delivery workflow and the buyer setup package. This free workflow remains fully usable without it.

## Licence

Free to use and modify for your own business or your clients' businesses, including agency deployments.

**Not open source.** You may not resell, redistribute, sublicense, or repackage the workflow itself as your own product. See [LICENSE.txt](LICENSE.txt).

## Honest status

This repository was published recently. It has no users, no reviews, and no results to claim. Nothing here is a customer-success or performance claim; inspect the workflow and judge it on what it does.

Built by [Rook Data Tools](https://apify.com/rook-data-tools).

## Related

Other free workflows and guides we publish:

- [n8n-ai-lead-scoring](https://github.com/willowridge1234/n8n-ai-lead-scoring) — Free workflow — score scraped leads against your ICP, log to Google Sheets
- [n8n-tradeshow-exhibitor-lead-scoring](https://github.com/willowridge1234/n8n-tradeshow-exhibitor-lead-scoring) — Free workflow — score trade-show exhibitors against your ICP
- [n8n-lead-scoring-guide](https://github.com/willowridge1234/n8n-lead-scoring-guide) — Guide — which signals predict a good lead, and how to tell if scoring works
- [chamber-association-lead-lists](https://github.com/willowridge1234/chamber-association-lead-lists) — Guide — building B2B lead lists from chamber & association directories
