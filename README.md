## Submission Information

**Submitted by:** Muhammad Haris  
**Assessment Reference:** MATACS-TH-2026-02  
**Time Spent:** 2 hours

### Repository Files

| File | Description |
|---|---|
| [README.md](README.md) | System overview, workflow, evaluation methodology, and AI usage |
| [ranking.json](ranking.json) | Structured evaluation results for all five proposals |
| [proposal_triage_process_flow.png](proposal_triage_process_flow.png) | End-to-end workflow showing AI steps, rule-based processing, and human checkpoints |
| [assessment_report.md](assessment_report.md) | Detailed proposal rankings, scores, eligibility decisions, and explanations |


### AI Tool Usage

I used ChatGPT to help structure the evaluation methodology, review scoring calculations, design the AI-assisted extraction and validation workflow, and document the system. I independently reviewed the proposed logic and corrected the approach to ensure that mandatory eligibility checks, weighted scoring, and ranking are deterministic rule-based operations rather than decisions made by the LLM.

**Correction and independent judgment:** I disagreed with treating missing or uncertain information as a score of zero or automatically rejecting a proposal. Instead, I implemented a human-review pathway for unresolved mandatory requirements and incomplete weighted evaluations, preventing unsupported assumptions from affecting proposal rankings.
