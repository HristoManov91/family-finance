# Decision log — family-finance

Date: 2026-10-29. Public documentation only: **NO real household data**.

**Status:** ACCEPTED — directly confirmed user behavior. PARTIAL — capability confirmed, precise semantics open. PROPOSED — technical/product suggestion. OPEN — awaiting interview. A new explicit user answer supersedes older wording.

| ID | Decision | Status | Outcome / question |
| --- | --- | --- | --- |
| D-001 | Repo | ACCEPTED | New public `HristoManov91/family-finance`. Old 2022–23 code is not an implementation base. Deletion of old repo is optional later, after transfer; no deletion was done. |
| D-002 | Browser & mobile | PARTIAL | Browser + Android and iPhone; installable experience desired. PWA vs native App Store/Google Play publication open. |
| D-003 | Hosting | OPEN | Hosted vs self-hosted, cloud provider, cost and backups. |
| D-004 | Users | PARTIAL | Multiple separate users with shared household workflows; login, member invites, roles open. |
| D-005 | Account names | ACCEPTED | User creates any number of financial accounts with any desired names. Types may include cash, cards, credit cards or other named accounts. |
| D-006 | Account attribution | ACCEPTED | **Only source/destination financial accounts matter financially. NO separate payer or beneficiary field.** Creator/editor can be audit metadata only. Supersedes earlier provisional payer idea. |
| D-007 | Opening balances | ACCEPTED | Define opening value on account creation, **not booked as income**. |
| D-008 | Income/expense | ACCEPTED | Choose account per transaction; expense decreases a positive asset balance, income increases it. Credit accounts require liability-specific behavior. |
| D-009 | Transfers | ACCEPTED | Transfer between accounts, not double counted as income or spending. |
| D-010 | Credit cards | PARTIAL | Support true credit card behavior; debt, limit, fees, payback, refunds and overpayment to clarify. |
| D-011 | Visibility | PARTIAL | User selects **which members may see each account**. View/edit/manage rights, transfer counterparties and aggregated reports open. |
| D-012 | Editing history | ACCEPTED | Editing/removing old transactions recalculates balances and reports. Exact voiding/audit rules open. |
| D-013 | Archiving | ACCEPTED | Account with history may be archived rather than destructively removed. Restore and transfer-before-archive rules open. |
| D-014 | Transaction name/description | ACCEPTED | Name and separate optional free-text note. |
| D-015 | Categories | PARTIAL | Required primary category on ordinary expense/income; optional subcategory, per-item override, custom categories and icons. |
| D-016 | Itemized expenses | PARTIAL | Transactions may contain one or many products; names, weight/quantity where available, categories and prices. Discounts/refunds/rounding rules open. |
| D-017 | Documents | PARTIAL | PDF/photo -> AI/OCR transaction draft with editable header and line items; human review is necessary. |
| D-018 | Budgets | PARTIAL | Monthly spending limit and/or income budgeting, periodic reports; calculation rules open. |
| D-019 | Historical data | ACCEPTED | Must import available existing Bluecoins history. New fields missing in historical transactions stay empty (do not invent). Import mapping and reconciliation open. |
| D-020 | Reporting/export | ACCEPTED | Filter by product/category/subcategory/transaction, period and account; export PDF, XLSX, CSV. Formats/authorization open. |
| D-021 | Passwordless auth | PARTIAL | Prefer modern no-password login, with recovery/authorization to decide. |
| D-022 | Stack | PROPOSED | Java 25, Spring Boot 4.1.x, PostgreSQL, Flyway, Nuxt 4, Vue 3, TypeScript, modular monolith; pin versions at development start. |
| D-023 | Implementation flow | ACCEPTED | Interview -> specs/ADRs -> epics and small issues -> Codex Draft PR -> independent review -> explicit merge. |
| D-024 | Currency | OPEN | EUR only or multi-currency/legacy BGN? FX and account currencies? |
| D-025 | Household reporting | OPEN | When some accounts are private, which aggregate totals, category reports and budgets are visible to other users? |
| D-026 | Sharing mutations | OPEN | Can account viewers add/edit transactions, change visibility or see private counterpart of transfers? |
| D-027 | Deleting transactions | OPEN | Physical delete vs logical void + audit and recovery. Resulting balance change ACCEPTED. |
| D-028 | Credit repayment | PROPOSED | Record credit-card repayment from another account as a transfer, NOT a second expense. |
| D-029 | Ledger correctness | PROPOSED | Model balanced journal/postings and derive balances rather than hand-patching cached balances, subject to architectural ADR. |

## Further decisions and change protocol
- Preserve a dated explicit owner decision with rationale, alternatives and consequences when moving from OPEN/PARTIAL to ACCEPTED.
- On change, update all affected specifications and parent issues together.
- No private family budget figures or financial sample exports should ever enter this public repository.
