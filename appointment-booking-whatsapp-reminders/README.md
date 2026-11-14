# Appointment Booking & WhatsApp Reminders

WhatsApp-based appointment management for a clinic — sends 24-hour reminders with confirm/cancel/reschedule options, and handles patient replies automatically.

## What it does

Patients get a WhatsApp reminder a day before their appointment, and can confirm, cancel, or reschedule by just replying — no receptionist involved.

## How it works

- **Reminders:** A daily 9 AM schedule trigger reads today's and tomorrow's appointments from Google Sheets, filters to confirmed/pending ones, and sends each patient a personalised WhatsApp reminder with reply options
- **Reply routing:** A WhatsApp trigger catches replies and a `Switch` routes by keyword — `confirm` marks the appointment confirmed in Sheets and updates Google Calendar; `cancel` marks it cancelled, removes the calendar event, and notifies the admin; `reschedule` shows a numbered list of available slots; `myappointment` sends a full booking-details card
- **Rescheduling:** The patient replies `slot 2`, the workflow validates the pick against a saved session, updates Sheets, sends the new confirmation, and notifies the admin
- **Admin loop:** Every cancel or reschedule sends a summary straight to the admin's WhatsApp, so nothing happens silently

## Why it matters

No-shows are pure lost revenue for clinics. This closes the loop — reminders go out automatically, patients self-serve confirm/cancel/reschedule on WhatsApp, and the calendar stays in sync without receptionist effort.

## File

- `appointment-booking-whatsapp-reminders.json` — n8n workflow, 31 nodes

## Requirements

- n8n instance
- WhatsApp (Twilio)
- Google Sheets (appointments)
- Google Calendar

## Setup

1. Import `appointment-booking-whatsapp-reminders.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`) with your own credentials and sheet IDs
3. Set up the appointments sheet with matching column headers
4. Adjust the reminder schedule trigger if you want a different time than 9 AM

## Note

Sanitized for public sharing — credentials, sheet IDs, and phone numbers have been replaced with placeholders.
