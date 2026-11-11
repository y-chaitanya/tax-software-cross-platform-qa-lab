# Tax Software Cross-Platform QA Lab

Independent QA testing of two professional tax platforms — **Intuit ProConnect Tax** and **TaxSlayer Pro** — using synthetic individual tax returns.

> **All data in this project is synthetic.** Taxpayer facts come from IRS Publication 4491-W practice scenarios or are invented outright. No real taxpayer information is entered into either platform at any point, and identifiers are masked in every screenshot.

**Status: in progress.** Started 10 November 2026.

📄 **[Read the test plan →](test-plan.md)**

---

## What this project is

For a clean return, the platforms should produce consistent results on comparable calculations. Differences arising from legitimate elections, assumptions, or rounding will be investigated separately. Where they differ is in what they do when the person entering the data makes a mistake — and that is where a support queue actually lives.

So this project runs two tracks. **Track A** compares computed amounts, as a control. **Track B**, the primary one, introduces deliberate errors and records how each platform responds: whether it blocks, warns clearly, warns vaguely, silently substitutes a value, or accepts the entry without comment.

Both platforms are run in **tax year 2025** so amounts are comparable. TaxSlayer Pro also offers 2024; it is not used, because a cross-year comparison would measure the tax year rather than the software.

## The bar for calling something a defect

A difference between two platforms is not a defect. A finding is recorded as a defect candidate only when it is reproducible from written steps, the mechanism is understood and can be stated, and the behavior is inconsistent with the Code, the form instructions, or the platform's own documented behavior.

**"No defects found" is a legitimate outcome and will be reported as one.**

---

## Current status

| Deliverable | Status | Date |
| --- | --- | --- |
| Test plan | Complete | 11 Nov 2026 |
| ProConnect environment | Set up | 10 Nov 2026 |
| TaxSlayer Pro environment | Available, TY2025 selected | 11 Nov 2026 |
| Track A — ProConnect | A1, A2 executed; all compared lines match hand calculations | 11 Nov 2026 |
| Track A — TaxSlayer Pro | Not started | — |
| Track B — ProConnect | B1 executed | 11 Nov 2026 |
| Track B — TaxSlayer Pro | Not started | — |
| Test case write-ups | TC-001 written | 11 Nov 2026 |
| Cross-platform comparison spreadsheet | Not started | — |
| Defect reports | None identified so far | — |
| Final QA summary | Not started | — |

*Status is recorded as it stands, not as I intend it to stand. Nothing above is marked complete that has not been done.*

---

## Findings so far

### Calculation differences investigated and classified as expected behavior

**Tax Table midpoint treatment.** Computed tax differed from a direct formula calculation on the same taxable income. Cause: the IRS Tax Table assigns tax at the midpoint of each bracket range rather than to the exact figure. Not a defect — this is how the table is constructed.

**Whole-dollar rounding of self-employment tax.** Small difference traced to rounding convention on Schedule SE. Not a defect.

Both of these would read as discrepancies to someone comparing outputs without tracing the cause. Identifying *why* two correct systems produce different numbers is the point of the control track.

### Input handling

**B1 — Taxpayer SSN omitted (ProConnect).** The return computes normally with the SSN missing; the omission surfaces only as a fatal e-file diagnostic. Documented as observed behavior; the comparison against TaxSlayer Pro is pending.

### Open observations — not yet verified

**Form 2210 penalty on a withholding-only scenario.** An $85 underpayment penalty was computed. Requires a safe harbor check — whether withholding reached 90% of current-year tax, or 100%/110% of prior-year — before this is classified. Unresolved, and not reported as a defect.

---

## Why I built this

I hold an active IRS Enrolled Agent credential and spent four years reproducing and writing up user-reported defects for an engineering team. This project puts those two halves in the same place: testing tax software as someone who can both drive the software and independently verify what it computed.

---

**Chaitanya Yarlagadda, EA** · [github.com/y-chaitanya](https://github.com/y-chaitanya)
