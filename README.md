# Next Generation Dashboard — UI Foundation v0.1

This is an isolated visual/interaction prototype. It does not overwrite the existing dashboard or reporting engine.

## Included
- Left functional navigation with Release Focus, Regression/Automation, and Performance Testing.
- Release Stream → Release → Build selectors. Sprint is intentionally excluded.
- Release Focus KPIs based only on Manual release-governing tests.
- Release Test Coverage based on completed applicable scenario × environment gates.
- Manual execution progress and Pass/Fail/Blocked/Not Executed totals.
- Environment pass rate derived from completed Manual scenario results in that environment.
- Release Item navigator (1 Jira ticket = 1 Release Item).
- Release Item → N Features → 1 Scenario per Feature → 1 Manual Test Definition.
- Feature and Selected Feature statuses displayed per environment as ✓ / ✕ / ! / — / N/A.
- Jira link retained at selected scenario level.
- Automation and Performance tabs reserved as separate functional areas.

## Run
From this `next_gen_preview` directory:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## Purpose
This package is for layout and interaction review before wiring the next-generation release manifest and reporting engine into production data.
