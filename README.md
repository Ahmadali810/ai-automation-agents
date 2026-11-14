# AI Automation Agents

A collection of production n8n workflows and voice AI agents built for real client use cases — lead response, CRM automation, RAG-powered chat/voice agents, and content automation. Built by **Ahmad**, an AI automation specialist building custom automation systems for service-based and e-commerce businesses.

All workflows below are sanitized for public sharing — credentials, sheet IDs, client contact numbers, and webhook URLs have been replaced with placeholders. Import into your own [n8n](https://n8n.io) instance and connect your own credentials to run them.

Each project lives in its own folder with its workflow file and a dedicated README explaining what it does, how it works, and how to set it up.

---

## Workflows

| # | Project | What it does |
|---|---|---|
| 1 | [Roofing Lead Response CRM](./roofing-lead-response-crm/) | End-to-end lead intake, AI qualification, and email replies for a local service business, with Google Sheets as a lightweight CRM. |
| 2 | [RAG Voice Agent](./rag-voice-agent/) | Vapi-powered phone AI agent that answers calls, filters spam, qualifies leads, and books appointments by voice. |
| 3 | [WhatsApp RAG Agent — Sage Leather](./whatsapp-rag-agent-sage-leather/) | WhatsApp AI sales/support agent with RAG over a live product catalog; understands text, voice notes, and images. |
| 4 | [Lead Scraper & Enrichment](./lead-scraper-enrichment/) | Turns a form request into an enriched, deduplicated prospect list with verified emails, ready for a CRM sheet. |
| 5 | [Email Follow-up Automation](./email-followup-automation/) | Multi-region cold email follow-up sequences with reply handling, sent in batches on schedule. |
| 6 | [LinkedIn Auto Poster](./linkedin-auto-poster/) | Automated LinkedIn content pipeline — researches a topic, writes the post, generates an image, and publishes. |
| 7 | [B2B Lead Management & AI Outreach](./b2b-lead-management-ai-outreach/) | Full automated B2B SDR pipeline — validation, enrichment, scoring, AI cold emails, multichannel touchpoints, reply classification, and analytics. |
| 8 | [Appointment Booking & WhatsApp Reminders](./appointment-booking-whatsapp-reminders/) | WhatsApp appointment reminders for a clinic, with patient self-serve confirm / cancel / reschedule. |
| 9 | [Salary & Payroll Automation](./salary-payroll-automation/) | Monthly payroll from Sheets attendance — deductions calculated, PDF report generated and emailed to the manager. |

---

## Stack

| Layer | Tools |
|---|---|
| Orchestration | n8n |
| LLMs | GPT-4o, GPT-4o-mini, GPT-4.1, Google Gemini |
| Voice | Vapi, Deepgram, AssemblyAI |
| Vector DB / RAG | Pinecone, OpenAI Embeddings |
| Data layer | Google Sheets, PostgreSQL |
| Channels | WhatsApp (Twilio), Gmail, LinkedIn, Webhooks, Slack |
| Scraping / enrichment | Apify, Tavily |

## Setup

1. Open a project's folder and read its README for the exact requirements
2. Import its `.json` file into your n8n instance (`Workflows → Import from File`)
3. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, etc.) with your own credentials and sheet IDs
4. Set up the corresponding Google Sheets with matching column headers where referenced
5. For the voice agent, import the JSON config into a [Vapi](https://vapi.ai) assistant and connect your own phone number and webhook

## Also Available

Alongside these automation workflows, I also set up and manage a lightweight CRM (Google Sheets-based, expandable to full CRM platforms) for tracking leads, follow-ups, and appointment status — built to work directly with the workflows above.

## Contact

Built by Ahmad — open to freelance/contract AI automation work.
Email: vornexia4@gmail.com
