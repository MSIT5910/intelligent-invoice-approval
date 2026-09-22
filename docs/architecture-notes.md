# Architecture Notes

## Module Specifications

### 1. Exchange / Outlook Invoice Intake

**Input:** Email containing an invoice PDF attachment.

**Processing:** A designated test mailbox receives the invoice and makes the message and attachment available to the automated workflow.

**Output:** Invoice PDF and associated email information.

### 2. Power Automate + Copilot Processing

**Input:** Invoice PDF and available email information.

**Processing:** Power Automate retrieves the attachment and uses a Copilot prompt to extract and normalize required invoice information. Required information is checked before the transaction proceeds.

**Output:** Structured invoice data or an identified exception requiring review.

### 3. ESM Approval Workflow

**Input:** Structured invoice information.

**Processing:** The ESM creates and maintains the invoice record, routes it for human review, and captures corrections, accounting coding, justification, approval or rejection, and workflow status.

**Output:** Completed invoice record and approval decision. Approved and complete transactions become ready for Purchasing.

## External Actors

### Human Approver
Reviews and corrects extracted information, provides or confirms coding and justification, and approves or rejects the transaction.

### Purchasing
Receives the completed transaction after the approval workflow is successfully completed.

## Design Principle

The architecture separates intake, intelligent automation, and workflow management so individual components can be enhanced or replaced independently as the solution evolves.
