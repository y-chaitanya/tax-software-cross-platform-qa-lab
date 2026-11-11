# Tax Software Cross-Platform QA Lab: Test Plan

Chaitanya Yarlagadda, EA · Project started 10 November 2026 · Status: in progress

## Objective

Prepare identical synthetic tax returns in two professional tax platforms, Intuit ProConnect Tax and TaxSlayer Pro, and compare them on two axes: the amounts each one computes, and how each one behaves when given incomplete or invalid input. The second axis is the primary one. Two mature platforms should agree on the arithmetic of a clean return; where they differ meaningfully is in what they do when the person entering the data makes a mistake.

## Why this axis

In a tax software support queue, most tickets are not wrong-answer tickets. They are a user who entered something the software accepted when it should not have, or who did not see a warning the software did show, or who cannot find a number the software computed silently. Testing how each platform handles bad input is therefore closer to the real support surface than testing whether it computes self-employment tax correctly, which it will.

## Scope

- Form 1040 individual returns with wage income, Schedule C self-employment income, the self-employment tax deduction, the qualified business income deduction, and one state return.
- Both platforms, same facts, entered independently rather than imported.
- Selected amounts recomputed by hand from the Internal Revenue Code and the form instructions, independent of either platform.

## Out of scope

- Electronic filing and printing. The ProConnect trial does not permit either, and no return in this project is intended for filing.
- Entity returns (Forms 1120, 1120-S, 1065), multi-state apportionment, and prior-year returns.
- Performance, load, and security testing.

## Test data policy

All data is synthetic. Taxpayer facts are drawn from IRS Publication 4491-W practice scenarios or invented outright. No real taxpayer information is entered into either platform at any point, and identifiers are masked in all screenshots. This follows the same rule applied to every project in my portfolio.

## Environment

| Platform | Version / access | Status |
|---|---|---|
| Intuit ProConnect Tax | Free trial, tax year 2025, browser-based | Set up 10 Nov 2026 |
| TaxSlayer Pro | IRS Practice Lab (TRAINPROWEB) | Available |
| Hand calculation | IRC, form instructions, spreadsheet | Available |

Both platforms are run in tax year 2025 so results are comparable.

## Approach: Track A, calculation comparison (control)

Each case is entered in both platforms and compared on AGI, taxable income, Schedule C net profit, self-employment tax, the deductible half of self-employment tax, the qualified business income deduction, total tax, and refund or balance due. Selected lines are also computed by hand.

| ID | Case | Compared on |
|---|---|---|
| A1 | Single, W-2 wages only, standard deduction | AGI, taxable income, total tax |
| A2 | A1 plus Schedule C with ordinary expenses | Net profit, SE tax, SE tax deduction |
| A3 | A2 plus qualified business income deduction | §199A deduction |
| A4 | A3 plus one state return | State taxable income, state tax |

## Approach: Track B, input handling and diagnostics (primary)

Each case introduces a deliberate error and records what each platform does: whether it blocks, warns clearly, warns vaguely, silently substitutes a value, or accepts the entry without comment. Each diagnostic message is recorded verbatim and assessed for whether a non-specialist could act on it unaided.

| ID | Condition introduced | Recorded |
|---|---|---|
| B1 | Taxpayer SSN omitted | Block / warn / silent; message text |
| B2 | Schedule C business code omitted or invalid | Block / warn / silent; message text |
| B3 | Negative wage amount entered | Accepted or rejected; message text |
| B4 | Date of birth set in the future | Accepted or rejected; downstream effect |
| B5 | Home office area exceeding total home area | Accepted or rejected; deduction computed |
| B6 | Expense entered with the wrong sign | Effect on net profit; any warning |
| B7 | All diagnostics encountered | Verbatim text; actionable by a non-specialist? |
| B8 | SE tax and §199A computed values | Navigation steps required to view the computation |

## What counts as a defect

A difference between the two platforms is not by itself a defect. Different default elections, rounding conventions, and treatments of an ambiguous entry all produce legitimate differences. A finding is recorded as a defect candidate only when all three of the following hold:

- It is reproducible from written steps, by me, on a fresh return.
- The mechanism is understood and can be stated, not merely observed.
- The behavior is inconsistent with the Internal Revenue Code, the form instructions, or the platform's own documented behavior.

Anything short of all three is documented as an observed difference, not reported as a defect. A result of "no defects found" is a legitimate outcome of this project and will be reported as such.

## Deliverables and current status

| Deliverable | Status | Date |
|---|---|---|
| Test plan (this document) | Complete | 11 Nov 2026 |
| ProConnect environment set up | Complete | 10 Nov 2026 |
| TaxSlayer Pro environment | Available | |
| Track A execution | In progress: A1 and A2 (with QBI) run in ProConnect, all compared lines match hand calculations; TaxSlayer Pro not yet run | 11 Nov 2026 |
| Track B execution | In progress: B1 observed in ProConnect (missing SSN computes, fatal e-file diagnostic) | 11 Nov 2026 |
| Test case write-ups | TC-001 written | 11 Nov 2026 |
| Cross-platform comparison spreadsheet | Not started | |
| Defect reports (if any qualify) | None so far | |
| Re-runnable test cases for any defect found | Not started | |
| Final QA summary | Not started | |

Status is recorded as it stands, not as I intend it to stand. Nothing above is marked complete that has not been done.

## Note on scope and limits

This is a self-directed project on a trial environment, not production support work. The ProConnect trial is a limited-feature environment and TaxSlayer Pro is accessed through the IRS practice platform, so neither is configured as a working firm would configure it. The purpose is to compare two products' behavior on identical inputs under controlled conditions, and to produce a documented record of that comparison, not to evaluate either product for purchase.
