# AI Proposal Triage Design
**Reference: MATACS-TH-2026-02**

## 1. AI vs. rules

- **AI is used for:** reading proposal text, extracting facts and evidence, independently verifying four team items, and a low-cost manipulation classifier.
- **Plain code is used for:** checking mandatory requirements, validating outputs, calculating every score, applying weights, ranking and breaking ties.

The admin selects a category and saves its mandatory requirements, weighted criteria and benchmarks; code checks that weights total 100%. A reviewer uploads proposals. The application extracts PDF text and checks readability; unclear files go to a person. Pattern rules and a low-cost AI classifier screen for instructions aimed at automated reviewers. Suspicious passages are quarantined before the main AI calls and shown only to the reviewer. AI extracts facts with evidence quotes, page references and confidence levels. A second independent AI check verifies the named lead, crew, safety plan and monitoring plan; disagreements are flagged. AI is useful for reading messy wording, while code is better at exact, repeatable decisions. A human makes the award.

## 2. Consistency and explainability

Temperature 0 reduces variation but does not guarantee identical AI answers; a fresh extraction could differ. The system therefore saves extracted facts, supporting evidence, review decisions, prompt and model versions, and criteria version. Re-ranking the same saved, confirmed facts against the same criteria version always produces the same order. Code uses full precision and rounds scores only for display.

The reviewer sees each criterion's score and weight, evidence and page, flags, and a plain-language reason for each position. Missing mandatory evidence is flagged; explicit failure makes a proposal ineligible. Proposal B is ineligible because the bidder does not state its own electrical licence and instead relies on a subcontractor to be confirmed after award; it is excluded from scoring and shown to the reviewer with that reason. Missing scoring facts are never guessed. Flagged proposals can show provisional calculations but stay out of the confirmed ranking until blocking issues are resolved.

Proposal A ranks first. Proposal E is second among currently ranked proposals, but its position is provisional: Proposal D's timeline is unknown, and D could overtake E with a timeline of about 14 weeks or less. Even a perfect timeline score would not put D ahead of A.

## 3. Human in the loop

People review unreadable PDFs, missing or unclear facts, low-confidence extraction, suspected manipulation and disagreements between the two AI team checks. They inspect original evidence, confirm facts, request clarification or correct values. Corrections rerun the mandatory gate and scoring. Overrides require written reasons; a human makes the final award decision.

The audit log records:
- File references, extracted facts, evidence pages and confidence.
- Screening flags and both AI outputs.
- Model, prompt and criteria versions; formulas and scores.
- Reviewer identity, timestamps, corrections and override reasons.
- Final ranking and award decision.

This shows what changed, who changed it and why.

## 4. Changing criteria

Criteria are configured through admin screens per category, never hard-coded. Each version stores mandatory checks, weights, scoring formulas and editable benchmarks. Code validates settings, including that weighted criteria total 100%.

When an admin changes a criterion, weight or benchmark, the system creates a new version without rewriting history. Old results stay linked to their original version for audit. Affected results are marked out of date and must be rescored under the new version before comparison. Reviewers can see both versions and why rankings changed. Only results from the same criteria version are compared.

## 5. Risks

**Wrong extraction:** Poor PDFs or confusing wording can produce wrong facts. Check readability, require evidence quotes and page references, and route uncertain evidence to people.

**Made-up facts:** AI may infer a licence, schedule or experience. Require explicit evidence, use `not_stated` or `null` for missing information, and verify quotes against source text.

**Bias:** Score stated criteria, not a bidder's name or company size. Apply the same formulas and benchmarks to all, keep evidence and review unusual outcomes.

**Manipulation:** Proposal C contains an attempt to direct automated evaluation. Quarantine suspicious text before main AI calls, ignore its instructions, flag it for review and evaluate legitimate content where safe.

**Cost and delay:** Use inexpensive screening first, cache validated facts and scores, and rerun only affected steps after changes.

**Invalid output or disagreement:** Validate strict JSON, retry once, then flag failures. Compare the independent team check with extraction and send differences to human review.

**Limited team rubric:** Four evidence checks measure completeness, not the quality of a plan. Show this limitation to reviewers rather than presenting completeness as proof of quality.

## Assumptions

The five-year experience window begins in October 2021. Accept stated counts of qualifying commercial installations of at least 100 kW; flag uncertain dates without automatically reducing scores. Missing mandatory evidence is flagged, while explicit failure is ineligible. An undetermined timeline remains pending.

Full-score benchmarks of 15 installations, 25-year panel warranty, 10-year workmanship warranty, price benchmark at 70% of the budget ceiling, and 8-week timeline are admin-configured design choices, not requirements from the brief. Prices above the ceiling or schedules beyond the deadline are flagged for review rather than silently scored. The four team items have equal weight.
