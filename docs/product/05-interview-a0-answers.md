# Interview outcomes — A0 + A1, 2026-10-29

No private financial amounts or identities are stored in this public file.

## A0 — repository, Bluecoins and platforms
- Created new public `HristoManov91/family-finance`; previous money-management repo is reference/legacy only.
- Android and iPhone are both used; app should be installable. The exact technology (PWA or app-store packaged app) remains open.
- History in Bluecoins is extensive and must be migrated, even though older records will lack newly introduced product fields.
- Users may create any number of financial accounts and give them arbitrary names. Account type and balance behavior are distinct from chosen names.

## A1 — verbatim question IDs, normalized product outcomes
1. **2.1 YES** — Account has a starting balance set on creation, separate from recognized income.
2. **2.2 YES** — Transfer funds directly between accounts, with no income or spending increase.
3. **2.3 YES** — Accounts can behave as true credit cards; exact statement/limit/debt and repayment UX to clarify.
4. **2.4 YES** — Choose for whom each account is visible. Permission levels and household aggregations to clarify.
5. **2.5 OVERRIDING CORRECTION** — The **person who pays does not matter**. Record **which account supplies money**. Do NOT design a distinct payer or beneficiary field. Creator/editor metadata is relevant only to audit.
6. **2.6 YES** — Editing/removing old transactions automatically corrects account balances; accounts with history should be archived rather than silently deleted.

## Consequences for product design
- Funding account (and destination account for transfer) is mandatory for posted transactions.
- A financial account cannot be assumed public to all members simply because the household is shared.
- Credit-card purchases count once as spending; credit-card settlements are not new purchases (proposed repayment details need interview).
- Personal/shared budgeting must not infer a payer from the user who entered the transaction.
- Historic Bluecoins records may have categories/names/dates/accounts/amounts but zero product rows.

## Current next interview
Finalize: credit-card debt & repayments; account view/edit roles; private-side transfer and reporting; currencies; negative account balances and archived-account lifecycle. Then move to full transaction and receipt-line interview.
