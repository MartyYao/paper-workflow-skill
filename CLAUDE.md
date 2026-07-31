# CLAUDE.md — Paper Workflow for Economists

## Core Principles

- **Plan first** — read SKILL.md, identify current phase, check the dashboard
- **Verify after** — run the do-file, inspect the log, confirm output exists  
- **Companion skill** — Stata work uses Stata-Regression-skill; load it for phases 4-5
- **No log, no claim** — every numerical result must trace to a log or CSV

## Quick Reference

| Phase | Action |
|-------|--------|
| 0 — Topic design | Read SKILL.md §0, follow structured dialogue |
| 1 — Literature | Multi-channel search → Zotero → thematic review |
| 2 — Theory | Institutional background → theoretical deduction → H1-H3 |
| 3 — Research design | ID strategy audit → variable construction plan |
| 4 — Data (Stata) | **Load Stata-Regression-skill** → do-file template → clean → construct |
| 5 — Empirical (Stata) | **Load Stata-Regression-skill** → regressions → graphs → tables → decision gate. Unexpected results → **load Research-Discovery-skill** (diagnose → decide → archive F-xxx in Obsidian 研究发现/) |
| 6 — Writing | Research design first → results → theory → intro → conclusion |
| 7 — Polish | 5-stage pipeline → journal matching |

## Key Decision Gate

Stage 5 exit requires: A (main results p<0.05, correct sign) + B (parallel trends pass). C/D/E partial failure → continue with caveats. A or B fail → roll back to Stage 3 or 4.

## Non-Negotiable Rules

- All regression tables: 4 decimals, t-values in parentheses, **no** ✓ for controls
- Graphs: RGB 49 145 255 for focal series, 142 164 184 for comparison, export PDF+PNG
- Cluster SE at the most aggregate plausible level; report cluster count
