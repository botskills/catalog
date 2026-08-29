---
name: invoice-spend-capture
description: >-
  From a receipt, invoice PDF, or billing email, extract vendor, amount, currency,
  due date, and a draft expense coding. Use when the user pastes a bill, forwards
  a receipt, or asks to log spend. Never pay, refund, or change billing without a
  fresh approval.
---

# Invoice / spend capture

Turn a receipt, invoice, or billing email into a clean spend record with draft coding. Draft only.

## When to use

- User pastes or attaches a receipt, invoice PDF, or billing email
- User asks to "log this charge", "capture this invoice", or "code this expense"
- A billing inbox message needs a structured summary before anyone pays

## Required inputs and access

**Inputs (required)**
- The source document: pasted text, image/PDF the Bot can read, or a single email body
- Optional: preferred chart of accounts / coding labels, home currency, tax note

**Access**
- None if the document is pasted or attached
- Email connector only when fetching a specific billing message the user named
- Never open a bank, Stripe, or card portal to pay

If there is no document and no named email to fetch, stop and ask. Do not invent a charge.

## Steps

1. Read the document carefully. Prefer printed totals over logos or marketing copy.
2. Extract: vendor, amount, currency, invoice/receipt number (if any), issue date, due date, line items if clear.
3. Flag uncertainty (blurry OCR, missing due date, multi-currency) instead of guessing.
4. Draft a short expense coding suggestion (category + memo) using the user's labels if provided; otherwise propose neutral categories and mark them as suggestions.
5. Output a single structured spend card ready for the user to approve or edit.
6. Stop. Do not pay, schedule payment, dispute, or message the vendor.

## How to validate

- Amount and vendor appear in the source; nothing invented
- Unclear fields are marked unknown, not filled with plausible guesses
- No payment, refund, subscription change, or portal login was attempted
- If OCR failed, say so and ask for a clearer paste

## Always ask for approval when

- Paying, scheduling payment, or initiating a refund
- Changing a subscription, card on file, or billing address
- Sending anything to the vendor or accounting team
- Writing to a finance system of record (QuickBooks, Ramp, etc.)

## Expected output

**Spend capture**
- Vendor:
- Amount / currency:
- Due date:
- Invoice #:
- Draft coding: category — memo
- Confidence / unknowns:
- Source: pasted | email subject | filename
