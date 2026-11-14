# RAG Voice Agent

A Vapi-powered phone AI agent ("Nate") that answers inbound calls for a local service business — handles customer questions, filters spam/robocalls, qualifies leads, and books appointments, all by voice.

## What it does

Answers inbound calls, qualifies the caller, and books appointments without a human picking up the phone.

## How it works

- Runs on Vapi with GPT-4.1 as the reasoning model and Deepgram (with AssemblyAI fallback) for transcription
- The system prompt defines a strict call flow: spam detection first → greeting → check for an existing appointment → lead qualification (name, address, phone, issue/request, urgency) → read back a summary → confirm → book
- Answers general questions using a connected knowledge base (company services, pricing approach, service area) instead of guessing facts
- Escalates urgent cases by skipping straight to essential details and prioritizing speed
- Sends call data to an n8n webhook at the end of each call for logging/follow-up automation

## Why it matters

Most missed calls become missed jobs. This agent never misses a call, never forgets to ask a qualifying question, and never double-books.

## File

- `rag-voice-agent.json` — Vapi assistant configuration (not an n8n workflow)

## Requirements

- Vapi account
- OpenAI API key (GPT-4.1)
- Deepgram (transcription) with AssemblyAI as fallback
- Phone number connected through Vapi
- n8n webhook to receive end-of-call data (optional, for logging)

## Setup

1. Import `rag-voice-agent.json` into a [Vapi](https://vapi.ai) assistant
2. Connect your own phone number and webhook
3. Replace placeholder values (knowledge base content, webhook URL) with your own

## Note

Sanitized for public sharing — credentials, phone numbers, and webhook URLs have been replaced with placeholders.
