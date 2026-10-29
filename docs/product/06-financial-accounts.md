# Financial accounts — A1 working specification v0.1

**Status:** core capabilities accepted, critical edge cases open. See [master discovery #1](https://github.com/HristoManov91/family-finance/issues/1), [accounts discovery #2](https://github.com/HristoManov91/family-finance/issues/2), and the decision log.

## Confirmed core behavior
- User can create freely named accounts, regardless of whether they represent bank, cash, debit card, credit card, named person or something else.
- Account creation supports **opening balance** that does not count as income.
- On an asset account: expense reduces current balance, income increases current balance.
- On a credit card: real liability behavior is desired, not naive cash balance handling. Exact reporting and limit rules remain open.
- Transfer between two accounts is supported; does not count as income or expense.
- An account has a configurable set of users who can **see it**. Being in the same household does not imply every account is visible.
- Editing/voiding a historical transaction corrects current and historical account balances and reports.
- Accounts with history should support archive instead of unsafe deletion. Archived accounts should not accidentally be selected for normal new entries.
- Transactions have name and optional free text, reference an account and never store a **financial payer** field.

## Example A — Cash-like account (synthetic)
1. Opening EUR 300 -> balance 300, income report 0.
2. Receive income EUR 500 -> balance 800, income report +500.
3. Spend EUR 40 -> balance 760, expense report +40.
4. Transfer EUR 100 to debit card -> balance 660, card +100, **no** extra expense or income.
5. Correct prior expense 40 to 35 -> balance 665; historical monthly spending corrected to 35.

## Example B — Credit card (tentative behavior, not yet signed off)
- Limit EUR 1,000, initial debt 0.
- Buy EUR 70 -> debt 70, available limit 930, family expense +70.
- Repay EUR 70 from bank -> bank -70, debt reduces to 0, **no new spending**.
- Receive refund EUR 15 -> credit-card debt reduces (possibly credit balance); associated expense adjusted.
Questions: Is credit limit mandatory? Track statement dates, due dates, card fees and interest? What about negative debt/overpayments and installments?

## Example C — Selective visibility
- A shares account S with B. A keeps another account P private.
- B can see S, but **not** P or P's spending history, receipts, exported data, search hits or contribution to aggregates.
- Transfer P -> S may be visible on the S side, but must not disclose P's private name, balance or identifying metadata. Exact redaction rules and whether such transfers are allowed remain to decide.
- Current user who records a transaction should NOT be interpreted as the financial payer.

## Proposal: lifecycle
`ACTIVE` account can accept new entries and transfers; `ARCHIVED` account keeps its historical ledger and reports but disallows ordinary new entries. Restore to `ACTIVE` may be permitted with authorization. No destructive deletion while referenced by transactions.

## Non-negotiable correctness constraints
- Exact decimal amounts and currency-specific rounding.
- Transfers and credit-card repayments should not inflate income/expense reports.
- All account operations, reports, expenses, receipts, and exports require object-level permission checks.
- Historical corrections reliably adjust balances and period reports.
- Opening balance may be positive, zero or a debt baseline; semantics need to match account type.
- No public repo access to actual household financial data.

## Open questions for A1 closure
1. Credit card: Which balances to show — debt, available credit, statement due — and which extra flows (interest, monthly statements, fees)?
2. Visibility: For each other household user, should 'can view' and 'can edit/add' be separate permissions?
3. Repayments: Should bank -> credit card be handled as normal account transfer?
4. Transfers: What should a viewer of only one of the two accounts see?
5. Currency: one per account? Can transfers use two currencies and exchange rates?
6. Normal accounts: may balance go below zero? How should negative or archived accounts be shown?
7. Reports/budgets: should private accounts be excluded from all other members' summaries (including household total)?
