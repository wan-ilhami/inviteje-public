# Architecture

High-level, public-safe view of how Inviteje is built. No internal URLs, credentials, or infrastructure identifiers — just the shape of the system.

## Two products, one platform

Inviteje is two independent products that happen to share infrastructure:

1. **Wedding Invitations** — the main SaaS. Invitation creation, RSVP, guest wishes, admin dashboard. A Next.js application with server-rendered pages and server-side data access.
2. **Wedding Photos** — a disposable-camera-style companion app. Guests join an event with a link, capture photos/video, and see a shared live feed. A dedicated Express API service, its own database schema, and a mobile app (React Native / Expo).

They are not one unified data model. A guest joining a Photos album has nothing to do with the Invitations tenancy model, and vice versa — the two domains are kept structurally separate even where they run in the same process today.

## Multi-tenancy: Postgres Row-Level Security

Every tenant's data (a couple's invitation, its guest list, its wishes) is isolated with Postgres **Row-Level Security**, not application-layer filtering. The application never queries the database with elevated/bypass privileges in a request path — every query runs scoped to the authenticated tenant, enforced by the database itself. This means a bug in application code cannot leak one couple's guest list into another's dashboard; the database refuses the row regardless of what the query asks for.

## Templates: one contract, unlimited designs

Every invitation template is visually distinct — different typography, color language, motion, physical metaphor — but every template is required to implement the same guest-facing contract: RSVP form, wishes wall, add-to-calendar, locale switching, an optional password gate, and a photo gallery. A template author can make anything look like anything; they cannot ship a template that's missing platform functionality. This is enforced by an automated contract validator that runs against every template before it ships.

## Deployment target

- **Frontend & backend**: Vercel (serverless), as two independent deployments sharing a JWT-signed trust boundary between them.
- **Database**: managed Postgres (connection-pooled for serverless concurrency), with RLS policies applied as versioned migrations.
- **Hot media storage**: S3-compatible object storage with direct-from-client presigned uploads — media never passes through the application server.
- **Cold archive**: event media moves to long-term storage after a guest-download window closes; nothing sensitive stays in hot storage indefinitely.
- **Mobile**: React Native (Expo), talking to the same backend API as the web app — one API, multiple clients.

## What this repo publishes

This public repository carries the shared data contract between frontend and backend (see [`VERSIONS.md`](./VERSIONS.md)) and this architecture overview. It intentionally does not carry application source, infrastructure configuration, or anything that would let someone stand up a copy of the private stack.
