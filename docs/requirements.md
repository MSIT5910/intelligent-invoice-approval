# System Requirements

## Functional Requirements

- **FR-01:** The system shall detect an invoice received in the designated Exchange/Outlook test mailbox and retrieve the attached invoice document.
- **FR-02:** The system shall process the invoice document using Power Automate and Copilot to extract required invoice information into a structured format.
- **FR-03:** The system shall identify whether required invoice information is present before the transaction proceeds through the normal workflow.
- **FR-04:** The system shall create or populate an ESM invoice record using the structured invoice information.
- **FR-05:** The system shall present invoice information to an authorized human reviewer and allow extracted information to be reviewed and corrected.
- **FR-06:** The system shall allow the human reviewer to provide or confirm accounting coding and justification.
- **FR-07:** The system shall capture an authorized human approval or rejection decision.
- **FR-08:** The system shall maintain the status of the invoice throughout the approval workflow.
- **FR-09:** The system shall identify an approved transaction as ready for Purchasing only after required information and approval are complete.

## Nonfunctional Requirements

- **NFR-01 - Usability:** The workflow should minimize unnecessary manual data entry and make extracted information easy to review and correct.
- **NFR-02 - Reliability:** Failure to extract required invoice information should result in an identifiable exception rather than silently continuing through the normal workflow.
- **NFR-03 - Security:** Access to invoice information, workflow records, and approval functions shall be limited to authorized users using platform access controls.
- **NFR-04 - Integrity:** AI-extracted information shall remain subject to human review and correction, and financial approval shall remain an authorized human action.
- **NFR-05 - Traceability:** The workflow should preserve sufficient status and decision information to determine how an invoice progressed through the prototype.
- **NFR-06 - Maintainability and Modularity:** Intake, intelligent processing, and workflow functions should remain sufficiently separated so one component can be modified or enhanced without redesigning the complete solution.
- **NFR-07 - Performance:** Under normal prototype conditions, automated intake and extraction should complete without unreasonable delay. A specific threshold will be established after an initial processing baseline is measured.

Minimum Extracted Invoice Fields

Vendor name
Invoice number
Invoice date
Invoice amount
Description/purpose
Due date, when present