# Domain Model v0.2 — discovery hypotheses (NOT implementation)

See [master discovery Issue #1](https://github.com/HristoManov91/family-finance/issues/1). The model is NOT an approved schema. It records user-confirmed capabilities and hypotheses requiring domain review.

## Candidate domain concepts

| Concept | Purpose / meaning | Status |
| --- | --- | --- |
| User | Individual passwordless identity; edits recorded for audit (NOT financial payer) | Required, auth provider open |
| Household / Workspace | Membership and permissions boundary for collaborating users | Required, invitation model open |
| FinancialAccount | Custom name, account type, currency, opening amount, status and account-specific visibility | Required |
| AccountAccess | Selected users with specific account permissions; authorization applies to linked transactions and exports | Visibility confirmed; roles open |
| FinancialEvent / Transaction | Expense, income, transfer, adjustment/correction, optional refund; name, date, amount, source/destination account(s) | Core required; refund rules open |
| TransactionItem | Purchased item/product or service with original title, normalized title, quantity, unit, price, category/subcategory | Required for itemized transactions, not mandatory for historic/manual single expenses |
| Category | Main category and optional subcategory, user-manageable and icon-rich | Required |
| Product | Optional normalized catalogue with aliases, units, store-specific display name | Candidate |
| Merchant | Optional shop/vendor name and location | Required optional metadata |
| ReceiptDocument | Protected PDF/photo and processing metadata | Required |
| ExtractionJob | OCR/AI-generated **draft** of transaction and items, manual confirmation and field-level corrections | Required |
| Budget | Limit/actual amount for selected period, scope and category/financial account | Required; semantics open |
| ImportBatch | Bluecoins import with preview, mapping, validation, deduplication, re-run safety | Required |
| AuditEvent | Actor and timestamp of changes; **not** a financial payer/beneficiary | Candidate |

**No payer or beneficiary field.** Expense entries reference the financial source account. Who created/edited a record may be stored for audit, but should not be used to classify expenses unless the owner explicitly asks later.

## Confirmed financial invariants

1. An **initial opening balance is NOT income**. When creating a cash/bank account, the initial value defines the balance baseline.
2. An expense subtracts from an ordinary asset account, and income adds to it. A credit-card liability must use debt-specific semantics.
3. A transfer moves funds between accounts as **one linked operation** and is not included in income/expense reports or overall family spending.
4. An edit, correction or void of an old transaction updates historical/current balances and report totals consistently.
5. An account with recorded history is archived rather than destroyed. Normal new transactions should not select an archived account.
6. Account visibility is per selected member; hidden accounts and associated transaction data **must not leak through search, reports, exports, receipt links or side of a transfer**.
7. Multi-line receipt items and their category breakdown MUST NOT be double counted in addition to the transaction total.
8. Use exact decimals and currency-specific rounding, never binary floating-point for money.
9. Old Bluecoins imports remain valid even if newly added per-product quantity/price fields are missing.
10. OCR/AI results are **drafts**. No financial posting until explicit user acceptance.
11. Credit-card purchases, repayments, refunds, interest and available-limit handling require explicit business rules and tests.

## Synthetic grocery transaction

*Transaction:* Grocery visit, paid from account `Shared Card`, category `Food`, date `2026-10-01`, merchant `Example Shop`, optional description `Weekly shopping`, total `12.30 EUR`.

| Item | Qty / unit | Final price | Main category | Subcategory |
| --- | --- | --- | --- | --- |
| Apples | 1.5 kg | 3.00 EUR | Food | Fruit & vegetables |
| Milk | 2 pcs | 3.30 EUR | Food | Dairy |
| Soap | 2 pcs | 6.00 EUR | Household | Cleaning |

The transaction-level `Food` category may serve as a default, but the soap must be attributed to `Household / Cleaning` for itemized reports. How inherited categories, discounts, VAT and rounding work is still open.

## Synthetic account examples

- Cash opening 500 EUR = balance 500 EUR, income report 0.
- Income 100 EUR to cash = balance 600 EUR, income 100.
- Expense 25 EUR from cash = balance 575 EUR, expense 25.
- Transfer 75 EUR from cash to bank = cash 500 EUR and bank +75 EUR, income/expense unchanged.
- Credit-card purchase 35 EUR = expense 35 EUR and card liability +35 EUR.
- Pay card debt 35 EUR from bank = bank -35 EUR, liability -35 EUR, **no additional expense**.

Credit card examples are **proposed conventions** pending the next interview, not a final accepted sign/balance contract.

## Questions
- View-only versus view/edit/manage account permissions, hidden transfer counterparties, household budgets.
- Multi-currency accounts, FX and currency exchange when transferring.
- Credit-card limit, repayment, overpayment, installments, interest/fees and due dates.
- Item-level category defaults, split tenders, partial refunds, vouchers, discounts and quantity units.
- Whether deleting transactions means voiding/archiving with audit history instead of permanently deleting.
