# AI Proposal Triage Design

**Assessment Reference:** MATACS-TH-2026-02

## 1. AI vs. Rules

The system will use AI for the extraction of the valuable information from the documents that will be submitted by the reviewer. The documents contain unstructured text, different writing styles and unformatted/varying versions. So, we will involve AI for getting the text, idea, general concept from the documents according to the requirements that we set.

The workflow will split between two parts: the first one is the information extraction where we will involve AI while the second one is the evaluation where we will incorporate the rubrics using python scripts and calculations.

- **Document processing:** Text will be extracted using a PDF parser and a fallback 
- **AI extraction:** It will include the extraction of licences, insurance, experience, price, timeline, warranties, and project team details. Each extracted field by the LLM must include supporting evidence and a page reference while the missing or ambiguous information is returned as unknown rather than inferred.
- **Validation:** The code will perform a strict validation test against pre-defined schema and evidences completeness will be checked.
- **Mandatory evaluation:** A rules engine checks the two mandatory requirements: the bidder's Ontario electrical contractor licence, and confirmation of both WSIB clearance and $5M liability insurance.
- **Weighted scoring:** A conventional code calculates criterion scores and the final weighted score using administrator-defined criteria and weights.
- **Ranking:** All the eligible proposals are sorted by their calculated scores along with explanations generated from the underlying evidence and score breakdown.

AI is used where language understanding is valuable. Rules are used for eligibility, calculations, and ranking because these operations must be predictable, testable, and repeatable.

## 2. Consistency and Explainability

The system uses a versioned scoring configuration and deterministic scoring rules to ensure repeatable results. Given identical proposal data, criteria, and scoring configuration, the system should produce identical scores and rankings.

The weighted criteria are:

| Criterion | Weight |
|---|---:|
| Relevant experience | 30% |
| Price | 25% |
| Timeline | 15% |
| Warranty | 15% |
| Team and approach | 15% |
| **Total** | **100%** |

Each criterion receives a score between 0 and 100. The final score is calculated as:

`Final Score = (Experience × 0.30) + (Price × 0.25) + (Timeline × 0.15) + (Warranty × 0.15) + (Team × 0.15)`

The proposed scoring rules use a capped experience score based on qualifying installations, relative price scoring against the lowest eligible bid, predefined timeline scoring bands, normalized panel and workmanship warranty scores, and a checklist for team and approach requirements.

These scoring thresholds are explicit design assumptions because the assessment provides weights but does not prescribe normalization formulas.

Reviewers can inspect each criterion's score, supporting evidence, missing information, and contribution to the final result. Unknown values are not silently converted into confirmed facts or arbitrary scores.
