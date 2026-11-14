# Salary & Payroll Automation

End-to-end monthly payroll automation — reads employee registration and attendance from Google Sheets, calculates deductions and net salary per employee, generates a formatted PDF report, and emails it to the manager.

## What it does

Attendance in, reviewed PDF in the manager's inbox — monthly payroll without the spreadsheet grind.

## How it works

- A monthly schedule trigger pulls employee registration data and attendance records, looping through employees in batches
- An attendance calculator counts Present/Absent/Half-day/Leave/Holiday days per employee and totals working hours from time-in/time-out (handling midnight crossovers)
- A salary engine applies the deduction rules (per-day salary on a 30-day base; leave, absent, and half-days deducted) and writes each employee's payroll row back to the Payroll sheet
- A second branch converts the payroll data into a styled HTML report, converts it to PDF via an API, and emails the PDF to the manager via Gmail

## Why it matters

Payroll is the most error-sensitive recurring ops task in any company. This turns a manual spreadsheet grind into a scheduled pipeline — attendance in, reviewed PDF in the manager's inbox, with every deduction traceable to its source rows.

## File

- `salary-payroll-automation.json` — n8n workflow, 11 nodes

## Requirements

- n8n instance
- Google Sheets (employee registration, attendance, payroll)
- Gmail account
- PDF conversion API

## Setup

1. Import `salary-payroll-automation.json` into n8n (`Workflows → Import from File`)
2. Replace placeholder values (`YOUR_GOOGLE_SHEET_ID_*`, `YOUR_CREDENTIAL_ID`, PDF API details) with your own credentials and sheet IDs
3. Set up the registration, attendance, and payroll sheets with matching column headers
4. Set the monthly schedule trigger to your payroll date

## Note

Sanitized for public sharing — credentials, sheet IDs, and email addresses have been replaced with placeholders.
