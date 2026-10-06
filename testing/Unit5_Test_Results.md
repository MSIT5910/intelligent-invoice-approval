# Unit 5 Component Test Results

All tests used synthetic data.

| Test ID | Component Tested | Scenario | Expected Result | Actual Result | Result |
|---|---|---|---|---|---|
| M01 | Message/attachment validation | Incoming email contained no attachments | Detect missing attachments and execute the no-attachment exception path | No-attachment exception path executed as expected | Pass |
| M02 | PDF/invoice identification and normal processing | Email contained a valid PDF invoice with all four required fields | Invoice passes Layers 1 and 2, reaches `READY_FOR_REVIEW`, draft is created, and original email moves to `InvoiceProcessed` | Flow completed successfully through the expected path, created the draft, and moved the original message to `InvoiceProcessed` | Pass |
| M03 | Attachment/PDF filtering | Email contained mixed attachment types, including a non-PDF/TXT attachment and valid PDF invoice | Ignore non-PDF attachment and process the valid PDF | Non-PDF attachment was ignored and valid PDF invoice was successfully processed | Pass |
| M04 | First qualifying invoice selection | Email contained multiple PDF invoices | Process only the first qualifying invoice and prevent later PDFs from replacing it | First qualifying invoice was selected and processed; later PDFs did not replace it | Pass |
| M05 | Invoice identification and Layer 1 exception handling | Attachments were present but no qualifying PDF invoice was identified | No invoice selected; execute `EXCEPTION_NO_PDF_INVOICE` and `NotProcessed` path | No qualifying invoice was selected and the implemented no-invoice exception path executed | Pass |
| I01 | Required invoice-field validation | Synthetic invoice contained Vendor Name, Invoice ID, and Invoice Total but no Invoice Date | Required-field condition evaluates False and missing-required-field exception path executes | False branch executed; normal review actions were skipped and missing-required-field exception handling executed | Pass |

## Defect Identified and Corrected
During exception testing, an invoice with a missing Invoice Date initially passed Layer 2 validation and continued into draft creation with a blank Invoice Date.

**Cause:** The four required fields were initially configured using `is not equal to [blank]`, which did not reliably identify the missing Invoice Date output as empty.

**Correction:** Each required field check was changed to use `empty(field) = false`, with all four checks remaining in the existing AND condition.

**Retest Result:** The same synthetic invoice was rerun with Invoice Date omitted. The corrected condition evaluated False, skipped the `InvoiceFound` / `READY_FOR_REVIEW` path, and executed the missing-required-field exception handling as intended.
