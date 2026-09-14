# Technical Requirements Document: Occasion Guide

**Status:** Draft 1.0  
**Companion:** [PRD](PRD.md)  
**Implementation posture:** build a fast public reading experience first; add authenticated, pre-moderated contribution second.

## 1. Architecture summary

Use a content-first web architecture with a small, auditable contribution system.

```text
Public reader
  -> Next.js site on Vercel
  -> published guide content and search index

Signed-in contributor
  -> authenticated contribution form
  -> API validation and rate limit
  -> moderation queue
  -> approved public community note

Editor / moderator
  -> protected editorial console
  -> review, approve, reject, redact, or publish correction
```

## 2. Recommended stack

| Area | Choice | Reason |
| --- | --- | --- |
| Application | Next.js, TypeScript, App Router | Static-first pages, strong SEO, server rendering, and Vercel deployment. |
| Hosting | Vercel | Preview deployments, image optimisation, edge caching, and simple custom-domain setup. |
| Guide content at launch | MDX in Git | Reviewable editorial changes, pull-request history, and no CMS dependency before the content model stabilises. |
| Content after editorial scale | Headless CMS or database-backed editor | Add only when non-technical editors need a publishing workflow. |
| Authentication | Supabase Auth or equivalent managed OIDC provider | Email/social sign-in, session management, and account controls without building auth from scratch. |
| Data | PostgreSQL via Supabase or managed Postgres | Relational moderation, source, tag, and contribution data. |
| File storage | Private object storage with signed upload URLs | Optional contribution attachments; do not expose raw uploads by default. |
| Abuse controls | CAPTCHA alternative / bot defence, rate limiting, moderation queue | Public comments need protection from spam and harmful content. |
| Observability | Vercel Analytics plus error monitoring | Track reading flow and failures without collecting unnecessary sensitive data. |

## 3. Repository layout

```text
occasion-guide/
  app/
    (public)/
      page.tsx
      occasions/[slug]/page.tsx
      search/page.tsx
    api/
      contributions/route.ts
      reports/route.ts
    admin/
      moderation/page.tsx
  content/
    occasions/
      bach-baras.mdx
      ganesh-chaturthi.mdx
  components/
    preparation-path.tsx
    source-list.tsx
    community-notes.tsx
  lib/
    auth.ts
    content.ts
    moderation.ts
    validation.ts
  db/
    migrations/
    schema.sql
  docs/
    editorial-style-guide.md
  PRD.md
  TRD.md
```

## 4. Content model

### Occasion front matter

```yaml
title: Bach Baras
slug: bach-baras
alternate_names: [Bachh Baras, Govatsa Dwadashi]
occasion_type: festival
traditions: [Hindu]
regions: [Rajasthan]
summary: A regional guide to preparation and common variations.
reviewed_at: 2026-09-14
review_status: reviewed
sources:
  - label: Government of India Utsav
    url: https://utsav.gov.in/view-event/bach-baras-1
```

### Required guide sections

The build must reject a guide missing any of: summary, common preparations, variation note, local-confirmation questions, sources, review date, or safety/accessibility note.

## 5. Database model

| Table | Key fields | Notes |
| --- | --- | --- |
| `profiles` | `id`, `display_name`, `role`, `created_at`, `status` | Linked to auth identity; do not expose email publicly. |
| `occasions` | `id`, `slug`, `title`, `status`, `reviewed_at` | Mirrors published content and supports related data. |
| `occasion_sources` | `occasion_id`, `label`, `url`, `source_type`, `checked_at` | Source attribution and review. |
| `contributions` | `id`, `occasion_id`, `author_id`, `kind`, `body`, `region`, `language`, `status`, `created_at` | Status: pending, approved, rejected, redacted. |
| `moderation_actions` | `id`, `contribution_id`, `moderator_id`, `action`, `reason`, `created_at` | Immutable moderation audit trail. |
| `reports` | `id`, `contribution_id`, `reporter_id`, `reason`, `status` | Any approved item can be reported. |
| `saved_occasions` | `profile_id`, `occasion_id`, `created_at` | Phase 2 only. |

Use UUID primary keys, UTC timestamps, and foreign keys. Enable row-level security for every public-facing table.

## 6. Roles and permissions

| Role | Can read | Can submit | Can publish | Can moderate |
| --- | --- | --- | --- | --- |
| Visitor | Published content and approved notes | No | No | No |
| Member | Published content and own submissions | Yes | No | No |
| Editor | All public content and assigned drafts | Yes | Guide drafts | No, unless also moderator |
| Moderator | Published and queued contributions | No | No | Contributions only |
| Admin | All | Yes | Yes | Yes |

