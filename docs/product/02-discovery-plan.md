# Staged interviews and requirements roadmap

Parent: [#6](https://github.com/HristoManov91/family-finance/issues/1). This is the **single source of truth for discovery order**, not a Codex implementation prompt.

## Phase A — Product discovery (current)
| Stage | Topic | Deliverable |
| --- | --- | --- |
| A0 | Repository choice and baseline usage | New public repo chosen; website + installable Android/iOS confirmed |
| A1 | Financial accounts, opening balances, credit cards, transfers, selective visibility, edits | Account lifecycle + permission rules |
| A2 | Transaction header, item rows, split lines, returns, promotions, VAT, currencies | Transaction specification, examples and invariants |
| A3 | Categories, subcategories, product name/alias catalog, quantities and merchant | Classification and catalog rules |
| A4 | Receipt photo/PDF import, recognition and corrections, asynchronous jobs, duplicate protection | Extraction/review state machine and sample fixtures |
| A5 | Incomes, global budget, category/member caps, periods and carryover | Budget calculation rules + edge-case scenarios |
| A6 | Search, reports, comparisons, product trends and PDF/XLSX/CSV | Reporting catalog and export contract |
| A7 | Web/mobile UX, offline and sync, passkeys/recovery, privacy, backups | UX journeys and security assumptions |
| A8 | Bluecoins migration, duplicates and historical correctness | Import mapping with preview, reconciliation |
| A9 | Architecture/stack/deployment and release strategy | ADRs, nonfunctional requirements, MVP boundary |

### Completed A0 and A1 answers (2026-10-29)
- New public repository `HristoManov91/family-finance`, no inherited legacy implementation.
- Arbitrarily named accounts, opening balances outside income, explicit transfers, credit-card account semantics.
- Each account has selectable visibility to members; fine-grained view/edit and reporting policy open.
- No payer/beneficiary field: the financial **source account** matters.
- Corrections of older transactions update balances; historical accounts are archived, not destructively erased.
- Import long-term Bluecoins history, with missing modern fields left blank.
- Android and iPhone; installable experience wanted, PWA vs app-store distribution undecided.

## Phase B — Backlog architecture
- Create a small set of **domain epics** after their spec has been agreed: Identity & Households; Accounts & Transactions; Taxonomy & Product Catalog; Receipt Intake/AI; Budgets & Recurring; Reporting & Exports; Bluecoins Import; Mobile/UX; Quality/Deployment.
- Each epic links to canonical specs and lists explicit cross-epic dependencies and out-of-scope items.
- Implementation Issues must be vertical, independently testable slices: problem, business rules, API/schema changes, UI scenarios, acceptance criteria, errors and limits, tests, migration, observability, security, dependencies.
- Track MVP / Later / Won't implement. Do not generate false precision (story points/dates) before requirements.

## Phase C — Implementation and review
- Start from an approved baseline + CI/security checks + local test environment.
- Codex takes **one implementation Issue**, creates **one Draft PR**, leaves it Draft and leaves Issue OPEN.
- Validate tests and CI at exact final head SHA; independent ChatGPT/user reviews the full diff and source requirements.
- Fix prompts remain copyable single blocks; merge only after explicit approval. No auto-merge.

## Discovery exit criteria
- All MVP screens and user workflows have signed-off examples.
- Domain entities and financial invariants are explicit (including refunds and item-total rounding).
- AI handling, verification states and data confidentiality are explicit.
- Hosting, passwordless sign-in, account recovery, family permissions and backup tested at design level.
- Codex implementation backlog is ordered; no blocking product questions are left inside coding tasks.
