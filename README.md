# Chain of Custody Documentation System for Digital Evidence
 
A browser-based tool for logging digital evidence, tracking custody hand-offs, and cryptographically verifying that neither the evidence file nor the custody log itself has been tampered with.
 
**Course:** CY376 — Network Security Auditing and Monitoring
**Track:** Blue Team
**Name:** Amy Ama Beduwa Engison
**Index Number:** FCM.41.018.130.23
**Institution:** University of Mines and Technology (UMaT), Tarkwa
 
## Overview
 
When responding to a security incident, a defender needs to prove — not just claim — that evidence (a disk image, log file, or device) was handled correctly and stayed unaltered from collection to analysis. This project implements that proof digitally:
 
- Every evidence item is logged with the metadata required by recognised forensic standards (case number, description, collector, timestamp, location).
- The evidence file itself is hashed with SHA-256 at the moment of collection, computed entirely in the browser.
- Every custody transfer can re-verify that hash against the original, flagging any mismatch permanently.
- Every custody log entry is cryptographically chained to the one before it, so editing a past entry — not just the evidence file — is independently detectable.
- Records can be exported/imported as JSON, and printed or saved as a clean PDF report.
The full reasoning behind these design decisions, the standards referenced (NIST SP 800-86, ISO/IEC 27037, ACPO, RFC 3227), and testing results are documented in the accompanying report (`Chain_of_Custody_Report_CY376.pdf`).
 
## Features
 
| Feature | Description |
|---|---|
| Evidence intake | Logs case number, description, evidence type, collector, timestamp, location, and notes |
| SHA-256 file hashing | Computed client-side via the browser's Web Crypto API — no file ever leaves the browser |
| Custody transfer log | Records every hand-off: from, to, timestamp, purpose |
| Hash re-verification | Re-upload a file at transfer time to confirm it still matches the original hash |
| Tamper-evident log chain | Each log entry is hashed together with the previous entry's hash, so editing history is detectable |
| Verify Log Integrity | Re-walks the entire chain and reports exactly where it breaks, if it does |
| Demo: Simulate Tampering | A built-in control that deliberately breaks the chain, for testing/demonstration purposes only |
| Investigator sign-in | Identifies the current user per session and auto-fills their name onto new records (identity tagging for usability — not password-protected authentication) |
| Export / Import | Download all evidence records as JSON, or reload them on another device |
| Print / Export Report | Produces a clean, printable custody report per evidence item |
 
## Tools and Technologies Used
 
- HTML5, CSS3, vanilla JavaScript (ES6+)
- Web Crypto API (`crypto.subtle.digest`) for SHA-256 hashing
- Browser `localStorage` for persistence (no server or database required)
## How to Run
 
This is a single self-contained HTML file — no installation, build step, or server required.
 
1. Download `Chain Of Custody Web App.html` from this repository.
2. Open it in any modern browser (Chrome, Edge, or Firefox) by double-clicking it, **or**
3. For full functionality (recommended), serve it locally, e.g. using the VS Code "Live Server" extension, then open it at `http://127.0.0.1:5500/`.
No account, API key, or internet connection is required after the page loads (aside from loading the Google Fonts used for styling).
 
## Repository Structure
 
```
├── Chain Of Custody Web App.html   # The complete application (HTML + CSS + JS)
├── CY376_Chain_of_Custody_Report.pdf   # Full project report
└── README.md
```
 
## Standards Referenced
 
- NIST SP 800-86 — Guide to Integrating Forensic Techniques into Incident Response
- ISO/IEC 27037:2012 — Guidelines for identification, collection, acquisition and preservation of digital evidence
- ACPO Good Practice Guide for Digital Evidence
- RFC 3227 — Guidelines for Evidence Collection and Archiving
- FIPS 180-4 — Secure Hash Standard (SHA-256)
## Limitations
 
This is a coursework-scoped, client-side tool. It does not include a backend, multi-user access control, or real authentication — the investigator sign-in screen identifies a user for convenience only and is explicitly not a security mechanism. These limitations, and recommended next steps, are discussed in full in the accompanying report.
 
## Author
 
Amy Ama Beduwa Engison — FCM.41.018.130.23
BSc Cybersecurity, University of Mines and Technology (UMaT), Tarkwa
