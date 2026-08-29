---
name: page-to-table-scrape
description: >-
  Turn a public or already-signed-in web page into a CSV or Markdown table with
  source URL and scrape time. Use when the user wants structured rows from a
  directory, list, or dashboard they can already see. Stop if login is missing;
  never bypass auth or scrape credentials.
---

# Page to table scrape

Extract a clean table from a page the Bot can already open. Honest about source and time. No credential workarounds.

## When to use

- User points at a URL or open page and wants rows in CSV or Markdown
- Directory, search results, pricing table, or dashboard list needs exporting
- User says "scrape this into a sheet" for a page they can access

## Required inputs and access

**Inputs (required)**
- Target page: URL, or clear pointer to a tab/window already open on the Bot computer
- Desired columns if known; otherwise infer from visible headers
- Output shape: CSV and/or Markdown table

**Access**
- Browser / computer use for the page
- Use an existing signed-in session if the site needs auth
- Never ask the user to paste passwords into chat; hand the desktop for login if needed

If the page requires login and no session exists, stop and ask the user to sign in on the Bot computer. Do not bypass paywalls, CAPTCHAs via shady means, or scrape behind stolen cookies.

## Steps

1. Open the page (or confirm the open tab). Record final URL after redirects.
2. If blocked by login, captcha, or hard paywall, stop and report. Do not invent rows.
3. Identify the repeating list/table. Prefer visible structure over guessing hidden APIs.
4. Extract rows into the agreed columns. Keep cell text faithful; do not "clean up" meaning.
5. Add metadata: source URL, scrape timestamp (user's timezone if known), row count.
6. Return CSV and/or Markdown. Offer a file on the Bot computer when the table is large.
7. Do not post the table anywhere, email it, or overwrite a production sheet without approval.

## How to validate

- Every row came from the page; no hallucinated companies, prices, or emails
- Source URL and scrape time are present
- Login failures are reported, not papered over with sample data
- Row count matches what was visibly extracted

## Always ask for approval when

- Writing into an existing spreadsheet, CRM, or database
- Emailing or publishing the exported file
- Running a large multi-page crawl beyond the single page the user named
- Using any credential or session the user did not already establish on the Bot

## Expected output

**Table export**
- Source URL:
- Scraped at:
- Rows:
- Columns:
- CSV or Markdown table
- Notes: login used? truncated? pagination stopped at page 1?
