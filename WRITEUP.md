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

