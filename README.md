
## reference-data.json (Telemetry Financial 2.0)

Values that change on a schedule, read by the app on every launch:

| Section | What | Changes |
|---|---|---|
| `milPay` | Military monthly basic pay, all grades, 22 service brackets (exact cents) | Every January |
| `bas` | Basic Allowance for Subsistence (officer / enlisted) | Every January |
| `va` | VA disability compensation rates by rating and dependents | Every December 1 |
| `irs` | TSP/401(k), IRA and HSA contribution limits | Every fall |

A monthly scheduled task fetches the official sources (the annual pay executive order / DFAS, va.gov, IRS),
updates only sections with a newer effective date, runs `python3 validate_reference.py reference-data.json`
(which compares against the committed version: every cell within range, pay rows = old × announced raise ±$1,
no missing grades), and commits only if it passes. The app re-runs the same checks and ignores any section
that fails, keeping its last good numbers.
