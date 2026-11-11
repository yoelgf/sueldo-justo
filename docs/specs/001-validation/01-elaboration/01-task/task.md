<!-- SPEC-ID: 001 | Date: 2026-11-12 | Type: Validation | Status: CHALLENGED 2026-11-12 (1 open question) -->

# 001: Validation — Task

---

## 💼 Business Context

### Current State

The concept, research and proposal exist (`docs/research/`, proposal doc). No code, no users, no convenio data.

### Problem / Opportunity

Two bets carry the whole product: (1) people want to know whether an offer pays what their convenio says and will pay for tailored applications; (2) the salary badge can be computed reliably from real offers. Both can be tested in about a week without building the app.

### Desired Outcome

After 7 days of traffic, Yoel has a clear go or no-go: waitlist sign-ups and paywall interest from real visitors, and a table of 20 real offers showing how often the badge could be computed and how long each check took.

---

## 📋 Requirements

### Functional Requirements

1. **Landing page (Spanish)**
   - Headline around the hook: "¿Te pagan lo que dice tu convenio?" Sub-line: paste any offer, see if it pays above your convenio, and get a CV tailored to it.
   - A static sample of the salary badge on a realistic offer (the screen-3 design of the MVP), with its citation line.
   - A waitlist form: email, sector (dropdown of the chosen convenios + "Otro"), province, and "¿Qué te interesa más?" (salary check / tailored CV / both).
   - A pricing block as a fake door: "Acceso anticipado: 4,99 €/semana o 9,99 €/mes" with a "Lo quiero" button that records the click, then explains it is not live yet and adds the person to the waitlist.
   - Legal basics: privacy notice (GDPR), what is stored (email, sector, province) and how to leave the list; no cookies beyond what the analytics tool needs.
2. **Hosting and data**
   - Static page on Cloudflare Pages; form submissions stored in a Cloudflare service or a simple form tool (decided below); one CSV export for analysis.
   - Privacy-friendly analytics (page views, form starts, sign-ups, fake-door clicks), no personal data in analytics.
3. **Traffic test**
   - Bring 500–1,000 visitors in 7 days without personal content: a small paid test (Google Ads on search terms such as "cuánto debo cobrar según convenio", "tablas salariales convenio") and posts in relevant communities (subreddits and forums about work in Spain), written as the product, not as Yoel.
   - Budget cap €100–150 for the paid part.
4. **Manual badge check (concierge)**
   - Pick 3–5 estatal convenios with many offers (candidates to verify: contact center, seguridad privada, ETT, consultoría, grandes almacenes).
   - Collect 20 real public offers in those sectors from different provinces.
   - For each: identify the convenio and category, find the current salary table, compare with the offer's salary, estimate net pay, and time the whole check.
   - Record the results in one table: offer, convenio, category found (yes / guessed / no), table year, salary in offer (yes/no), result, minutes spent, notes.

### Non-Functional Requirements

- **Time:** page live within 2 evenings; manual check within 1 week alongside the traffic test.
- **Cost:** under €150 total (domain, ads).
- **Privacy:** only email, sector and province are collected; deleted if the project stops.
- **No personal brand:** nothing on the page or posts identifies Yoel.

---

## ✅ Acceptance Criteria

| # | Given | When | Then |
|---|-------|------|------|
| AC1 | the landing page is deployed | a visitor opens it on a phone | the headline, sample badge, form and pricing block show without horizontal scrolling |
| AC2 | a visitor fills the form | they submit | the entry is stored and appears in the CSV export |
| AC3 | a visitor taps "Lo quiero" on pricing | the click is recorded | they see the "not live yet" message and can join the waitlist |
| AC4 | 7 days of traffic | the test ends | visits, sign-up rate and fake-door click rate are known from analytics |
| AC5 | 20 real offers | the manual check is done | the results table shows, per offer, whether the badge could be computed and the minutes spent |

---

## 🎯 Go / No-Go (proposed, to agree)

| Signal | Go if |
|--------|-------|
| Visitor → waitlist sign-up | ≥ 10% |
| Visitor → fake-door click | ≥ 3% |
| Offers where the badge could be computed (category found + current table) | ≥ 70% of the 20 |
| Average minutes per manual check | Low enough to automate: the hard part must be data, not judgement |

Mixed result (for example strong sign-ups, weak badge coverage): re-scope, don't kill. No-go: sign-ups under 5% and badge coverage under 50%.

---

## 🚫 Out of Scope

Any app code, AI, accounts, job feed, swipe deck, contract or nómina checks, Catalan. Each has its own spec.

---

## ✅ Decisions (2026-11-12)

1. **MVP shape:** "paste an offer" (badge + tailored CV + tracker); swipe deck later, once a legal job feed exists.
2. **Market:** the whole of Spain via estatal convenios first, not one region.
3. **Name:** "Sueldo Justo" (chosen over Curro and Nómina+ because it states the promise).
4. **Form storage:** a form tool (Tally or Formspree), live in minutes; the privacy notice names it as the processor.
5. **Traffic:** Google Ads (€100–150 cap) plus community posts.
6. **Go/no-go thresholds:** accepted as drafted above.
7. **Repo:** private GitHub repo `yoelgf/sueldo-justo`.
8. **Domain:** free placeholder `sueldo-justo.pages.dev` (Cloudflare Pages); buy a real domain only after a go.

## ❓ Open Questions

1. **Convenios for the check (proposed, to confirm):**

| Convenio (estatal) | Latest tables | Valid until | Note |
|---|---|---|---|
| Seguridad privada (99004615011982) | 2026, new convenio in BOE 18 Apr 2026 | 2030 | Same tables in every province; most stable choice |
| Consultoría, TI y estudios de mercado, XIX (99001355011983) | 2026–2027, adapted to SMI, BOE 24 Apr 2026 | 2027 | Tech and office jobs; an audience Yoel can reach |
| Contact center, III (99012145012002) | 2026, BOE 6 Mar 2026 | 31 Dec 2026 | High turnover, many offers; renewal due for 2027 |
| Grandes almacenes (99002405011982) | 2026, BOE 12 Feb 2026, revised June 2026 | 31 Dec 2026 | Retail; renewal due for 2027 |
| Grandes cadenas de comercio textil y calzado, I (optional 5th) | 2026–2028, BOE 30 Jul 2026 | 2028 | New convenio; fashion retail chains |

Dropped: ETT. Its estatal convenio covers the agency's own staff; workers placed at client companies are paid under the client's convenio, so it would not give the badge.

---

## 👥 Stakeholders

| Role | Name | Interest |
|------|------|----------|
| Decision maker and developer | Yoel | A clear go/no-go before spending weeks on the build |
| Target users | Job seekers in sectors with estatal convenios | Knowing if an offer pays fairly; better applications |
