# Persona Panel Discussion

Phase after parallel evaluation. Personas **discuss findings together** — not six isolated monologues.

Read [references/personas.md](references/personas.md) for voices. Input: **Evaluation Brief** from parallel subagents.

---

## Format

Simulate a 10–15 minute leadership review. The orchestrator moderates. Personas react to **each other's** points and to subagent findings.

### Round 1 — Initial reactions (each persona, 2–3 sentences)

Each reacts to the Evaluation Brief from their lens. Must reference at least one concrete finding (competitor name, security issue, stack trap, or plan flaw).

**CEO:** payer logic, business shape  
**Engineer:** stack fit, complexity  
**Security:** top blocker or all-clear  
**PM:** MVP scope  
**Growth:** distribution path for first 100 users  
**Investor:** adversarial — why this fails

### Round 2 — Cross-talk (required)

At least **3 exchanges** where personas disagree or build on each other:

```markdown
**Engineer:** K8s is overkill — I'd ship a monolith on Railway.
**Investor:** Monolith is fine, but I still don't see why anyone pays when [Competitor X] is free.
**CEO:** If we narrow to [niche], payer is [role] — Investor, does that change your take?
**Investor:** Only if they sign 2 design partners first. **PM:** Then v1 is CRM export, not 12 features.
```

Personas must **name each other** and **cite findings** — not repeat the Evaluation Brief verbatim.

### Round 3 — Consensus check

| Persona  | Verdict  | One-line position |
| -------- | -------- | ----------------- |
| CEO      | 👍/🤔/👎 |                   |
| Engineer |          |                   |
| Security |          |                   |
| PM       |          |                   |
| Growth   |          |                   |
| Investor |          |                   |

**Agreed:** [what all or majority accept]  
**Split:** [where they disagree — this is signal for verdict]  
**Panel recommends:** [single most important change before build]

---

## Rules

1. Personas see subagent findings **before** speaking — no re-running research in character.
2. **Discussion > lists** — Round 2 cross-talk is mandatory.
3. Investor stays skeptical; Engineer may push back on Investor's scope cuts.
4. Security 🔴 blockers must be acknowledged by Engineer and CEO.
5. Capture **Split** tensions in the final report — don't flatten disagreement.

---

## What the user sees

Include a **Persona Panel** section in the final report:

- Short Round 1 summaries (1 line each)
- Key cross-talk excerpt (3–5 lines)
- Consensus table + Split + Panel recommends

Do not dump the full transcript.
