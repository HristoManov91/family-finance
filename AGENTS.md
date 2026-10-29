# AGENTS.md — Family Finance repository rules

**PHASE: PRODUCT DISCOVERY. NO IMPLEMENTATION WORK IS AUTHORIZED YET.**

- Follow [master discovery #1](https://github.com/HristoManov91/family-finance/issues/1) and the current accepted decision log before proposing code.
- This is a **new** repository; DO NOT reuse 2022–23 legacy code or assumptions.
- Clearly separate `ACCEPTED`, `PARTIAL`, `PROPOSED` and `OPEN` in specs. Newer user answers supersede older provisional assumptions.
- There is **no financial payer/beneficiary field**. Expenses link to their funding account. CreatedBy/updatedBy may be used for audit only.
- Opening balances, asset spending, income, transfers and credit-card debt are distinct domain operations; avoid double counting credit-card repayments and transfers.
- Per-account sharing and household isolation must be enforced on every read, write, report, export, attachment and linked transfer.
- PUBLIC REPOSITORY: no actual receipts, names, home addresses, financial statements, real household budgets, bank details, production data, tokens, credentials or private exports. Use synthetic examples only.
- Do not add implementation dependencies, UI, backend endpoints or schema until the corresponding implementation Issue is approved.
- One approved bounded implementation Issue per Draft PR. Do not auto-merge, mark Ready, close Issues or claim checks not run.
- Provide final SHA, exact checks, full scope and risk notes. Independent review precedes user-authorized merge.
- Avoid unrelated refactors and overengineering; note additional opportunities separately.
