# Fragment (fragment-dev)

Fragment is a ledger API for engineering teams. It provides a real-time, double-entry ledger to track money movement, model balances, and reconcile against external systems (banks, processors, PSPs). The product is GraphQL-first — developers define a Schema (chart of accounts and entry types), create Ledgers, post immutable Ledger Entries composed of balanced debit/credit lines, and read balances and lines back through a single GraphQL endpoint. Every write mutation is idempotent.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/fragment-dev/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/fragment-dev/refs/heads/main/apis.yml)

## Tags

- Ledger
- Double-Entry
- Accounting
- Fintech
- Payments
- Reconciliation
- GraphQL
- Balances

## Timestamps

- **Created:** 2026-07-01
- **Modified:** 2026-07-01

## Authentication

Fragment uses the **OAuth2 client-credentials** flow. Exchange a `client_id`/`client_secret` (HTTP Basic) at a region-scoped token endpoint (for example `https://auth.us-west-2.fragment.dev/oauth2/token`) for a Bearer access token (~1 hour lifetime), then send it on every GraphQL request. See [graphql/fragment-dev-graphql.md](graphql/fragment-dev-graphql.md).

## APIs

### Fragment Ledger GraphQL API

Single GraphQL endpoint for defining a ledger Schema, creating Ledgers, posting balanced double-entry Ledger Entries, and reading balances and lines. All write mutations are idempotent via an idempotency key (ik). The endpoint is region-scoped (for example api.us-west-2.fragment.dev) and authenticated with OAuth2 client-credentials Bearer tokens.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Ledger
- GraphQL
- Double-Entry
- Balances

#### Properties

- [Documentation](https://fragment.dev/docs)
- [API Reference](https://fragment.dev/api-reference)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)
- [Postman Collection](collections/fragment-dev.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/fragment-dev.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Fragment Schema API

Define and version the ledger Schema — the chart of accounts, account types (asset, liability, income, expense), currency modes, and the ledger entry types your product posts. Stored with the storeSchema mutation and read back via the schema field on a ledger.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Schema
- Chart of Accounts
- Entry Types

#### Properties

- [Documentation](https://fragment.dev/docs)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)

### Fragment Ledgers API

Create and query Ledgers from a stored Schema. A Ledger is an isolated database for tracking money for a use case, tenant, or environment, created with createLedger and read with the ledger query.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Ledgers
- Provisioning

#### Properties

- [Documentation](https://fragment.dev/docs)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)

### Fragment Ledger Entries API

Post immutable, balanced double-entry Ledger Entries made of debit and credit lines against accounts. Uses addLedgerEntry with an idempotency key (ik), reverseLedgerEntry to correct posted entries, and the ledgerEntry query to read a single entry back.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Ledger Entries
- Postings
- Double-Entry
- Idempotency

#### Properties

- [Documentation](https://fragment.dev/docs)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)

### Fragment Balances API

Read real-time balances and the underlying lines. Query overall ledger balances (getLedgerBalances), per-account balances (getLedgerAccountBalances), and the debit/credit lines behind an account (getLedgerAccountLines), across single or multi-currency accounts.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Balances
- Lines
- Reporting

#### Properties

- [Documentation](https://fragment.dev/docs)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)

### Fragment Reconciliation API

Match ledger activity against external money movement. reconcileTx reconciles a transaction idempotently by transaction ID, while syncCustomAccounts and syncCustomTxs ingest external accounts and transactions to keep the ledger and source systems in agreement.

- **Human URL:** [https://fragment.dev/docs](https://fragment.dev/docs)
- **Base URL:** `https://api.fragment.dev/graphql`

#### Tags

- Reconciliation
- Payments
- Sync

#### Properties

- [Documentation](https://fragment.dev/docs)
- [GraphQL](graphql/fragment-dev-graphql.md)
- [GraphQL Schema](graphql/fragment-dev-schema.graphql)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/fragment-dev)
- [Website](https://fragment.dev)
- [Documentation](https://fragment.dev/docs)
- [Sign Up](https://dashboard.fragment.dev)
- [Status Page](https://status.fragment.dev)
- [Change Log](https://fragment.dev/changelog)
- [Plans](plans/fragment-dev-plans-pricing.yml)
- [Rate Limits](rate-limits/fragment-dev-rate-limits.yml)
- [Fin Ops](finops/fragment-dev-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
