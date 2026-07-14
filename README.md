# Should I Vibe It?

Pre-build validation for startup and side-project ideas — **before** you vibe code the wrong thing.

`/vibe-check` returns a verdict, **logical reasoning**, competitor research, security flags, and concrete improvements (stack recommendation or plan fixes). No fake revenue projections or invented timelines.

---

## What you get

| Output             | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| **Verdict**        | ✅ Build · 🟡 Change first · ❌ Don't build                           |
| **Reasoning**      | Evidence-based argument — problem, differentiation, feasibility       |
| **Competitors**    | Links, saturation, gaps                                               |
| **Security**       | Critical issues before you code                                       |
| **Stack guidance** | Recommendation if none chosen; fixes if wrong fit                     |
| **Cost traps**     | Only when your stack risks bill shock (AWS, VPS, open AI proxy, etc.) |
| **Plan fixes**     | If you shared a PRD, architecture, or repo                            |
| **Persona panel**  | Experts discuss subagent findings — agreements and splits             |
| **Roadmap**        | Three next steps                                                      |

Parallel subagents evaluate stack, security, and competitors at the same time; personas then debate before your report is written.

---

## Structure

```
vibe-check/
├── SKILL.md          # Workflow and rules
├── references/       # Personas, security, stack guide
└── templates/        # Report and intake formats
```

---

## Install

```bash
npx skills add m-heyda/vibe-check --skill vibe-check -y
```

**Cursor · Claude Code · Codex · Copilot** and [17+ agents](https://skills.sh) via [Agent Skills](https://agentskills.io).

**Claude.ai:** Download ZIP → Settings → Capabilities → Skills → Upload.

---

## Usage

```
/vibe-check

[Describe your idea — add PRD, stack, or repo link if you have them]
```

**Idea only:** marketplace for videographers, solo dev, no stack chosen.

**With plan:** paste PRD + `Next.js + Supabase` — get plan fixes and stack fit.

**With repo:** link + "should I keep going?" — get prioritized fixes.

---

## Requirements

- Agent Skills-compatible agent
- Web search (competitor research)
- Subagent/Task support recommended (Cursor, Claude Code) for parallel evaluation — falls back to sequential if unavailable
