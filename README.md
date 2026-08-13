# AI Automation Agents

A collection of production n8n workflows and voice AI agents built for real client use cases — lead response, CRM automation, RAG-powered chat/voice agents, and content automation. Built by **Ahmad**, an AI automation specialist building custom automation systems for service-based and e-commerce businesses.

All workflows below are sanitized for public sharing — credentials, sheet IDs, client contact numbers, and webhook URLs have been replaced with placeholders. Import into your own [n8n](https://n8n.io) instance and connect your own credentials to run them.

---

## Workflows

### 1. `roofing-lead-response-crm.json`
**What it does:** End-to-end lead intake and response system for a local service business. Captures leads from a website chatbot and a contact/appointment form, checks whether the contact is a new lead, an old lead requesting a new service, or an existing customer, then routes each case through the right AI-driven response.

**How it works:**
- Two webhooks receive events: one from a website chatbot widget, one from an appointment/contact form
- A `Switch` node routes the payload based on source and intent
- An AI Agent (GPT-4o via OpenAI, with conversation memory) reads the incoming message and the lead's history in Google Sheets to decide how to respond
- New leads get logged to a "New Leads" sheet; returning leads requesting a different service get logged separately ("Old lead but New Service") so nothing is missed
- A second AI Agent drafts and sends a personalized email reply via Gmail, and a third layer handles inbound Gmail replies (Gmail Trigger) so the conversation continues automatically
- All lead data — status, service requested, timestamps — is written back to Google Sheets, functioning as a lightweight CRM

**Why it matters:** Service businesses lose leads when nobody responds fast enough. This closes that gap — lead comes in, gets qualified and answered within seconds, and is tracked without a human touching a spreadsheet.

---

### 2. `rag-voice-agent.json`
**What it does:** A Vapi-powered phone AI agent ("Nate") that answers inbound calls for a local service business — handles customer questions, filters spam/robocalls, qualifies leads, and books appointments, all by voice.

**How it works:**
- Runs on Vapi with GPT-4.1 as the reasoning model and Deepgram (with AssemblyAI fallback) for transcription
- The system prompt defines a strict call flow: spam detection first → greeting → check for an existing appointment → lead qualification (name, address, phone, issue/request, urgency) → read back a summary → confirm → book
- Answers general questions using a connected knowledge base (company services, pricing approach, service area) instead of guessing facts
- Escalates urgent cases by skipping straight to essential details and prioritizing speed
- Sends call data to an n8n webhook at the end of each call for logging/follow-up automation

**Why it matters:** Most missed calls become missed jobs. This agent never misses a call, never forgets to ask a qualifying question, and never double-books.

---

### 3. `whatsapp-rag-agent-sage-leather.json`
**What it does:** A WhatsApp AI sales/support agent with Retrieval-Augmented Generation (RAG) — built for an e-commerce leather goods brand. Understands text, voice notes, and images, and answers using the brand's actual product catalog.

**How it works:**
- **Knowledge ingestion pipeline:** A Google Drive trigger watches for new product/catalog files, splits them into chunks (Recursive Character Text Splitter), generates embeddings (OpenAI), and stores them in a Pinecone vector index
- A second pipeline scrapes the brand's product sitemap on a schedule (HTTP Request + HTML parsing) to keep pricing and product data fresh in the vector store
- **Conversation pipeline:** WhatsApp Trigger receives messages. A `Switch` node detects message type:
  - **Text** → goes straight to the AI Agent
  - **Voice note** → downloaded and transcribed (Google Gemini) before being passed to the AI Agent
  - **Image** → downloaded and analyzed (Gemini Vision) so the agent can respond to product photos
- The AI Agent (GPT-4o + conversation memory) retrieves relevant product info from Pinecone (RAG) to answer questions accurately instead of hallucinating prices or specs
- Replies are sent back via WhatsApp, and conversation data is logged to Google Sheets

**Why it matters:** This is the most technically complete piece in the repo — multi-modal input (text/voice/image), real RAG over live product data, and automatic knowledge refresh. It shows the full stack: ingestion, embeddings, vector search, and generation.

---

### 4. `lead-scraper-enrichment.json`
**What it does:** Takes a form submission (e.g. "find me business leads matching X criteria") and turns it into an enriched, deduplicated list of prospects with verified emails, ready to load into a CRM sheet.

**How it works:**
- Triggered by an n8n form submission
- Uses an Apify actor to scrape business listings/search results for the given criteria
- Runs the results through cleaning steps (JavaScript code nodes) to parse and normalize the raw SERP/scrape data
- Attempts to extract or find an email for each business; leads with a found email go to a "Data complete" sheet, leads without go to separate "Without mail" sheets for manual follow-up
- Deduplicates records before writing to Google Sheets, so the same business never gets contacted twice

**Why it matters:** This is the top of the outreach funnel — it's what feeds the cold email and CRM systems with fresh, clean prospect data instead of manually researching each lead.

---

### 5. `email-followup-automation.json`
**What it does:** Automates a multi-region cold email follow-up sequence (configurable per target market/region) with reply handling.

**How it works:**
- A scheduled trigger pulls leads from region-specific Google Sheets (one sheet per target market)
- A `Switch` node routes each lead down the correct regional path
- Loops through leads in batches, sends a follow-up email via Gmail, and waits a set interval before the next batch — avoiding spam-trigger sending patterns
- A separate branch handles a manual trigger for one-off follow-ups and processes inbound Gmail replies, so responses to a cold email get picked up automatically rather than sitting in an inbox

**Why it matters:** This is the engine behind the daily 25-30 cold emails — it keeps the follow-up sequence running on schedule without manual sending, across multiple markets at once.

---

### 6. `linkedin-auto-poster.json`
**What it does:** Fully automated LinkedIn content pipeline — picks a topic, researches it, writes a post, generates a matching image, and publishes it.

**How it works:**
- Scheduled trigger pulls the next topic/title from a content calendar in Google Sheets
- Tavily web search pulls current, relevant information on that topic
- An AI Agent (GPT-4o-mini, with memory) synthesizes the research into a high-level, professional LinkedIn post
- A second AI Agent turns that post into an image generation prompt
- OpenAI's image model generates a matching visual
- The post and image are published directly to LinkedIn via the LinkedIn node

**Why it matters:** Keeps a consistent LinkedIn content cadence (educational / case study / personal posts) running without manually writing and designing every post.

---

## Stack

| Layer | Tools |
|---|---|
| Orchestration | n8n |
| LLMs | GPT-4o, GPT-4o-mini, GPT-4.1, Google Gemini |
| Voice | Vapi, Deepgram, AssemblyAI |
| Vector DB / RAG | Pinecone, OpenAI Embeddings |
| Data layer | Google Sheets |
| Channels | WhatsApp (Twilio), Gmail, LinkedIn, Webhooks |
| Scraping / enrichment | Apify, Tavily |

## Setup

1. Import any `.json` file into your n8n instance (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, etc.) with your own credentials and sheet IDs
3. Set up the corresponding Google Sheets with matching column headers where referenced
4. For the voice agent, import the JSON config into a [Vapi](https://vapi.ai) assistant and connect your own phone number and webhook

## Also Available

Alongside these automation workflows, I also set up and manage a lightweight CRM (Google Sheets-based, expandable to full CRM platforms) for tracking leads, follow-ups, and appointment status — built to work directly with the workflows above.

## Contact

Built by Ahmad — open to freelance/contract AI automation work.
Email: vornexia4@gmail.com
