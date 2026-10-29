# Family Finance — Product Vision (Draft v0.1)

Status: **DISCOVERY / NOT READY FOR IMPLEMENTATION**  
Source: user discovery request, 2026-10-29. Parent: [Discovery Issue #6](https://github.com/HristoManov91/family-finance/issues/1).  
Repository choice is **confirmed**: `HristoManov91/family-finance` is the new public repository; the 2022–23 legacy application code will **not** be imported.

## Problem and outcome
Build a family expense and budgeting application that preserves the fast manual transaction experience of Bluecoins but supports shared household workflows and item-level purchase intelligence. It should work well both on phones and in a desktop browser.

## Confirmed user needs (requirements, not implementation decisions)
- R-001 Record expenses and income, with a configurable monthly spending limit and/or monthly income.
- R-002 Enter transactions manually with name, amount, date, selected source/destination financial account, required primary category where applicable, optional subcategory, optional free-text description, and optional merchant.
- R-003 A transaction may contain one or many items. Items have a name, amount/price, a category and optional subcategory; preserve quantity/weight when known.
- R-004 Attach a receipt/document, including a PDF or photo, and generate a **reviewable draft** transaction with extracted items.
- R-005 Edit the proposal before saving: transaction-level attributes and specific item rows can be corrected independently.
- R-006 Run configurable weekly, monthly, quarterly and other-period reports by transaction name, item/product, category, subcategory and other useful dimensions.
- R-007 Browser and mobile usage.
- R-008 Multiple independent users collaborate through selectively shared financial accounts. Each user can choose who may see an account. Spending is associated with the account used, **not with an additional payer or beneficiary field**.
- R-009 Add and manage user-defined categories and subcategories, and use expressive icons/images in the UI.
- R-010 Export data and reports to **PDF, native XLSX, and CSV**.
- R-011 Support modern passwordless authentication, browser use and an installable Android/iPhone experience (PWA/native packaging decision pending).
- R-012 Preserve historical Bluecoins transaction data even if new per-item fields do not exist; detail requirements through staged interviews and generate GitHub/Codex work only afterward.

## Candidate capabilities (NOT YET APPROVED)
Recurring bills; refunds and returns; quantities and price-per-unit; merchant normalization; receipt deduplication; budget carryover; saved reports and filters; migration from Bluecoins; offline entry and later sync; backups and recovery; optional chat-based ingestion; AI product-name normalization; time-based price comparisons.

## Confirmed financial-account semantics
- User creates freely named accounts and supplies an opening balance that is **not income**.
- Expenses reduce an ordinary asset-account balance; income increases it.
- Internal transfers move funds but must not be counted as income or spending.
- Credit cards have debt/liability semantics; repayments must not double count spending.
- Historical edits and deletions correct derived balances and reports; archived accounts retain existing history.
- No transaction payer field; creator/editor audit metadata is separate.
- Account visibility can be granted selectively to other users.

## Design principles
1. **Fast ordinary entry:** simple expense entry should require few interactions even with the richer data model.
2. **No fabricated certainty:** receipt extraction suggests data; user reviews/corrects it, including low-confidence fields.
3. **Household and account privacy first:** multiple separate identities and permissions, one or more shared workspaces (scope to be agreed).
4. **Finance correctness:** exact decimal arithmetic, explicit transaction types, consistent totals and non-double-counted transfers.
5. **Privacy first:** never commit genuine family budgets, receipts, bank details, PII, credentials, logs, or tokens to this public repository.
6. **Data portability:** import/export, deletion, backup/restore and vendor-independent storage are first-class requirements.
7. **Accessible and localized:** start with Bulgarian UI and euro currency as a *candidate*, not a fixed restriction; determine other locales/currencies during discovery.
8. **Testable by design:** product invariants, edge cases, and examples precede implementation tasks.

## Not in scope without separate approval
Bank-login scraping, autonomous payments, paid subscriptions, public social features, inventory, shopping-list automation, retail promotions, or mass AI data sharing. Historical ideas in the 2023 README are not automatically part of this project.

## Definition of discovery completion
Signed-off domain model, category rules, family membership and permissions, receipts review state machine, budget semantics, export and import contracts, deployment/authentication ADRs, prioritized MVP/non-MVP boundaries, and a dependency-ordered implementation backlog with acceptance criteria.
