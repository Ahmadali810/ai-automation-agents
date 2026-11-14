# WhatsApp RAG Agent — Sage Leather

A WhatsApp AI sales/support agent with Retrieval-Augmented Generation (RAG) — built for an e-commerce leather goods brand. Understands text, voice notes, and images, and answers using the brand's actual product catalog.

## Workflow

![Sage Leather WhatsApp RAG Agent workflow](./screenshot.png)

## What it does

Answers customer enquiries on WhatsApp from the live product catalog — text, voice notes, and product photos — instead of guessing prices or specs.

## How it works

- **Knowledge ingestion pipeline:** A Google Drive trigger watches for new product/catalog files, splits them into chunks (Recursive Character Text Splitter), generates embeddings (OpenAI), and stores them in a Pinecone vector index
- A second pipeline scrapes the brand's product sitemap on a schedule (HTTP Request + HTML parsing) to keep pricing and product data fresh in the vector store
- **Conversation pipeline:** WhatsApp Trigger receives messages. A `Switch` node detects message type:
  - **Text** → goes straight to the AI Agent
  - **Voice note** → downloaded and transcribed (Google Gemini) before being passed to the AI Agent
  - **Image** → downloaded and analyzed (Gemini Vision) so the agent can respond to product photos
- The AI Agent (GPT-4o + conversation memory) retrieves relevant product info from Pinecone (RAG) to answer questions accurately instead of hallucinating prices or specs
- Replies are sent back via WhatsApp, and conversation data is logged to Google Sheets

## Why it matters

This is the most technically complete piece in the repo — multi-modal input (text/voice/image), real RAG over live product data, and automatic knowledge refresh. It shows the full stack: ingestion, embeddings, vector search, and generation.

## File

- `whatsapp-rag-agent-sage-leather.json` — n8n workflow, 39 nodes

## Requirements

- n8n instance
- OpenAI API key (GPT-4o + embeddings)
- Pinecone vector index
- Google Gemini (voice transcription + image analysis)
- WhatsApp (Twilio) + Google Drive + Google Sheets

## Setup

1. Import `whatsapp-rag-agent-sage-leather.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, Pinecone index details) with your own credentials
3. Point the Drive trigger at your product catalog folder and the scraper at your product sitemap

## Note

Sanitized for public sharing — credentials, sheet IDs, client contact numbers, and webhook URLs have been replaced with placeholders.
