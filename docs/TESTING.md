# Testing evidence and remaining checks

The statements below come from the project's 1.1.0 delivery and test records. They describe the tests documented there; this public repository does not contain the commercial test suite, raw databases, installer, or customer data.

| Check | Recorded result | Limit |
| --- | --- | --- |
| TypeScript/Vite build | Passed for version 1.1.0. | A build does not prove customer-machine behavior. |
| Automated suite | 26 tests passed, zero failures. | Local suite only; no claim of complete coverage. |
| Quotations and output | Disposable-profile QA covered calculations, discounts, quick-customer flow, short and 42-item A4 PDFs; the print dialog opened and was cancelled. | No physical customer printer test. |
| Layout | Six real Electron window widths (720–1920 px) at 100%, 115%, and 130% scale were reviewed. | These are recorded local observations, not a guarantee for every display. |
| Local storage | A disposable copy of a prior database passed integrity and record-count checks after opening with 1.1.0. | The normal customer installation and real license were untouched. |
| Packaged runtime | The 1.1.0 packaged executable started without a development server in a disposable profile and displayed activation without a license. | The installer was not run on the customer computer in the recorded final check. |
| Package audit | Extracted package contents matched the expected runtime set; private issuer, private key, test license, database, and backups were not found. | This is an inventory audit, not a third-party penetration test. |

## Pending customer-site acceptance

- Run the 1.1.0 NSIS installer and verify shortcuts on the customer's computer.
- Verify an upgrade from the normal 1.0.0 installation while retaining real records and license state.
- Activate with a production license issued by the owner and verify the complete workflow.
- Test a physical printer, paper output, margins, logo, and totals.
- Complete native file-dialog workflows in the final installed build where the record lists them as pending.
- Confirm operation with Windows network connectivity physically disabled.

The installer is **unsigned** (`NotSigned` in the recorded Authenticode check). These pending items are not counted as passed tests. Version 1.1.0 is described as completed and packaged for **controlled delivery**, with customer-site acceptance outstanding.
