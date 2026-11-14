# LinkedIn Auto Poster

Fully automated LinkedIn content pipeline — picks a topic, researches it, writes a post, generates a matching image, and publishes it.

## What it does

Turns a content calendar into published LinkedIn posts with matching visuals, on autopilot.

## How it works

- Scheduled trigger pulls the next topic/title from a content calendar in Google Sheets
- Tavily web search pulls current, relevant information on that topic
- An AI Agent (GPT-4o-mini, with memory) synthesizes the research into a high-level, professional LinkedIn post
- A second AI Agent turns that post into an image generation prompt
- OpenAI's image model generates a matching visual
- The post and image are published directly to LinkedIn via the LinkedIn node

## Why it matters

Keeps a consistent LinkedIn content cadence (educational / case study / personal posts) running without manually writing and designing every post.

## File

- `linkedin-auto-poster.json` — n8n workflow, 9 nodes

## Requirements

- n8n instance
- OpenAI API key (GPT-4o-mini + image generation)
- Tavily API key (web search)
- Google Sheets (content calendar)
- LinkedIn account connected to n8n

## Setup

1. Import `linkedin-auto-poster.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, Tavily API key) with your own credentials
3. Fill the content calendar sheet with topics and titles
4. Set the schedule trigger to your posting cadence

## Note

Sanitized for public sharing — credentials, sheet IDs, and API keys have been replaced with placeholders.
