<!-- SPEC-ID: 002 | Date: 2026-11-12 | Type: Feature | Status: DRAFT 2026-11-12 (to challenge) -->

# 002: Foundation — Task

---

## 💼 Business Context

### Current State

Spec 001 tests demand with a static landing page. No app code exists.

### Problem / Opportunity

The MVP handles personal documents (CVs, offers, later contracts and nóminas) and calls a paid LLM. Privacy, cost control and deploys have to be right from the first line, not added later.

### Desired Outcome

Yoel opens `sueldo-justo.pages.dev` on his iPhone, adds it to the home screen, logs in with an email link, and sees an empty "Mis candidaturas" screen. A test endpoint returns an LLM answer through the backend, with the call's cost logged and no document text stored.

---

## 📋 Requirements

### Functional Requirements

1. **App skeleton**
   - TypeScript (strict) + Vite, installable PWA (manifest, icons, offline shell). Mobile-first layout for 360–430 px wide screens.
   - UI framework: to decide (see Open Questions); all user-facing text in `src/strings/es.ts`.
   - Routes for the MVP screens as placeholders: onboarding, paste an offer, offer result, tailored CV, my applications, settings.
2. **Backend**
   - Cloudflare Workers (API under `/api`), deployed with Pages.
   - Database: Cloudflare D1 (SQLite) for users, profiles (sector, province, category, convenio) and applications. Schema migrations versioned in the repo.
   - Convenio knowledge base as typed data files in the repo (`data/convenios/`), loaded by the Worker; no database for it in the MVP (content as data).
3. **Login**
   - Email magic link (no passwords). Session in an HttpOnly cookie.
   - Email delivery through a transactional email service (to decide).
   - Delete my account: removes the user and all their data at once.
4. **LLM gateway**
   - One backend module that every AI feature calls: provider and model set in config, API key only in Worker secrets, never in the app.
   - Per-call logging of model, tokens and cost, never prompt or document text.
   - Per-user daily limit and a global monthly spend cap that turns AI features off with a friendly message.
   - Test endpoint `/api/ai/ping` (admin only).
5. **Documents and privacy**
   - CVs are parsed in the request and kept only if the user saves them; saved CVs stored encrypted (to decide: D1 field or R2 object).
   - Privacy policy and legal notice pages in Spanish; cookie use limited to the session cookie and privacy-friendly analytics.
6. **Builds and CI**
   - GitHub Actions: typecheck, lint, tests on every push; deploy to Cloudflare Pages on main, preview link per branch (same as Idle Love & Lava).
   - `npm run dev` runs app and Worker locally with a local D1.

### Non-Functional Requirements

- **Performance:** first load under 2 s on 4G on Yoel's iPhone; app shell under 150 KB gzipped.
- **Cost:** €0 fixed cost on free tiers until real users; LLM spend capped (value to decide).
- **Privacy:** GDPR basics from day one: data minimisation, delete account, no document text in logs, EU data location where the service allows.
- **Accessibility:** readable at 200% text size; colour is never the only signal (the badge uses icon + text).

---

## ✅ Acceptance Criteria

| # | Given | When | Then |
|---|-------|------|------|
| AC1 | a push to main | CI finishes | the app is live at `sueldo-justo.pages.dev` and installable from Safari on iPhone |
| AC2 | a new visitor | they enter their email and open the link | they are logged in and see "Mis candidaturas" (empty) |
| AC3 | a logged-in user | they choose "Borrar mi cuenta" and confirm | their user, profile and applications are gone from D1 |
| AC4 | the admin | they call `/api/ai/ping` | an LLM answer comes back and the log shows model, tokens and cost, and no prompt text |
| AC5 | the monthly spend cap is reached | any AI feature is called | it returns a friendly "no disponible ahora" message and no LLM call is made |
| AC6 | the app bundle | it is built | no API key or secret appears in it |
| AC7 | a pull request | CI runs | typecheck, lint and tests pass and a preview link is posted |

---

## 🚫 Out of Scope

Convenio data (003), salary badge (004), offer extraction (005), tailored CV (006), tracker and paywall (007), Capacitor app, payments.

---

## ✅ Decisions (2026-11-12)

1. **Starts after a "go" from 001.**
2. **Hosting:** Cloudflare Pages + Workers + D1 (free tiers), same family as Idle Love & Lava.
3. **Convenio data lives in the repo as typed files**, not in the database, for the MVP.

## ❓ Open Questions

1. **UI framework:** plain TypeScript + a small view layer (like Idle Love & Lava), Preact, or Svelte? (Claude leans to Preact: small, familiar React model, good for forms and lists.)
2. **LLM provider and model:** Claude (Haiku-class for extraction, Sonnet-class for CV writing?), another provider, or decide per feature in 005/006?
3. **Email service for magic links:** Resend, Postmark or Cloudflare Email Sending?
4. **Saved CVs:** encrypted field in D1 or encrypted object in R2?
5. **Monthly LLM spend cap:** €20? €50?

---

## 👥 Stakeholders

| Role | Name | Interest |
|------|------|----------|
| Decision maker and developer | Yoel | A safe, cheap skeleton that every MVP spec plugs into |
| Users | Job seekers | Fast app, private documents, easy login |
