# Fragment (fragment-dev)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
