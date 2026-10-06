# Unit 5 Requirements-to-Test Coverage

| Implemented Logic | Actual Test Coverage |
|---|---|
| Message/attachment validation | M01, M03, M05 |
| PDF filtering | M03 |
| PDF/invoice identification | M02, M05 |
| First qualifying invoice behavior | M04 |
| Normal successful processing path | M02 |
| Vendor Name presence | M02 |
| Invoice ID presence | M02 |
| Invoice Date presence | M02, I01 |
| Invoice Total presence | M02 |
| All four required fields collectively present | M02 |
| Missing required-field exception | I01 |
| Layer 1 no-qualifying-invoice exception | M05 |
| `READY_FOR_REVIEW` status | M02 |
| Successful draft creation/output | M02 |
| Original successful email moved to `InvoiceProcessed` | M02 |

## Coverage Clarification
Individual missing-field tests were not performed separately for Vendor Name, Invoice ID, and Invoice Total. M02 demonstrated successful processing when all four required fields were present, while I01 specifically demonstrated exception handling when Invoice Date was absent. The implemented Layer 2 condition applies the same presence-check pattern to each of the four required fields.
