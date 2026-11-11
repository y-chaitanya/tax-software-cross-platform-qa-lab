# TC-001: W-2 Wages Only, Single, Standard Deduction

| Field | Value |
|---|---|
| Test case ID | TC-001 |
| Test plan reference | Track A, case A1 (calculation comparison, control) |
| Tax year | 2025 |
| Platforms | Intuit ProConnect Tax (free trial, browser) / TaxSlayer Pro (IRS practice lab) |
| Date run | 11 November 2026 (ProConnect) |
| Tester | Chaitanya Yarlagadda, EA |
| Status | ProConnect: Executed, Pass. TaxSlayer Pro: Not yet run |

## Objective

Confirm that a simple W-2-only return computes AGI, taxable income, income tax, and refund correctly, and record how the platform arrives at the tax amount. This is the control case: a clean return that both platforms should compute the same way.

## Test data (synthetic)

All data is fictional. No real taxpayer information is used.

| Item | Value |
|---|---|
| Taxpayer | Test A1, single, date of birth 01/15/1985 |
| Address | 100 Main St, Los Angeles, CA 90001 |
| SSN | Left blank on purpose (see Observations; also used for TC-B1) |
| Dependents | None |
| W-2 employer | Sample Test Co, EIN 12-3456789 (fictional) |
| Box 1 wages | 52,000 |
| Box 2 federal withholding | 5,000 |
| Box 3 / Box 5 SS and Medicare wages | 52,000 |
| Box 4 SS tax / Box 6 Medicare tax | 3,224 / 754 |
| State | CA, state withholding 1,500 |

## Preconditions

- New client and new 1040 return for tax year 2025.
- No other income, adjustments, or credits entered.

## Steps (ProConnect Tax)

1. Tax returns > Create tax return > Add new client (Individual).
2. Enter name, date of birth and address above. Leave Tax ID blank.
3. Select return type 1040, tax year 2025.
4. Input return > General > Client Information: filing status Single.
5. Input return > Income > Wages, Salaries, Tips (W-2): enter the W-2 values above.
6. Refresh forms. Open Form 1040 and the Federal Income Tax Summary.
7. Record each value below.

## Expected results (hand calculation)

| Line | Item | Expected | Basis |
|---|---|---|---|
| 1040 line 11 | AGI | 52,000 | W-2 box 1 |
| 1040 line 12e | Standard deduction | 15,750 | 2025 single |
| 1040 line 15 | Taxable income | 36,250 | 52,000 minus 15,750 |
| 1040 line 16 | Income tax | 4,115 | Tax Table row 36,250 to 36,300 (midpoint 36,275): 1,192.50 + 12% x 24,350 = 4,114.50, rounded |
| 1040 line 35a | Refund | 885 | 5,000 minus 4,115 |

Formula method for comparison: 1,192.50 + 12% x (36,250 minus 11,925) = 4,111.50.

## Actual results (ProConnect Tax)

| Line | Item | Expected | Actual | Result |
|---|---|---|---|---|
| 11 | AGI | 52,000 | 52,000 | Pass |
| 12e | Standard deduction | 15,750 | 15,750 | Pass |
| 15 | Taxable income | 36,250 | 36,250 | Pass |
| 16 | Income tax | 4,115 | 4,115 | Pass |
| 35a | Refund | 885 | 885 | Pass |

## Actual results (TaxSlayer Pro)

Not yet run. Will be entered in tax year 2025 so the comparison uses the same year as ProConnect.

## Observations

| # | Observation | Classification |
|---|---|---|
| 1 | Income tax is 4,115, not the formula amount of 4,111.50. For taxable income under 100,000, the software uses the IRS Tax Table, which computes tax at the midpoint of each 50-dollar row. | Expected behavior, not a defect |
| 2 | With the SSN blank, the return still computed and forms were produced. The missing SSN appeared only under Check return as a Fatal diagnostic: "Taxpayer's social security number missing." | Input handling observation (feeds TC-B1) |

## Evidence

- Screenshots of Form 1040 page 2 and the Federal Income Tax Summary, identifiers masked (to be added to `evidence/TC-001/`).

## Result

ProConnect Tax: **Pass.** All five compared lines match the expected values. No defects found.
