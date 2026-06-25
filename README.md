# CoachFile

> Never walk into a client session cold again. CoachFile is a private client-memory system that turns a coach's scattered notes into organized, searchable client timelines, session prep, and follow-up discipline.

![Status](https://img.shields.io/badge/status-live-2ea44f)
![Platform](https://img.shields.io/badge/platform-web-0a66c2)
![AI](https://img.shields.io/badge/AI-Claude%20(Anthropic)-7a5cff)
![Stack](https://img.shields.io/badge/stack-Next.js%20%C2%B7%20Supabase%20%C2%B7%20Cloudflare-000000)
![License](https://img.shields.io/badge/license-proprietary-8a8a8a)

**Live:** [coachfile.app](https://coachfile.app)  ·  **Source is private by design** — public showcase only.

![CoachFile](assets/hero.png)

---

## The problem
A coach's most valuable asset is what they remember about each client, and that memory is scattered across Word docs, Google Docs, and unstructured folders. The real incumbent isn't another app — it's "files + folders + memory," and it doesn't scale. So coaches walk into sessions cold.

## What it does
- **AI migration (the wedge).** Drop in your existing notes (Word, PDF, or text files). CoachFile extracts an organized client record, with every field traced back to its source line.
- **Client memory.** Searchable timelines, custom fields, full session history.
- **Session prep + follow-up loops.** Weekly habits that keep coaches close to their clients: a prep brief before a session, a capture nudge after one, and a follow-up reminder when a client goes quiet.

## The principle: organize, don't invent
The AI **structures what a coach actually wrote.** It never fabricates a name, a date, or a detail. Every extracted field carries a **source citation**, sensitive content is **flagged for human review**, and nothing becomes a record until the coach **approves** it. For a tool that holds real information about real relationships, faithfulness is the whole product.

## How it's built
```mermaid
flowchart LR
    UP["Coach uploads notes<br/>.docx · .pdf · .txt"] --> R2[("Cloudflare R2")]
    R2 --> Q[["Extraction queue<br/>Cloudflare Worker"]]
    Q --> EX["Claude extracts client + sessions<br/>with source citations"]
    EX --> RV["Review queue<br/>source + draft, side by side"]
    RV -->|coach approves| DB[("Encrypted client record<br/>Supabase + Row-Level Security")]
    EX -. flags .-> SENS["Sensitive content<br/>held for review"]
    DB --> LOOPS["Weekly loops<br/>prep · capture · follow-up"]
```

## Security
- **Encrypted at rest** (AES-256), with **column-level encryption** on the most sensitive fields (client names, notes, extracted data).
- **Row-Level Security** enforces strict per-coach tenant isolation, verified on every change.
- **Two-tier model:** no standing engineer access to client data; clinical / emergency use is out of scope by design.

## Tech
| Layer | Stack |
|---|---|
| App | Next.js 15 (App Router, TypeScript) |
| Data | Supabase Postgres + Row-Level Security |
| Auth | Clerk |
| Edge | Cloudflare Workers (OpenNext) · R2 · Queues · KV |
| AI | Claude (Anthropic) — source-cited extraction |
| Payments / Email / Observability | Stripe · Resend · Sentry |

## Status
Live at **[coachfile.app](https://coachfile.app)**. Co-founded and built in partnership with a bestselling author and coach. Shipped: the AI migration tool, client + session management, custom fields, billing, the three retention loops, and column-level encryption.

---

Built by **Jesse Jolly** · [SFX Tech Innovation](https://sfxtechinnovation.com) · [LinkedIn](https://linkedin.com/in/jessegjolly)

*Source code is private and proprietary. This repository showcases the product and its architecture only.*
