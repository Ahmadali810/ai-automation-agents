# Vapi Voice Agent Configuration

Vapi assistant configuration for a roofing-service phone assistant with knowledge-base guidance and appointment qualification.

## Overview

This folder contains a Vapi assistant configuration JSON, not an n8n workflow export.

## Included capabilities

- Natural-language phone greeting and call flow
- Knowledge-base-grounded company answers
- Lead qualification and caller-confirmed booking flow
- Spam/irrelevant-call handling instructions

## Setup

1. Review this README and the exported JSON before importing.
2. Import the JSON into a compatible n8n instance / Vapi assistant configuration.
3. Replace all `YOUR_*` placeholders and reconnect credentials in your own environment.
4. Confirm provider node versions, API permissions, data schema, webhook URLs and timezone.
5. Keep the workflow inactive until the validation tests pass.

## Limitations and production checklist

- This is a Vapi assistant configuration, not an n8n workflow.
- Referenced tool IDs and knowledge-base file IDs are external resources not included here.
- Configure a production n8n webhook; the former webhook-test URL is replaced with a placeholder.
- Booking cannot be verified from this assistant JSON alone; include connected tool/backend evidence.

## Suggested validation tests

- [ ] Knowledge-base answer and unknown-answer fallback
- [ ] Existing appointment check before creating a new one
- [ ] Booking requires explicit caller confirmation
- [ ] Webhook/tool timeout and call-end report

## Security

- Never commit API keys, OAuth tokens, private webhook URLs, phone numbers or customer data.
- Use least-privilege credentials and provider-side rate limits.
- Configure authentication and request validation on public webhooks.
- Test with synthetic records before connecting live customers.

## Verification status

This repository update includes static JSON/configuration and documentation cleanup. It does **not** mean the workflow has been executed end-to-end. Mark a test as passed only after observing the actual execution in your own connected environment.

## Files

- `rag-voice-agent.json` — workflow/configuration export

