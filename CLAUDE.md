# Sueldo Justo — Developer Guide

A Spanish job app for the whole job lifecycle. Job seekers paste an offer (a swipe deck comes once a legal job feed exists) and see a salary badge from their convenio colectivo, get an AI-tailored CV and carta for every offer, and keep using the app after they are hired to check their contract, nóminas and finiquito.

Name chosen 2026-11-12 (earlier working name: Curro). Placeholder domain: sueldo-justo.pages.dev.

## 📋 Project Overview

- **Market:** the whole of Spain. Convenio coverage grows in stages: state-wide (estatal) convenios first, then the provincial convenios of the biggest job markets (Madrid, Barcelona, Valencia, Málaga, Sevilla), then Cataluña in depth, then the rest.
- **Language:** Spanish at launch; all user-facing text lives in string files (Catalan later).
- **Monetisation (to test):** weekly subscription while job hunting, one-off checks (contract, nómina, finiquito), a monthly plan after hiring, lawyer referral fees, and a free tier (unlimited salary badges + 3 tailored CVs a week).
- **Proposal doc:** https://claude.ai/artifact/MUUgk5RfiJiMF8huLU9JQF
- **Research:** `docs/research/` (job-market pain points, Sprout teardown, combined concept; 2026-11-12).

## 🛠️ Tech Stack (decided in spec 002)

| Layer | Technology |
|-------|-----------|
| Language | TypeScript (strict) |
| App | Preact + Vite, installable PWA; Capacitor iPhone app later |
| Backend | Cloudflare Workers (API under `/api`) + Pages |
| Database | Cloudflare D1 (users, profiles, applications); migrations in the repo |
| Convenio knowledge base | Typed data files in `data/convenios/` |
| AI | Claude via one backend LLM gateway; keys only in Worker secrets; €20/month spend cap |
| Login | Email magic link sent with Resend (EU) |
| Tests | Vitest |

## 📐 Code Conventions

- **Every salary figure cites its source:** convenio name, bulletin (BOE, DOGC, BOP…), year of the table and an as-of date. No uncited numbers in the UI.
- **Checks are guidance, not legal advice:** label them "orientativo"; serious cases point to an employment lawyer.
- **No scraping and no auto-apply.** Offers come from legal feeds; the user sends each application themselves.
- **Personal data is minimal:** CVs, contracts and nóminas are processed for the check and not kept unless the user saves them. GDPR first; never log document contents.
- **AI runs only where it is the core value** (tailoring, document checks), and its cost per use must be covered by the pricing. Deterministic rules (convenio minimums, net pay, indemnización formulas) are plain code, tested, not AI.
- **Content as data:** convenio tables, categories and strings live in typed data files, not in code branches.

## 🔄 Methodology

AIDLC, same as Litoral and Idle Love & Lava. Specs live in `docs/specs/` (registry: `docs/specs/index.md`). One spec at a time: draft → challenge → lock → build.

---

**Last Updated:** 2026-11-12
