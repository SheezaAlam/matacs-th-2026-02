# AI Proposal Triage Design

**Candidate:** Sheeza Alam Khan  
**Assessment Reference:** MATACS-TH-2026-02  
**Time Actually Spent:** [50 minutes]

## Overview

This repository contains my design for an AI-assisted contractor proposal evaluation tool. The system extracts proposal information, checks mandatory requirements, calculates weighted scores and produces an explainable ranking. AI assists with reading and verifying evidence; code handles eligibility, scoring and ranking; and a human makes the final award decision.

## Submission Files

- [WRITEUP.md](matacs-th-2026-02/matacs-th-2026-02/WRITEUP.md): process decisions, explainability, human oversight and risks.
- [PROMPTS.md](matacs-th-2026-02/matacs-th-2026-02/PROMPTS.md): structured extraction and independent evidence verification.
- [ranking.json](matacs-th-2026-02/matacs-th-2026-02/ranking.json): expected results for proposals A to E.
- [diagram/flowchart.png](diagram/flowchart.png): workflow showing AI, rules and human checkpoints.

## Expected Ranking

**Proposal A: 1st (72.55) | Proposal E: 2nd, provisional (57.23) | Proposal C: Flagged | Proposal D: Flagged | Proposal B: Ineligible**

Proposal E's second-place position remains provisional until Proposal D's missing timeline is resolved.

## How I Used AI Tools

I used ChatGPT to draft the design, prompts and write-up, then reviewed and corrected its output. For example, it scored Proposal D's team and approach at 3.75 when only two of the four required items were evidenced, so I had it corrected to 2.50. I also had its original price formula replaced because it squeezed all scores into a narrow range, and I switched to Mermaid code after its image generator kept drawing one connection wrongly.

## Design Principle

**AI extracts and verifies evidence. Code calculates results. Humans make the final decision.**
