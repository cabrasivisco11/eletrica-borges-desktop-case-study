# Technical case study

## Objective and scope

The project delivers a Windows x64 quotation application for a local electrical-services business. Version 1.1.0 was built, tested in controlled local environments, and packaged for commercial delivery. The published evidence supports a completed software and installer scope, while customer-site acceptance remains open.

The workflow covers customer and catalog records, composing quotations with fractional quantities and discounts, PDF/print output, record history, backup, and offline licensing. The application stores business records locally rather than depending on a hosted service.

## Challenges and decisions

### 1. Keep quotations and output consistent

The editor and its financial summary must agree on services, materials, quantities, discounts, and totals. PDF and printing use the same quotation content rather than a separate manual document. Local QA checked a short A4 PDF and a 42-item quotation that paginated to two A4 pages. The Windows print dialog opened and was cancelled during testing; no customer printer job was sent.

### 2. Protect commercial data during development

Electron's installed application and the SQLite database have different lifecycles. The database resides in the user's application-data area; the uninstall configuration preserves it. Development and QA used marked disposable profiles, temporary licenses, and test databases. Backup/restore validation and a recovery copy were part of the implementation. A disposable copy of a version 1.0.0 database passed `integrity_check` and retained its recorded counts when opened with 1.1.0. That is compatibility evidence for the copied data, not a completed upgrade on the customer's PC.

### 3. Enforce offline licensing at the correct boundary

The permanent device-bound license is signed with Ed25519. The packaged application contains a public verification key, while the private issuer and signing material remain outside distribution. Writes are checked in the main process, so an unlicensed renderer cannot bypass the restriction through a normal UI path. Local tests covered signature rejection and blocked writes with temporary or invalid licenses. Activation with a real production license on the customer computer has not been completed in the documented checks.

### 4. Make a dense business UI usable at different sizes

The application offers 100%, 115%, and 130% interface scales. The 1.1.0 work added a narrow-window menu, local scrolling for wide tables, and a quick-customer dialog that preserves the quotation draft when opened or cancelled. A CSS specificity issue hid inactive menu labels in reduced windows; the team reproduced and corrected it. Manual QA traversed six window widths, from 720 to 1920 pixels, at all three scales. Two observations made during asynchronous loading were checked again after rendering and passed.

### 5. Package without private operational material

The Windows installer was generated with NSIS. A documented package audit compared the extracted `app.asar` with the unpacked application and found the expected commercial runtime files. The audit did not find the administrative issuer, private key, test licenses, databases, or backups in the package. This repository goes further by publishing only narrative documentation and three selected QA captures; it does not provide the installer or application source.

## Result and evidence boundary

The 1.1.0 build, 26 automated tests, local UI scenarios, installer generation, package audit, and initial packaged-executable launch are documented as passed. Customer-PC installation, production-license activation, a real upgrade preserving the installed data and license, physical printing, and a physically disconnected network test remain pending. The unsigned installer is a distribution limitation. See [Testing and limitations](TESTING.md) for the exact split.

## AI and attribution

Codex assisted with reviewing the available project evidence and drafting this public case study. The private implementation is not published here, and this document does not claim that every line was authored manually or identify unsupported individual code contributions. The project owner's approval of product behavior and the recorded tests are distinct from AI assistance.
