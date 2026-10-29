# Family Finance

A family finance management application focused on **shared and private financial accounts**, fast income/expense/transfer tracking, configurable budgets, item-level receipt capture, and rich reports.

> **Status: product discovery, not implementation.** Requirements, domain rules, security, platform choices, and the implementation backlog are being defined through staged interviews. The repository is public, but financial data is private.

## Core direction
- Browser and installable Android/iPhone experiences (distribution and offline strategy to be decided).
- User-created accounts with custom names, initial balances, income, expenses, and transfers.
- Optional sharing of each financial account with selected household members.
- Transactions link to the **funding account**, not a separate "who paid" field.
- One transaction may have multiple purchased products, categories, quantities, and optional store details.
- Assisted image/PDF receipt import produces an **editable draft**, never an automatically approved expense.
- Reports and exports: PDF, XLSX and CSV; import historical transactions from Bluecoins.
- Modern passwordless sign-in (mechanism and recovery to be selected).

## Planning process
1. Interview for a complete, unambiguous product specification and edge cases.
2. Record approved choices separately from suggestions and open questions.
3. Prepare epics and implementation issues, with acceptance criteria, tests, dependencies, and Codex-ready prompts.
4. Implement only after scope is agreed, using Draft PRs and independent review; no auto-merge.

**Privacy:** Do not put real family receipts, balances, financial details, user data, credentials, tokens or production exports into this public repository. Use fictional samples only.

_The detailed discovery documents are being migrated from the previous planning repository into this new codebase. No legacy application code is being imported._
