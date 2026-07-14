# Technology Guide

Phase 2 reference. Match stack to product, builder skills, and scale. **Reason about fit — don't invent dollar or week estimates.**

---

## Infrastructure cost traps

Flag these when the user's stack includes them. Describe the **mechanism** of bill shock, not precise costs.

| Choice                                  | Risk mechanism                                                    | Safer alternative (when applicable)                 |
| --------------------------------------- | ----------------------------------------------------------------- | --------------------------------------------------- |
| **AWS/GCP raw** (EC2, RDS, Lambda maze) | NAT Gateway, idle RDS, log ingestion, egress, forgotten resources | Railway, Render, Fly, Supabase, Vercel for MVP      |
| **Kubernetes** solo MVP                 | Cluster cost + ops time >> product value                          | Managed PaaS or modular monolith                    |
| **VPS self-host** (Hetzner, DO)         | 24/7 CPU (video, ML, crawlers), no autoscaling, you are on-call   | Managed services for DB/auth; VPS only if ops-savvy |
| **Open LLM proxy** (no caps)            | One user/script → unbounded token API bill                        | Server-side keys, per-user rate limits, spend caps  |
| **Client-side API keys**                | Theft → account drain                                             | Server-only keys                                    |
| **Serverless + heavy always-on work**   | WebSockets, long jobs, FFmpeg on Lambda                           | Container or dedicated worker                       |
| **S3 + heavy egress / no CDN**          | Download-heavy product without CloudFront                         | CDN or object storage with egress awareness         |
| **Realtime DB reads at scale**          | Firestore/Supabase realtime on every doc                          | Poll or SSE for MVP                                 |
| **Multiple managed SaaS** early         | Stripe + Clerk + Posthog + Intercom + ... before revenue          | Start minimal; add when needed                      |

**When to mention cost:** only if the proposed stack triggers a row above. Otherwise skip cost entirely.

---

## Fit checklist

| Question                    | ✅             | ⚠️             | ❌                     |
| --------------------------- | -------------- | -------------- | ---------------------- |
| Builder knows stack?        | Production use | Learning       | Never used             |
| Matches product shape?      | Right tool     | Tuning needed  | Wrong paradigm         |
| Right complexity for stage? | Boring MVP     | Slightly heavy | K8s for 10 users       |
| Ops burden?                 | Managed        | Some ops       | Full infra team needed |

---

## Quick picks

| Need                        | Default recommendation                         |
| --------------------------- | ---------------------------------------------- |
| Full-stack SaaS MVP         | Next.js + Supabase + Vercel                    |
| Mobile-first                | Expo + Supabase or Firebase                    |
| Content / marketing site    | Astro or Next static                           |
| Internal tool, one dev      | Next.js or SvelteKit + SQLite/Postgres         |
| Heavy background jobs       | Postgres + worker (Inngest, Bull, Trigger.dev) |
| AI feature (not AI product) | Server-side API call, not product core         |

---

## Common mismatches

| They chose          | Problem                   | Suggest                     |
| ------------------- | ------------------------- | --------------------------- |
| Microservices + K8s | Ops >> MVP                | Monolith on PaaS            |
| MongoDB             | Complex relations / money | Postgres                    |
| Firebase            | Heavy reporting / SQL     | Supabase/Postgres           |
| AWS from day 1      | Complexity, bill surprise | Managed PaaS until traction |
| GraphQL             | 3 endpoints               | REST or tRPC                |
| Roll-your-own auth  | Weeks lost                | Clerk / Supabase Auth       |

---

## AI products

| Pattern               | Moat   | Cost trap                                    |
| --------------------- | ------ | -------------------------------------------- |
| API wrapper           | None   | Token spend with no pricing power            |
| RAG on public data    | Weak   | Embedding + retrieval + generation per query |
| Proprietary data loop | Medium | Worth building if data is exclusive          |

Flag wrapper pattern in Phase 7. Require server-side keys and rate limits if AI is used.

---

## Output template

```markdown
**Stack fit:** ✅ / ⚠️ / ❌
**Strengths:** ·
**Concerns:** ·
**Cost traps:** [mechanism-based, or "none identified"]
**Recommended stack:** [if missing or mismatch]
```
