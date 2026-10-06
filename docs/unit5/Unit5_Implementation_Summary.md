# Unit 5 Implementation Summary

## Trigger
The flow begins when a new email arrives in the designated invoice mailbox.

## Major Processing Stages
1. Receive incoming email.
2. Initialize processing variables and status information.
3. Check whether the email contains attachments.
4. Process attachments sequentially.
5. Ignore non-PDF attachments.
6. Evaluate eligible PDFs using AI Builder Process Invoice.
7. Select only the first qualifying invoice.
8. Validate the four required invoice components.
9. Route successful invoices to the review/draft path or incomplete/invalid inputs to the applicable exception path.
10. Construct the review draft and route the original email to its final mailbox folder.

## Layer 1: Message and Attachment Validation
- Emails without attachments follow the no-attachment exception path.
- Non-PDF attachments are ignored.
- Eligible PDFs are evaluated to determine whether they represent an invoice.
- Once the first qualifying invoice is identified, later attachments do not replace it.
- Messages with no qualifying PDF invoice follow the `EXCEPTION_NO_PDF_INVOICE` / `NotProcessed` path.

## Layer 2: Required Invoice Fields
The MVP validates only the presence of these four fields:
1. Vendor Name
2. Invoice ID
3. Invoice Date
4. Invoice Total

The four checks use an AND relationship. No additional invoice validation is included in the Unit 5 MVP.

## Successful Outcome
When all four required invoice fields are present, the flow sets the process status to `READY_FOR_REVIEW`.

For a successfully validated invoice, the flow prepares a forwarded draft for human review, preserves the original message and attachments, updates the subject/body with extracted invoice information, and adds a renamed copy of the selected invoice PDF. The original email is then moved to `InvoiceProcessed`.

## Exception Outcome
When one or more required invoice fields are missing, the normal review path is skipped and the missing-required-field exception path executes. The implemented exception reason is:

`One or more required invoice fields are missing.`

Messages that do not satisfy the implemented processing rules are routed to `NotProcessed`.

## Current MVP Limitations
- Presence-only validation for the four required fields
- No mathematical invoice reconciliation
- No amount reasonableness/range checks
- Invoice Date checked for presence only
- No AI Builder confidence-threshold evaluation
- No duplicate or anomaly detection
- No accounting-code validation
- Only the first qualifying invoice is processed
- No autonomous approval, payment authorization, or downstream financial-system integration
