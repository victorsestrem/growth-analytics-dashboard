# Growth Analytics Dashboard — Case Study

> Internal growth dashboard I built for **Vale Verde Festas** with marketing campaign and messaging-blast metrics pulled from the Kommo CRM API.
> **Source code is private.** This repository documents the project; a live walkthrough is available on request.

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS_11-E0234E?logo=nestjs&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000?logo=nextdotjs)
![TanStack Query](https://img.shields.io/badge/TanStack_Query-FF4154?logo=reactquery&logoColor=white)

## The problem

Marketing and sales leadership needed to see, in one place, how each campaign and each WhatsApp blast performed — leads, sources, conversions — without exporting data from the CRM by hand every week.

## What I built

- **Campaigns** and **Blasts** views with filters by period, campaign, source and blast.
- **Automatic refresh** every morning at 08:00 (Brasília) plus an on-demand "Refresh now".
- **Print** (A4 landscape) and **Export to Excel** — one sheet per view, only the filtered data.
- **Read-only by design**: the dashboard never writes back to the CRM.

## Architecture

```mermaid
flowchart LR
  K[Kommo CRM API] -->|scheduled + on-demand sync| API[NestJS API<br/>collection, business rules, .xlsx]
  API --> W[Next.js dashboard<br/>TanStack Query]
  API --> X[Excel export<br/>ExcelJS]
```

- Business rules documented per column (where each number comes from).
- **Fake Kommo server** with invented data for local development and tests — no real customer data ever needed on a developer machine.
- Verification script that compares a real week against the expected counts (read-only).
- Secrets only in the server's `.env`, Argon2 password hashing.

## My role

Requirements with marketing and sales, data rules, API integration, UI, exports and tests.

---
Built by **Victor Sestrem** · [LinkedIn](https://www.linkedin.com/in/victor-sestrem/) · victor-sestrem@hotmail.com
