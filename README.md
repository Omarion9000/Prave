<h1 align="center">PRAVÉ</h1>

<p align="center">
  <strong>Express Entry CRS optimization tool.</strong><br/>
  Calculate, simulate, and improve your Canadian permanent-residency score.
</p>

<p align="center">
  <a href="https://pravepath.ca"><img src="https://img.shields.io/badge/Live-pravepath.ca-1E4D5C?style=flat" alt="Live site" /></a>
  <img src="https://img.shields.io/badge/status-in%20production-3FCF8E?style=flat" alt="Status" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js%2016-000000?style=flat&logo=next.js&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Supabase-3FCF8E?style=flat&logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/Google%20OAuth-4285F4?style=flat&logo=google&logoColor=white" />
  <img src="https://img.shields.io/badge/Stripe-635BFF?style=flat&logo=stripe&logoColor=white" />
  <img src="https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white" />
</p>

---

<p align="center">
  <em>↓ <img width="1512" height="946" alt="Screenshot 2026-06-04 at 6 44 32 PM" src="https://github.com/user-attachments/assets/8a54eee1-0385-4b2e-b747-872ce1eb3498" />
 ↓</em>
</p>

## What it is

PRAVÉ helps Canadian Express Entry candidates understand and improve their **Comprehensive Ranking System (CRS)** score. It calculates a score against the current official rules, simulates outcomes against historical draws, and surfaces a personalized path to the next cutoff — including provincial nominee (PNP) options.

It's built to stay accurate as IRCC rules change, and to comply with Canadian immigration-advice regulations (CICC).

## Features

- **CRS calculator** aligned with current IRCC rules (including the 2025 removal of job-offer points).
- **Draw simulator** backed by **400+ historical draws**, so candidates can see where they'd land.
- **Category-based draw matching** across all official draw categories.
- **PNP matching across 11 provinces** to surface nomination pathways.
- **FSW 67-point eligibility grid** for upfront program-eligibility checks.
- **Personalized strategy engine** that maps a candidate's profile to the highest-leverage score improvements.

## Architecture

```mermaid
flowchart LR
    User([Applicant]) --> App[Next.js 16 App]
    App --> OAuth[Google OAuth]
    App --> Auth[Supabase Auth + RLS]
    App --> DB[(Supabase / Postgres)]
    App --> Pay[Stripe Billing]
    App --> Engine[CRS + Strategy Engine]
    Pipeline[IRCC JSON mirror] -->|scheduled ingest| Draws[(Historical draws)]
    Draws --> Engine
    App --> Edge[Vercel Edge / CDN]
```

A scheduled **data pipeline** ingests official IRCC draw data and feeds the **CRS and strategy engine**, which scores profiles and matches them against draw categories and provincial programs. Row-level security isolates each user's data at the database layer.

## Engineering highlights

- **Resilient data pipeline.** The original source (canada.ca) is bot-protected, so ingestion was rebuilt to pull from a structured **IRCC JSON mirror** — reliable, parseable, and resistant to layout changes.
- **OAuth with hard edge cases solved.** Google OAuth as primary auth, plus handling for the **Safari iOS PKCE flow** and detection of **in-app browsers** (Gmail / webviews) with automatic redirect to a compliant flow.
- **Row-level security** on sensitive tables so users can only ever read their own records.
- **Rules-accurate CRS engine** maintained against official IRCC point tables as policy changes.
- **Stripe subscription lifecycle** wired end to end: checkout, webhooks, billing management.

## Status

🔒 **Source is private** — PRAVÉ is a live product with active billing. This repository is a public showcase of the architecture and engineering. Try the real thing at **[pravepath.ca](https://pravepath.ca)**.

---

<p align="center">
  Built by <a href="https://omarserrano.ca">Omar Serrano</a> ·
  <a href="https://www.linkedin.com/in/omar-serrano-b40b01216/">LinkedIn</a>
</p>
