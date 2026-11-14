# Lead Scraper & Enrichment

Takes a form submission (e.g. "find me business leads matching X criteria") and turns it into an enriched, deduplicated list of prospects with verified emails, ready to load into a CRM sheet.

## What it does

Turns a simple request into a clean prospect list — scraped, enriched, deduplicated, and sorted by whether a verified email was found.

## How it works

- Triggered by an n8n form submission
- Uses an Apify actor to scrape business listings/search results for the given criteria
- Runs the results through cleaning steps (JavaScript code nodes) to parse and normalize the raw SERP/scrape data
- Attempts to extract or find an email for each business; leads with a found email go to a "Data complete" sheet, leads without go to separate "Without mail" sheets for manual follow-up
- Deduplicates records before writing to Google Sheets, so the same business never gets contacted twice

## Why it matters

This is the top of the outreach funnel — it's what feeds the cold email and CRM systems with fresh, clean prospect data instead of manually researching each lead.

## File

- `lead-scraper-enrichment.json` — n8n workflow, 16 nodes

## Requirements

- n8n instance
- Apify account + actor for business-listing scraping
- Google Sheets (Data complete + Without mail sheets)

## Setup

1. Import `lead-scraper-enrichment.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, Apify actor details) with your own credentials and sheet IDs
3. Set up the Google Sheets with matching column headers

## Note

Sanitized for public sharing — credentials, sheet IDs, and API details have been replaced with placeholders.
