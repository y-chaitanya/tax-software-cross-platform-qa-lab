# Tax Software Cross-Platform QA Lab

**Status:** In Progress  
**Project Type:** Independent Software QA and Tax Workflow Validation  
**Tools:** Intuit ProConnect Tax, TaxSlayer Pro, Excel, SQL, GitHub

## Project Overview

This independent testing project evaluates tax preparation software workflows through synthetic individual tax return scenarios.

The project focuses on cross-platform validation, independent calculation checks, input-handling behavior, discrepancy investigation, defect documentation, and regression testing.

The objective is to demonstrate a structured QA approach to tax software: reproduce a scenario, compare results, investigate differences, document evidence, and distinguish genuine defects from expected tax calculation behavior.

## Testing Approach

1. Develop synthetic individual tax return scenarios.
2. Prepare the same scenarios in Intuit ProConnect Tax and TaxSlayer Pro.
3. Compare calculated results and relevant tax forms.
4. Independently verify selected calculations.
5. Record and investigate discrepancies.
6. Classify findings as expected behavior, input/configuration issues, or potential software defects.
7. Document confirmed defects with reproducible steps and supporting evidence.
8. Develop regression tests for verified defects.

## Work Completed

### ProConnect Tax — Initial Testing

Two synthetic practice scenarios have been tested:

- W-2 income only.
- W-2 income plus Schedule C business activity.

Calculated results were compared against independent manual calculations. Both scenarios matched on key amounts, including adjusted gross income, qualified business income deduction, taxable income, and tax.

Two observed calculation differences were investigated and identified as expected behavior rather than defects:

- Tax Table midpoint treatment versus formula calculations.
- Whole-dollar rounding of self-employment tax.

### Input Handling and Diagnostic Observations

Additional behaviors have been documented for investigation:

- A missing SSN allowed return calculation but generated a fatal e-file diagnostic.
- Entering Schedule C expenses before gross receipts resulted in a $5,000 loss.
- A withholding-only payment scenario generated an $85 Form 2210 penalty that requires further verification.

These observations are not classified as confirmed software defects. Further testing and tax-year-specific verification are required.

### TaxSlayer Pro Practice

Fifteen fictional practice returns have been prepared in the IRS practice environment for tax year 2024. Scenarios include business income, rental income, capital gains, retirement distributions, Social Security, credits, and amended returns.

Cross-platform recreation of the ProConnect scenarios is in progress.

## Planned Deliverables

| Deliverable | Status |
|---|---|
| Initial test plan | Started |
| Synthetic test scenarios | In Progress |
| ProConnect testing | Initial scenarios completed |
| TaxSlayer Pro comparison | In Progress |
| Cross-platform comparison spreadsheet | Planned |
| Independent calculation worksheets | In Progress |
| Formal defect reports | Pending verified findings |
| Regression test suite | Planned |
| Synthetic-data screenshots | Planned |
| Final QA summary | Planned |

## QA Documentation Standards

Each test case will record:

- Test case ID
- Tax year and software
- Scenario and assumptions
- Preconditions and input data
- Reproduction steps
- Expected result
- Actual result
- Evidence and observations
- Test status

Potential defects will be reported only when the behavior is reproducible and evidence supports a genuine software problem.

## Customer Support and Issue Tracking — Learning in Progress

Additional practice will cover:

- Zendesk ticket intake, prioritization, customer communication, and escalation.
- Linear issue creation, reproduction steps, labels, and engineering handoff.
- Browser Developer Tools for technical investigation.
- Regression testing and release verification.

## Data Integrity and Limitations

- All scenarios use fictional taxpayer information.
- No real taxpayer personally identifiable information is included.
- Tax calculation observations are evaluated in the context of the applicable tax year.
- Expected differences are not reported as software defects.
- Only tests actually performed and findings actually verified will be marked complete.

## Project Goal

Build a practical, evidence-based demonstration of tax software QA skills, combining tax knowledge, application testing, cross-platform validation, technical investigation, and clear communication between customer support and engineering.
