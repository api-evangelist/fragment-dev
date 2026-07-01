# Fragment Ledger GraphQL API

Fragment (fragment.dev) is a ledger API for engineering teams. It provides a
real-time, double-entry ledger that tracks money movement, models balances, and
reconciles against external systems. Fragment is GraphQL-first: there is a single
GraphQL endpoint that covers schema definition, ledger provisioning, posting
entries, reading balances, and reconciliation.

**Endpoint:** `https://api.fragment.dev/graphql` (region-scoped, e.g. `https://api.us-west-2.fragment.dev/`)
**Schema:** https://api.fragment.dev/schema.graphql
**Documentation:** https://fragment.dev/docs
**API Reference:** https://fragment.dev/api-reference

- Reference: https://fragment.dev/api-reference
- Schema (local): [fragment-dev-schema.graphql](fragment-dev-schema.graphql)

## Authentication

Fragment uses the **OAuth2 client-credentials** flow. You exchange a `client_id`
and `client_secret` for a short-lived access token, then send it as a Bearer
token on every GraphQL request.

- **Token endpoint (region-scoped):** `https://auth.us-west-2.fragment.dev/oauth2/token`
- **Grant:** `grant_type=client_credentials`
- **Scope (region-scoped):** e.g. `https://api.us-west-2.fragment.dev/*`
- **Client auth:** HTTP Basic header `Authorization: Basic base64(client_id:client_secret)`
- **Access token:** expires in ~1 hour; sent as `Authorization: Bearer {access_token}` on API calls

```bash
curl -X POST https://auth.us-west-2.fragment.dev/oauth2/token \
  -H "Authorization: Basic $(printf '%s:%s' "$CLIENT_ID" "$CLIENT_SECRET" | base64)" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=client_credentials&scope=https://api.us-west-2.fragment.dev/*&client_id=$CLIENT_ID"
```

## Core Concepts

- **Schema** — A versioned configuration that defines the chart of accounts,
  account types (asset, liability, income, expense), currency modes (single or
  multi), and the ledger entry types your product posts. Stored via `storeSchema`.
- **Ledger** — An isolated database for tracking money, created from a Schema with
  `createLedger`. Ledgers can be `event` or `balance` type.
- **Ledger Account** — A container for money (asset / liability / income / expense).
  Accounts are hierarchical (via `path`) and track balances by currency.
- **Ledger Entry** — An immutable posting to the ledger, composed of balanced
  debit/credit **lines** (up to 30 per entry). Written with `addLedgerEntry` and an
  idempotency key.
- **Line** — A single debit or credit against one account, with an amount and
  currency. The debits and credits of an entry must balance (double-entry).
- **Idempotency Key (`ik`)** — A unique key on every write mutation that makes
  retries safe and prevents duplicate postings.

## Queries

| Operation | Purpose |
|-----------|---------|
| `ledger` | Retrieve ledger configuration, status, schema, and accounts. |
| `ledgerAccount` | Retrieve a single account's details and metadata. |
| `ledgerEntry` | Retrieve a specific posted ledger entry and its lines. |
| `getLedgerBalances` | Read overall balances for a ledger. |
| `getLedgerAccountBalances` | Read balances for specific accounts. |
| `getLedgerAccountLines` | Read the debit/credit lines behind an account. |

## Mutations

All write mutations are idempotent via an idempotency key.

| Operation | Purpose |
|-----------|---------|
| `storeSchema` | Store / version a ledger Schema definition. |
| `createLedger` | Create a new ledger from a stored Schema. |
| `addLedgerEntry` | Post a balanced double-entry ledger entry (`ik` required). |
| `reverseLedgerEntry` | Reverse a previously posted entry. |
| `reconcileTx` | Reconcile a transaction against external money movement (idempotent by transaction ID). |
| `syncCustomAccounts` | Ingest / sync external accounts (idempotent by account ID). |
| `syncCustomTxs` | Ingest / sync external transactions (idempotent by transaction ID). |

## Example: post a balanced entry

```graphql
mutation PostSimpleEntry($ik: SafeString!) {
  addLedgerEntry(
    ledgerIk: "main"
    ik: $ik
    type: "user_funds_account"
    date: "2026-07-01"
    parameters: {
      amount: "10.00"
      currency: { code: "USD" }
      userId: "user-123"
    }
  ) {
    __typename
    ... on AddLedgerEntryResult {
      entry { ik posted date lines { amount currency { code } type account { path } } }
    }
    ... on BadRequestError { code message }
    ... on InternalError { code message }
  }
}
```

## Example: read a balance

```graphql
query GetBalance {
  ledgerAccount(ledgerIk: "main", path: "user_funds/user-123") {
    path
    name
    type
    ownBalance {
      amount
      currency { code }
    }
  }
}
```
