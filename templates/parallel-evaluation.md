# Parallel Evaluation — Subagent Briefs

Use after Phase 1 confirmation. Launch **all applicable subagents in one parallel batch** (e.g. Cursor `Task` tool), then synthesize before personas meet.

**Fallback:** If subagent/Task tools are unavailable, run the same briefs sequentially yourself — do not skip domains.

---

## Context packet (include in every subagent prompt)

```markdown
## Idea brief

- Product: [one sentence]
- Customer / payer: [...]
- Problem: [...]
- Intent: personal / side project / startup
- Maturity: A / B / C / D / E
- Stack (if any): [...]
- Plan/repo (if any): [summary or link]
- Skills/constraints: [...]
```

---

## Subagent 1 — Stack & technology

**subagent_type:** `generalPurpose` or `explore`  
**readonly:** true

**Prompt:**

> Evaluate stack fit for this idea. Read technology-guide patterns from the vibe-check skill references if available.
>
> - If no stack: recommend a concrete MVP stack matched to builder skills and product shape.
> - If stack proposed: rate fit ✅/⚠️/❌, suggest swaps, flag infrastructure **cost traps** (AWS/K8s/VPS/LLM proxy mechanisms only — no dollar estimates).
>   Return: fit rating, recommended stack table, cost traps (or none), top 3 stack concerns.

---

## Subagent 2 — Security

**subagent_type:** `generalPurpose`  
**readonly:** true

**Prompt:**

> Security review for this idea and stack. Check auth, secrets, RLS/rules, AI key exposure, PII, rate limits.
> Return: 🔴 critical, 🟡 important, 🟢 good-practice items — each with one-line fix. Flag blockers for MVP.

---

## Subagent 3 — Competitors

**subagent_type:** `explore` or `generalPurpose`  
**readonly:** true

**Prompt:**

> Web search required. Find direct and adjacent competitors, OSS repos, AI-wrapper clones in this niche.
> Return: table (name, URL, strength, gap), saturation level, whether a wedge exists. If 10+ mature players and no wedge, say so explicitly.

---

## Subagent 4 — Plan & architecture _(Level C/D/E only)_

**subagent_type:** `explore`  
**readonly:** true

**Prompt:**

> Review the user's plan, feature list, architecture, or repo against MVP discipline.
> Return: top 5 plan/architecture fixes (current → issue → fix → priority), features to cut from v1, what to keep.

---

## Orchestrator synthesis (after all subagents return)

Merge into an internal **Evaluation Brief** before personas meet:

```markdown
## Evaluation Brief (internal)

### Stack

[subagent 1 summary]

### Security

[subagent 2 summary]

### Competitors

[subagent 3 summary]

### Plan fixes (if any)

[subagent 4 summary]
```

Do **not** show the raw Evaluation Brief to the user. Personas and final report consume it.

---

## Parallel launch example (Cursor)

Send one message with multiple Task calls:

```
Task: Stack evaluation — [paste context packet + Subagent 1 prompt]
Task: Security review — [paste context packet + Subagent 2 prompt]
Task: Competitor research — [paste context packet + Subagent 3 prompt]
```

Wait for all to complete → write Evaluation Brief → proceed to persona panel.
