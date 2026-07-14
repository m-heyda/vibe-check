# Security Checklist

Use in Phase 3. Adapt checks to the stated stack. Flag issues even if stack is undecided — note "required regardless of stack."

## Contents

- Universal checks (all projects)
- Supabase
- Firebase
- PostgreSQL (self-hosted / Railway / RDS)
- Next.js / full-stack JS
- AI / LLM integrations
- Mobile apps
- GDPR & privacy baseline

---

## Universal checks (all projects)

| Check              | Pass criteria                                       | Common failure                             |
| ------------------ | --------------------------------------------------- | ------------------------------------------ |
| Authentication     | Every protected resource requires verified identity | "Security through obscurity" URLs          |
| Authorization      | Users access only their own data (server-enforced)  | Client-only permission checks              |
| Secrets management | API keys in env/secrets manager, never in repo      | Keys in `.env` committed to GitHub         |
| Input validation   | All user input validated server-side                | Trusting client JSON                       |
| Rate limiting      | Auth, write, and AI endpoints rate-limited          | Unlimited OpenAI proxy                     |
| HTTPS              | TLS everywhere in production                        | HTTP API in prod                           |
| Dependency hygiene | Dependabot/Snyk, no known critical CVEs             | Ignored npm audit                          |
| Logging            | No secrets/PII in logs; structured errors           | Logging full JWT payloads                  |
| Backups            | Database backup + tested restore                    | "Supabase handles it" without verification |
| Incident plan      | Know how to rotate keys and notify users            | No runbook                                 |

---

## Supabase

| Check               | Detail                                                        |
| ------------------- | ------------------------------------------------------------- |
| RLS enabled         | RLS ON for every table with user data — no exceptions         |
| RLS policies tested | Test as anon, authenticated user A, user B — verify isolation |
| Service role        | NEVER in client, mobile, or browser; server/edge only         |
| Storage policies    | Bucket policies mirror table RLS; no public write buckets     |
| Auth design         | Use Supabase Auth; don't roll custom JWT unless necessary     |
| Edge functions      | Validate JWT inside function; don't trust client claims alone |
| SQL injection       | Parameterized queries only; no string-concat SQL in RPC       |
| Realtime            | Channel authorization matches RLS intent                      |
| Webhooks            | Verify signatures; idempotent handlers                        |

**Instant reject:** "I'll add RLS later" on a multi-tenant SaaS.

---

## Firebase

| Check              | Detail                                            |
| ------------------ | ------------------------------------------------- |
| Security rules     | Not `allow read, write: if true` in production    |
| Rules unit tests   | Firebase emulator tests for auth boundaries       |
| Admin SDK          | Server-only; never ship service account to client |
| Storage rules      | Match Firestore auth model                        |
| Callable functions | Auth check at function entry                      |
| App Check          | Consider for abuse-prone apps                     |

**Instant reject:** Open Firestore rules "for development" shipping to prod.

---

## PostgreSQL (self-hosted)

| Check              | Detail                                      |
| ------------------ | ------------------------------------------- |
| Connection pooling | PgBouncer or equivalent at scale            |
| Least privilege    | App role ≠ superuser                        |
| Row-level security | If multi-tenant and ORM bypasses app layer  |
| Migrations         | Versioned, reversible, no manual prod edits |
| Encryption at rest | Provider-managed or disk encryption         |
| Network            | DB not publicly accessible                  |

---

## Next.js / full-stack JS

| Check            | Detail                                                          |
| ---------------- | --------------------------------------------------------------- |
| Server vs client | Secrets and DB calls in Server Components / Route Handlers only |
| API routes       | Auth middleware on all mutating routes                          |
| CSRF             | Protection on cookie-based auth forms                           |
| XSS              | Sanitize user HTML; CSP headers                                 |
| SSRF             | Validate URLs if fetching user-supplied links                   |
| Env vars         | `NEXT_PUBLIC_` only for truly public values                     |

---

## AI / LLM integrations

| Check             | Detail                                              |
| ----------------- | --------------------------------------------------- |
| API key exposure  | Keys server-side only; never proxy wide-open        |
| Prompt injection  | Treat user content as untrusted; sandbox tool calls |
| Cost caps         | Per-user and global spend limits                    |
| Output validation | Don't execute LLM-generated code without sandbox    |
| Data retention    | Don't send PII to models without DPA/consent        |
| Abuse             | Rate limit; monitor for prompt spam / token farming |

**Instant reject:** Client-side OpenAI key "for simplicity."

---

## Mobile apps

| Check               | Detail                                                 |
| ------------------- | ------------------------------------------------------ |
| Certificate pinning | Consider for high-security apps                        |
| Local storage       | No secrets in AsyncStorage/Keychain without encryption |
| API auth            | Short-lived tokens; refresh rotation                   |
| Reverse engineering | Assume attacker has APK/IPA                            |

---

## GDPR & privacy baseline

| Requirement         | MVP minimum                                                        |
| ------------------- | ------------------------------------------------------------------ |
| Lawful basis        | Know why you process data (contract, consent, legitimate interest) |
| Privacy policy      | Required before collecting EU personal data                        |
| Data minimization   | Collect only what you need                                         |
| Right to deletion   | Mechanism to delete user account + data                            |
| Data processors     | DPAs with Supabase, OpenAI, analytics vendors                      |
| Breach notification | 72-hour plan for EU incidents                                      |
| Cookies             | Consent banner if non-essential cookies (EU)                       |

**Note:** GDPR applies to EU users regardless of where the founder lives.

---

## Severity guide

| Level            | Criteria                                | Action                          |
| ---------------- | --------------------------------------- | ------------------------------- |
| 🔴 Critical      | Data breach likely; blocks safe MVP     | Fix before writing product code |
| 🟡 Important     | Exploitable with effort; compliance gap | Fix before public launch        |
| 🟢 Good practice | Hardening, monitoring, maturity         | Schedule post-MVP               |
