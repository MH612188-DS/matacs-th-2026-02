# Evaluation Criteria and Scoring Rubric

**Assessment Reference:** MATACS-TH-2026-02

## 1. Evaluation Configuration

| Parameter | Configuration |
|---|---|
| Evaluation category | Commercial Solar Installation |
| Project capacity | 150 kW |
| Project location | Windsor, Ontario |
| Budget ceiling | $260,000 CAD |
| Maximum completion time | 16 weeks |
| Criteria version | 1.0 |
| Scoring scale | 0–100 |

The evaluation configuration is administrator-defined and must not be hard-coded into the application.

## 2. Mandatory Criteria

Mandatory criteria are evaluated independently of the weighted score.

| Criterion | Passing condition |
|---|---|
| Ontario electrical contractor licence | Bidder holds an Ontario electrical contractor licence, explicitly stated in the proposal |
| WSIB clearance and liability insurance | Both current WSIB clearance and $5M liability insurance are confirmed |

### Eligibility rules

- **Pass:** All mandatory requirements are confirmed.
- **Fail:** At least one mandatory requirement is explicitly contradicted or not met.
- **Needs review:** Evidence is missing, ambiguous, or requires human verification.

A confirmed failure results in an ineligible proposal. Uncertain evidence is flagged for human review rather than automatically treated as a failure.

## 3. Weighted Evaluation Criteria

| Criterion | Weight | Evaluation objective |
|---|---:|---|
| Relevant experience | 30% | Commercial installations of 100 kW or more in the last five years |
| Price | 25% | Lower total project cost within the budget ceiling |
| Timeline | 15% | Shorter completion time within 16 weeks |
| Warranty | 15% | Panel and workmanship warranty durations |
| Team and approach | 15% | Named project lead, crew, safety and monitoring plan |
| **Total** | **100%** | |

## 4. Scoring Methodology

Each weighted criterion receives a score between 0 and 100.

### 4.1 Relevant Experience (30%)

Proposed formula:

`Experience Score = min((Qualifying Projects / 10) × 100, 100)`

Only commercial installations of 100 kW or more completed within the last 5 years qualify. The threshold for maximum score is set at 10 projects within last 5 years where more than 10 will also give maximum score. 

### 4.2 Price (25%)

First all the prices are subtracted from the 260,000, then they will be divided by the largest results and multiplied by 100. This gives us a normalized value that can be added to the final score.

`Price Score = {260000-P_i}/{260000-P_{min}} x 100`

The budget ceiling is $260,000 CAD. Bids exceeding the ceiling are flagged for review under the budget policy before ranking.

### 4.3 Timeline (15%)

Proposed scoring bands:

| Completion time | Score |
|---|---:|
| 10 weeks or less | 100 |
| 11 weeks | 90 |
| 12 weeks | 80 |
| 13 weeks | 70 |
| 14 weeks | 60 |
| 15 weeks | 50 |
| 16 weeks | 40 |
| More than 16 weeks | 0 |

An unspecified completion timeline is treated as unknown and requires human review.

### 4.4 Warranty (15%)

Panel and workmanship warranties are evaluated separately.

`Panel Score = min((Panel Warranty Years / 25) × 100, 100)`

`Workmanship Score = min((Workmanship Warranty Years / 10) × 100, 100)`

`Warranty Score = (Panel Score + Workmanship Score) / 2`

### 4.5 Team and Approach (15%)

Each component receives 25 points when supported by proposal evidence.

| Component | Points |
|---|---:|
| Named project lead | 25 |
| Defined project crew | 25 |
| Site safety plan | 25 |
| Performance monitoring plan | 25 |
| **Total** | **100** |

## 5. Final Weighted Score

The final score is calculated as:

`Final Score = (Experience × 0.30) + (Price × 0.25) + (Timeline × 0.15) + (Warranty × 0.15) + (Team × 0.15)`

All criterion scores are between 0 and 100.

## 6. Ranking and Decision Rules

| Status | Definition | Rank |
|---|---|---|
| ranked | Eligible and sufficiently evaluated | Numerical |
| flagged | Requires clarification or human verification | null |
| ineligible | Fails a confirmed mandatory requirement | null |

Ranking procedure:

1. Evaluate mandatory criteria.
2. Exclude proposals that fail confirmed mandatory requirements.
3. Flag proposals with unresolved mandatory evidence.
4. Calculate weighted scores for eligible proposals with sufficient evidence.
5. Sort by final score in descending order.
6. Apply a documented tie-breaking rule when scores are equal.
7. Present evidence, score breakdowns, and explanations to the reviewer.

Unknown values must not be silently converted into confirmed facts or arbitrary scores.

## 7. Versioning and Audit

Every evaluation must retain:

- Criteria version and weights.
- Scoring formula version.
- Extracted proposal data and evidence references.
- Individual criterion scores.
- Final weighted score.
- Human corrections and overrides.
- Evaluation timestamp.

Changes to evaluation criteria create a new version. Previous evaluation results remain available for audit, and rescoring requires an explicit action.

---

**Note:** The formulas and scoring bands in this document are proposed design assumptions. The assessment specifies the criteria and weights but does not prescribe exact scoring formulas or normalization thresholds.
