# inviteje-public

**Public** shared contract + version table for Inviteje.

This repository is the dependency-free, secret-free description of the data shape that flows between Inviteje's `frontend` and `backend`. It contains **no API keys, no internal URLs, and no customer data** — only the contract and docs.

> **Phase 1 status: placeholder.** The real shared contract (the invitation `data` shape, today defined by `frontend/templates/_shared/wedding-core-v1.ts`) is published here when the backend is extracted in phase 2.

## Contents
- [`VERSIONS.md`](./VERSIONS.md) — released versions of frontend/backend (updated by release automation).
- _(phase 2)_ the shared `WeddingInvitation` data contract.

## Rules for this repo
- ❌ No API keys, tokens, credentials, internal URLs, or customer/PII data.
- ✅ Only the shared data contract, helper signatures, and architecture docs.

_This is a separate git repository, nested inside the private `inviteje` monorepo for convenience but gitignored there._
