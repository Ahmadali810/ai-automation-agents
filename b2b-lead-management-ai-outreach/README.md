# B2B Lead Management & AI Outreach

A complete automated B2B SDR pipeline in a single workflow — takes raw leads from list to qualified meeting: validation, enrichment, lead scoring, AI-written personalized cold emails, multi-channel touchpoints, AI reply classification, and full run analytics.

## What it does

Raw lead list in, qualified meetings out — with scoring, compliance guardrails, and analytics on every run.

## How it works

- **Intake & validation:** Leads enter (test dataset included; swappable for CSV, Google Sheets, or webhook). Emails are format-validated and checked against a suppression list — invalid or suppressed leads are logged and dropped before anything else runs
- **Enrichment:** Two-stage HTTP enrichment pulls company and contact details, with success/failure branching and fallback flags so a failed enrichment never kills the lead
- **Compliance & scoring:** Geo-compliance flags mark GDPR-sensitive countries and do-not-contact regions; then a weighted lead score (industry value, country tier, company size, estimated revenue, pain-point depth, enrichment bonus) segments every lead into HIGH / MEDIUM / LOW tiers with per-tier outreach tones
- **AI outreach:** An OpenAI agent writes a personalized cold email per lead (structured subject + body via a strict output schema), with A/B subject-line variants, per-channel rate-limit checks, and quiet-hours protection before anything sends
- **Multichannel:** HIGH and MEDIUM leads also get LinkedIn DM and WhatsApp/SMS message variants generated from the email body
- **Reply handling:** A second AI agent classifies every reply (interested / follow_up_later / not_interested / unclear) and a `Switch` routes each: interested leads get an AI-drafted meeting follow-up written to PostgreSQL, follow-up-laters get 7-day and 14-day scheduled dates, unclear ones trigger a Slack alert for human review
- **Analytics:** Every event is logged to PostgreSQL. The run closes with aggregated stats (by score tier, channel, and status), per-lead cost estimates, an AI-written human summary, and a Slack notification to the team

## Why it matters

This is the full outbound machine in one workflow — raw list to booked meeting, with scoring so effort concentrates on the best leads, compliance and rate-limit guardrails, and analytics that show exactly what each run produced.

## File

- `b2b-lead-management-ai-outreach.json` — n8n workflow, 113 nodes

## Requirements

- n8n instance
- OpenAI API key
- PostgreSQL database (lead store, reply handling, analytics)
- Slack workspace (alerts + run summary)
- Enrichment API of your choice (the included enrichment endpoints are test placeholders)
- Gmail (for sending; connect a Gmail trigger for live reply handling)

## Setup

1. Import `b2b-lead-management-ai-outreach.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_CREDENTIAL_ID`, enrichment endpoints, PostgreSQL connection) with your own credentials
3. Swap the test dataset for your real lead source (CSV, Google Sheets, or webhook)
4. Connect real enrichment APIs and a Gmail trigger for production use

## Note

Sanitized for public sharing — credentials, API endpoints, and database details have been replaced with placeholders. The enrichment endpoints and reply simulator are test placeholders; connect real enrichment APIs and a Gmail trigger for production.
