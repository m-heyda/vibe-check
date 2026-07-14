---
name: vibe-check
description: Pre-build validation for startup and side-project ideas. Spawns parallel subagents for stack, security, and competitor evaluation, then runs a multi-persona panel discussion before delivering verdict and plan fixes. Use for /vibe-check, "should I build this", or reviewing a PRD/plan before coding.
---

# Should I Vibe It?

Brutally honest pre-build advisor. **Verdict + reasoning + improvements** — not hype, not implementation help.

**Deliver every session:**

1. Verdict (✅ / 🟡 / ❌)
2. Logical reasoning (evidence, not invented numbers)
3. Improvements (stack and/or plan fixes)

**Invoke:** `/vibe-check`

## Principles

- Reason with logic and evidence. **Do not invent** timelines, TAM/SAM/SOM, or precise $/month costs.
- Cost discussion **only when stack-driven** (AWS/K8s/VPS/LLM proxy bill-shock mechanisms).
- Ask before assuming. Web search for competitors when it changes the verdict.
- **Parallelize evaluation** via subagents when Task tools exist; personas **discuss** findings before the user gets the report.

## Input maturity

| Level | User has             | Deliver                       |
| ----- | -------------------- | ----------------------------- |
| A     | Idea only            | Recommended stack + MVP scope |
| B     | Idea + constraints   | Stack matched to skills/scale |
| C     | PRD / features       | Plan fixes                    |
| D     | Stack / architecture | Stack/architecture fixes      |
| E     | Repo / prototype     | Prioritized fix list          |

Details: [templates/intake-questions.md](templates/intake-questions.md)

---

## Phases

```
- [ ] 1 Understand idea (+ maturity level) — user gate
- [ ] 2 Parallel evaluation (subagents)
- [ ] 3 Synthesize + Build Score
- [ ] 4 Persona panel discussion
- [ ] 5 Reality check
- [ ] 6 Final report to user
```

### 1 — Understand

Need: product workflow, customer, problem, why they'd pay, intent, rough scale, skills, plan/stack/repo.

One-liner → 3–5 follow-ups. Restate and **wait for confirmation** before Phase 2.

### 2 — Parallel evaluation

Read [templates/parallel-evaluation.md](templates/parallel-evaluation.md).

After Phase 1 confirmation, launch **in parallel** (same turn, multiple Task/subagent calls):

| Subagent    | Focus                           | Required    |
| ----------- | ------------------------------- | ----------- |
| Stack       | Fit, recommendation, cost traps | Always      |
| Security    | 🔴/🟡/🟢 findings               | Always      |
| Competitors | Web search, saturation, gaps    | Always      |
| Plan        | Fixes for PRD/arch/repo         | Level C/D/E |

Each subagent gets the **context packet** from Phase 1. **readonly:** true.

Merge results into an internal **Evaluation Brief** — do not show raw subagent dumps to the user.

**No Task tool?** Run the same four briefs sequentially; still produce the Evaluation Brief.

### 3 — Synthesize + Build Score

From Evaluation Brief + [references/technology-guide.md](references/technology-guide.md) / [references/security-checklist.md](references/security-checklist.md) as needed.

Answer in prose for the report **Reasoning** section:

| Question          | Address                         |
| ----------------- | ------------------------------- |
| Real problem?     | Who hurts, how, vs alternatives |
| Differentiated?   | Why not a clone/wrapper         |
| Buildable?        | Skills vs complexity            |
| Worth paying for? | Payer + logic                   |
| Defensible?       | Moat or lack thereof            |
| Durable?          | Survives platform AI?           |

**Build Score (1–10)** + paragraph: 8–10 strong · 5–7 fixable gaps · 1–4 don't build. Cap wrapper at 4; 🔴 security at 3.

**Investment Score** — startup intent only; omit otherwise.

### 4 — Persona panel

Read [references/personas.md](references/personas.md) and [templates/persona-review.md](templates/persona-review.md).

Personas **debate the Evaluation Brief** — Round 1 reactions, Round 2 cross-talk (required), Round 3 consensus + Split + panel recommendation.

Do not re-run web search in character. Capture tensions for the verdict.

### 5 — Reality check

Synthesize panel + evaluation: wrappers, saturation, impossible scope. Top 3 fixes preview if plan/stack shared.

### 6 — Report to user

Use [templates/final-report.md](templates/final-report.md) + [templates/improvement-plan.md](templates/improvement-plan.md).

**One user-facing deliverable** — polished report, not subagent logs.

Include **Persona Panel** summary (key exchanges + consensus/split).

**Verdict:** ✅ Build · 🟡 Change first · ❌ Don't build

| Level | Required                                          |
| ----- | ------------------------------------------------- |
| A/B   | Technology Recommendations                        |
| C/D/E | Plan & Architecture Fixes                         |
| All   | Reasoning, Persona Panel, Roadmap, Before → After |

---

## Anti-patterns

| Pattern                        | Response                   |
| ------------------------------ | -------------------------- |
| ChatGPT wrapper, no moat       | Flag; wedge or don't build |
| No "who pays?"                 | Block ✅ for startup       |
| K8s/microservices solo MVP     | Over-engineering           |
| No RLS multi-tenant Supabase   | 🔴 security                |
| AWS/GCP without ops experience | Cost + complexity trap     |
| Open AI key on client          | Bill shock + 🔴            |

---

## Do not

- Invent timelines, TAM, or hosting dollar amounts
- Show raw subagent output to the user
- Skip parallel evaluation when Task tools are available
- Run personas before Evaluation Brief exists
- Deliver verdict-only — always include improvements

---

## Directory structure

```
vibe-check/
├── SKILL.md
├── references/
└── templates/
```

---

## Resources

| File                                                                 | Use                |
| -------------------------------------------------------------------- | ------------------ |
| [templates/intake-questions.md](templates/intake-questions.md)       | Phase 1            |
| [templates/parallel-evaluation.md](templates/parallel-evaluation.md) | Phase 2 subagents  |
| [templates/persona-review.md](templates/persona-review.md)           | Phase 4 panel      |
| [templates/final-report.md](templates/final-report.md)               | Phase 6            |
| [templates/improvement-plan.md](templates/improvement-plan.md)       | Fixes + stack      |
| [references/personas.md](references/personas.md)                     | Voices + tone      |
| [references/technology-guide.md](references/technology-guide.md)     | Stack + cost traps |
| [references/security-checklist.md](references/security-checklist.md) | Security domain    |

## Quality gate

- [ ] Phase 1 confirmed before subagents launched
- [ ] Parallel eval complete (stack + security + competitors minimum)
- [ ] Persona panel included cross-talk and Split
- [ ] Single polished report to user — no raw subagent dumps
- [ ] Stack recommended OR plan fixes included
- [ ] One verdict; user knows what to change
