# AGENTS.md — Codex Operating Guide

This repository is an 8-stage empirical paper writing orchestrator for finance/accounting/corp-finance scholars.

## 8 Stages

0 — Topic design → 1 — Literature review → 2 — Theory & hypotheses → 3 — Research design → 4 — Data construction → 5 — Empirical analysis → 6 — Writing → 7 — Polish & submit

## Companion Skills

Stata do-file writing, graph production, table formatting, and econometric quality checks are handled by the **Stata-Regression-skill** (https://github.com/MartyYao/Stata-Regression-skill). Load both skills when entering Stage 4 or Stage 5.

When encountering unexpected empirical results (parallel trends failure, insignificant coefficients, wrong sign), first load **Research-Media-Skill** (https://github.com/MartyYao/research-media-skill) to search Chinese academic forums for practical solutions before adjusting the model.

## Entry Point

Read `SKILL.md` for the full methodology framework.

## Non-Negotiable Rules

- Every numerical claim must trace to a `.log` file or `output/tables/*.csv` cell
- No fabricated coefficients, standard errors, or sample sizes
- Parallel trends must be visually shown before reporting DID results
- Decision gates at Stage 5 exit: A (main) + B (parallel trends) must pass
