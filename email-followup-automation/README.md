# Email Follow-up Automation

Automates a multi-region cold email follow-up sequence (configurable per target market/region) with reply handling.

## What it does

Keeps follow-up emails going out on schedule across multiple markets, and picks up replies automatically instead of letting them sit in an inbox.

## How it works

- A scheduled trigger pulls leads from region-specific Google Sheets (one sheet per target market)
- A `Switch` node routes each lead down the correct regional path
- Loops through leads in batches, sends a follow-up email via Gmail, and waits a set interval before the next batch — avoiding spam-trigger sending patterns
- A separate branch handles a manual trigger for one-off follow-ups and processes inbound Gmail replies, so responses to a cold email get picked up automatically rather than sitting in an inbox

## Why it matters

This is the engine behind the daily cold emails — it keeps the follow-up sequence running on schedule without manual sending, across multiple markets at once.

## File

- `email-followup-automation.json` — n8n workflow, 15 nodes

## Requirements

- n8n instance
- Gmail account
- Google Sheets (one per target region)

## Setup

1. Import `email-followup-automation.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`) with your own credentials and sheet IDs
3. Set up one Google Sheet per region with matching column headers
4. Adjust the batch size and wait interval to your sending limits

## Note

Sanitized for public sharing — credentials, sheet IDs, and email addresses have been replaced with placeholders.