No client request may grant a role. Role checks occur server-side and are enforced by database policies.

## 7. Contribution and moderation workflow

1. Client fetches a CSRF-safe authenticated session.
2. The submission API validates the body, contribution type, region/language fields, and rate limit.
3. The server stores the contribution as `pending`; it is never visible in the public query.
4. A moderator sees context: occasion, contribution type, optional regional tag, author history, and report history.
5. Moderator approves, rejects with a private reason, or redacts unsafe personal data.
6. Only `approved` items are returned by public APIs.
7. A report can temporarily hide an approved item from public reads until a moderator reviews it.

### Moderation rules

Reject or redact content containing harassment, hate, caste or religious superiority claims, coercive instructions, medical claims, doxxing, spam, vendor solicitation, copied copyrighted text, or private information about a child/family.

## 8. API contract

| Method | Route | Purpose |
| --- | --- | --- |
| `GET` | `/api/occasions?query=&region=&type=` | Search/filter published occasion metadata. |
| `GET` | `/api/occasions/:slug/contributions` | Return approved community notes only. |
| `POST` | `/api/contributions` | Authenticated, rate-limited pending submission. |
| `POST` | `/api/reports` | Authenticated report of an approved note. |
| `GET` | `/api/admin/contributions?status=pending` | Moderator queue; protected. |
| `PATCH` | `/api/admin/contributions/:id` | Approve/reject/redact; protected and audited. |

All mutations use schema validation, structured error responses, request IDs, and server-side authorisation.

## 9. Security and privacy requirements

- Require authentication for any contribution or report.
- Store email only in the auth provider; show display name or initials only.
- Pre-moderate every public contribution in v1.
- Rate-limit sign-in-linked submissions, reports, and search endpoints.
- Escape or sanitise all user-generated text; render Markdown only through an allowlist.
- Do not allow HTML, script, embedded links with previews, or public file uploads in v1.
- Use secure cookies, HTTPS, CSP, CSRF protection for mutations, and environment-secret rotation.
- Record moderation actions but avoid logging full private content in analytics.
- Provide deletion/export requests and a retention policy before collecting saved occasions or notification preferences.

## 10. Search, SEO, and performance

- Generate static occasion pages at build time with revalidation for editorial updates.
- Create metadata, canonical URLs, Open Graph images, and structured data for each public guide.
- Index title, alternate names, plain-language summary, region, tradition, occasion type, and month/season.
- Use local search for the seed catalogue; introduce hosted search only when content size requires it.
- Serve responsive, compressed images; target Core Web Vitals green on common mobile networks.
- Never index pending contributions or moderator routes.

## 11. Accessibility and localisation

- WCAG 2.2 AA baseline: keyboard navigation, visible focus, colour contrast, semantic headings, and screen-reader labels.
- Dates must show calendar context carefully; no date is considered authoritative without an editorial source and declared regional/calendar basis.
- Keep all ritual terms in their original form alongside a plain-language explanation.
- Store language, script, and translation-review metadata separately from the guide body.
- Do not machine-translate ritual instructions directly into publication; require human review.

## 12. Delivery plan

### Milestone A - Readable pilot

- Next.js shell and design tokens.
- 8-12 MDX guides, source cards, preparation path, and search.
- No accounts, comments, or database required.

### Milestone B - Safe contribution

- Authentication, Postgres schema, row-level security, contribution form, moderation queue, reports, and audit trail.
- Security review before public launch.

### Milestone C - Personal planning

- Saved guides, optional reminders, translation workflow, and editorial dashboard.

## 13. Test strategy and acceptance criteria

| Area | Acceptance criterion |
| --- | --- |
| Public guide | A guide loads without authentication, has sources/review date, and passes keyboard navigation. |
| Submission | An authenticated member can create a valid pending note; visitor cannot. |
| Moderation | Pending/rejected/redacted contributions never appear in the public API or page HTML. |
| Reporting | A report hides the relevant item until review and creates an audit event. |
| Authorisation | A member cannot read or alter another member's private moderation outcome. |
| Content safety | Dangerous HTML and disallowed links render as plain text or are rejected. |
| Search | Search returns only published occasions and respects filters. |
| Mobile | Preparation Path, checklist, and comments remain usable at 320 px viewport width. |

## 14. Operational runbook

- Review moderation queue daily during the first three seasonal launches.
- Review source links and dates before every festival season.
- Keep a public correction policy and an internal incident log.
- Back up database daily once contribution data exists.
- Use preview deployments for editorial and application changes.
- Do not deploy a guide with unresolved high-severity correction requests.

