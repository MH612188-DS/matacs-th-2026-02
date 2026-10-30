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

The proposed scoring rules use a capped experience score based on qualifying installations, relative price scoring against the lowest eligible bid, predefined timeline scoring bands, normalized panel and workmanship warranty scores, and a checklist for team and approach requirements. These scoring thresholds are explicit design assumptions because the assessment provides weights but does not prescribe normalization formulas. Reviewers can inspect each criterion's score, supporting evidence, missing information, and contribution to the final result. Unknown values are not silently converted into confirmed facts or arbitrary scores.

## 3. Human in the Loop

Human will remain in the loop to make the systems more resilient and less prone to hallucinations. The human will be the one that has the final verdict on what the results are telling.

1. A reviewer uploads proposals.
2. The system extracts information from the documents and presents it with supporting evidence.
3. A reviewer then verifies uncertain, missing, or conflicting information.
4. Flagging the proposals requiring clarification so that it can be reviewed.
5. The reviewer can approve documented corrections or override results with a recorded reason.
6. The final award decision remains with the human reviewer.

The audit log records proposal identifiers, extracted data, evidence references, criteria and scoring versions, model and prompt versions, calculated scores, reviewer actions, overrides, timestamps, and the final decision. The system will provide recommendations and not autonomous procurement decisions.

## 4. Changing Criteria

The administrators can manage evaluation criteria through configuration rather than hard-coded application logic. Whenever criteria or weights change, the system creates a new criteria version. Previous generated results are kept for the audit and flagged as review.

The reviewer can initiate rescoring using the updated configuration. The system will preserve both results and allows comparison of the previous and updated rankings. This prevents historical decisions from being silently modified and ensures that every result can be traced to the criteria under which it was evaluated.

## 5. Risks and Safeguards

| Risk | Safeguard |
|---|---|
| Incorrect information extraction | Require evidence snippets and page references, followed by human verification where necessary. |
| AI hallucination | Require unknown values for unsupported claims and validate structured output. |
| Prompt injection | Treat proposal content as untrusted data. Instructions embedded in documents must never override system instructions or evaluation criteria. |
| Missing or ambiguous information | Flag the proposal for human review instead of inventing values or silently assigning scores. |
| Inconsistent rankings | Use deterministic scoring formulas, fixed scoring configurations, and versioned criteria. |
| Bias in evaluation | Apply the same administrator-defined criteria and scoring rules to every proposal. |
| Unexpected API costs or failures | Use bounded retries, process documents in controlled batches, cache validated extraction results, and log failures. |
| Unauthorized changes | Apply role-based access controls and maintain an audit trail of configuration changes and reviewer overrides. |

The proposed system combines AI-based document understanding with deterministic evaluation and human decision-making. This separation makes the process explainable, auditable, and adaptable when procurement requirements change.

