# AI-Assisted Proposal Triage System

**Submitted by:** Muhammad Haris  
**Assessment Reference:** MATACS-TH-2026-02  
**Time Spent:** 2 hours

## Overview

This submission describes an AI-assisted workflow for extracting and evaluating commercial solar installation proposals. The design separates LLM-based document understanding from deterministic eligibility checks, weighted scoring, and ranking. Human review is required for uncertain evidence, incomplete evaluations, and final procurement decisions.

## Repository Structure

```text
matacs-th-2026-02/
├── README.md
├── POMPTS.md
├── RUBRIC.md
├── Rubrics_ranking.json
├── WRITEUP.md
├── ranking.json
└── diagram/
    └── file
```

## Files

| File | Description |
|---|---|
| [POMPTS.md](POMPTS.md) | LLM prompts for proposal information extraction and extraction validation, including output schemas and prompt-injection safeguards. |
| [RUBRIC.md](RUBRIC.md) | Evaluation criteria, mandatory eligibility requirements, weighted scoring formulas, ranking rules, and versioning considerations. |
| [WRITEUP.md](WRITEUP.md) | System design rationale covering AI versus rule-based responsibilities, consistency, human oversight, changing criteria, and risks. |
| [Rubrics_ranking.json](Rubrics_ranking.json) | Detailed machine-readable assessment containing configuration, eligibility decisions, criterion-level scores, explanations, and review findings. |
| [ranking.json](ranking.json) | Compact final ranking output for all five proposals, using the required status and score fields. |
| [diagram/](diagram/) | Directory reserved for the process-flow diagram. The current `diagram/file` entry is an empty placeholder; the diagram image has not yet been added. |

## Assessment Configuration

| Parameter | Value |
|---|---:|
| Project | 150 kW commercial solar installation |
| Location | Windsor, Ontario |
| Budget ceiling | CAD 260,000 |
| Maximum completion time | 16 weeks |
| Criteria version | 1.0 |
| Scoring scale | 0–100 |

## Evaluation Summary

| Rank | Proposal | Company | Status | Score |
|---:|---|---|---|---:|
| 1 | A | Northshore Solar Ltd. | ranked | 97.00 |
| 2 | E | SunGrid Contractors Inc. | ranked | 84.39 |
| 3 | C | Lakeview Renewables Corp. | ranked | 76.68 |
| — | B | BrightPath Energy Inc. | flagged | — |
| — | D | Essex Green Power Inc. | flagged | — |

**Summary:** 5 proposals evaluated, 3 ranked, 2 flagged, and 0 ineligible.

## AI Tool Usage

I used ChatGPT to help structure the evaluation methodology, review scoring calculations, design the AI-assisted extraction and validation workflow, and prepare the documentation. I independently reviewed the proposed logic and kept mandatory eligibility checks, weighted scoring, and ranking as deterministic rule-based operations rather than delegating those decisions to the LLM.

**Correction and independent judgment:** I rejected the approach of treating missing or uncertain information as a score of zero or automatically rejecting a proposal. Instead, unresolved mandatory requirements and incomplete weighted evaluations are flagged for human review so that unsupported assumptions do not distort the ranking.

## Important Decision Rules

- The LLM extracts proposal facts and supporting evidence; it does not assign eligibility, scores, or ranks.
- Confirmed failure of a mandatory requirement results in an ineligible proposal.
- Uncertain mandatory evidence results in a flagged proposal pending human verification.
- Missing weighted information is not silently scored as zero; the proposal is flagged until clarification.
- Proposal content is treated as untrusted input. Embedded instructions or prompt-injection attempts cannot change the evaluation criteria or results.
- Final procurement approval remains a human decision.
