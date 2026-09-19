# Inviteje

**Beautiful, shareable wedding invitations — with real RSVP, guest wishes, and a photo-sharing companion app.**

Inviteje is a multi-tenant SaaS for couples who want a wedding invitation that looks hand-crafted, not templated. Every design is built to a strict craft floor — bespoke SVGs, custom typography, physical material metaphors, living motion — and still ships with full platform functionality: RSVP, guest wishes, a countdown, add-to-calendar, a locale switcher, and an optional password-gated guest list.

## Screenshots

| | | |
|---|---|---|
| ![Agate Foil](./assets/screenshots/agate-foil.png) | ![Billet Doux](./assets/screenshots/billet-doux.png) | ![Jejak Kembara](./assets/screenshots/jejak-kembara.png) |

Three of dozens of hand-built templates — each with its own physical archetype, ambient lighting, and motion design. No two look like the same product wearing different colors.

## What's inside

- **Invitations** — the core product. Create an invitation, pick a template, share one link. Guests RSVP, leave wishes, add the date to their calendar, and unlock a gated invitation with a passcode if the couple wants privacy.
- **Wedding Photos** — a companion "disposable camera" experience for the event itself: guests join with a link/QR, capture photos and short videos through the app, and everyone sees a shared live feed. Albums move to cold storage after the event; the couple keeps a full-resolution archive.
- **Dozens of templates, one contract** — every template is visually unique but guarantees the same guest-facing functionality (RSVP, wishes, calendar, gallery, password gate). Couples pick the look; the platform guarantees the substance.

## Try it

The product is being brought up on production infrastructure right now — see [`VERSIONS.md`](./VERSIONS.md) for what's shipped. Interested in an early look or want to build your invitation on Inviteje? Reach out via the contact on this GitHub profile.

## Architecture

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for how the system is put together: two independent products sharing infrastructure, Postgres row-level security for tenant isolation, and the deploy target (Vercel + managed Postgres + object storage).

## What this repository is

This is the **public** half of Inviteje's codebase — the shared data contract, version table, and architecture overview. The application code (Next.js frontend, Express backend, React Native mobile app) lives in a private repository. This repo contains:

- ❌ No API keys, tokens, credentials, internal URLs, or customer/PII data.
- ✅ Only the shared data contract, architecture docs, and screenshots.

_This is a separate git repository, nested inside the private `inviteje` monorepo for convenience but gitignored there._
