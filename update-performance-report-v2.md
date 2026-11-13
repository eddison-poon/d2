# Performance Report V2 Updater

Update the corresponding **Scenario X / Milestone X V2 HTML performance report** using the latest result data in `res.md`.

## Objective

Use `res.md` as the source for newly added performance test results.

Identify which Scenario and Milestone has new or updated result data, then update the corresponding V2 HTML report:

`scenario_XX_milestone_XX_v2.html`

Do not update the non-V2 HTML report.

---

## 1. Read Existing Data First

Before making any change:

1. Read `res.md`.
2. Identify the Scenario, Milestone, test date, environment, execution period, and all test result rows.
3. Open the corresponding existing `_v2.html` report.
4. Review the existing historical results before modifying the file.

The existing HTML report is cumulative performance evidence.

**Do not remove existing historical test results.**

New data from `res.md` must be added to the existing report unless the new data is clearly an update/correction to an existing result.

---

## 2. Result Data

For every new execution, capture all available fields:

- Execution Period
- Concurrent Executions
- Number of Files, if applicable
- Pass
- Failed
- Passing Rate
- Average Response Time
- P95 Response Time

If Passing Rate is blank in `res.md`, calculate:

`Passing Rate = Pass / (Pass + Failed) × 100`

Calculate Error Rate as:

`Error Rate = Failed / (Pass + Failed) × 100`

Round percentages to two decimal places where required.

Do not invent missing test data.

---

## 3. Daily Result Sections

Add the newest testing date above older testing dates.

For each testing date:

- Keep all executions from that date in the same table.
- Include `Execution Period` as the first column when the source provides it.
- Preserve all existing executions.
- Add new executions without overwriting unrelated historical rows.

The newest date should display the `LATEST` badge.

Remove the `LATEST` badge from the previous latest date.

---

## 4. Representative Result / Used for Trend

Each testing date must have one representative execution selected using the **Used for Trend** radio button.

For a newly added date:

- If there is only one execution, select it.
- If there are multiple executions, use the latest execution as the default representative unless the existing report or source explicitly indicates another result.

All radio buttons must remain **selectable**.

When the user selects another execution for the same date:

- Remove the representative-row highlight from the previous row.
- Highlight the newly selected row.
- Update all Performance Trend charts using the newly selected result.

Do not disable or remove the existing radio-button JavaScript behavior.

---

## 5. Performance Trend

Update:

**Performance Trend — Representative Result Per Day**

Add the new date chronologically to all three charts:

- Passing Rate (%)
- P95 Response Time (seconds)
- Concurrent Executions

Only one representative result per testing date should appear in the trend.

Preserve the existing target lines and target values defined by that milestone.

If a new result exceeds the current chart scale, adjust the chart scale so the result remains visible.

Do not change the milestone target merely to fit the new result.

---

## 6. Completion Status

Update Completion Status using the representative result from the **latest testing date**.

Update:

- Latest Result date/environment
- Representative execution
- Volume
- P95 Response Time
- Error Rate

Volume is:

`Pass + Failed`

Do not automatically change the overall status to `ACHIEVED`.

Keep `RESULT RECORDED` unless the existing report has explicit milestone acceptance logic that proves the milestone has been achieved.

---

## 7. Execution Config

If the existing V2 report contains an **Execution Config** section:

**preserve it exactly.**

Do not remove, rewrite, or infer changes to:

- Agent
- Config
- Prompt
- Attachment

unless new execution-config information is explicitly provided in the source.

---

## 8. Issue List

Preserve the existing **Issue List**.

Do not overwrite or clear manually entered issue information.

---

## 9. Historical Data Protection

This rule is critical:

**Never delete historical performance results simply because they are no longer present in `res.md`.**

`res.md` may contain only newly added results.

The existing V2 HTML report is the historical record.

Only replace an existing row when the new source clearly represents a correction to that same execution.

---

## 10. Scope Protection

Do not:

- redesign the report
- change established styling
- change milestone targets
- modify another Scenario/Milestone
- modify non-V2 reports
- remove historical data
- remove Execution Config
- remove Issue List
- disable radio buttons
- add speculative information
- modify `res.md`

Make the smallest necessary change to incorporate the new performance results.

---

## 11. Validation

Before finishing, verify:

1. New results match `res.md`.
2. Passing Rate calculations are correct.
3. Error Rate calculations are correct.
4. Volume calculations are correct.
5. Existing historical dates and rows remain present.
6. Execution Period is shown when available.
7. Latest date has the `LATEST` badge.
8. Previous date no longer has the `LATEST` badge.
9. One representative result is selected for every date.
10. All radio buttons remain selectable.
11. Trend charts contain all historical dates in chronological order.
12. Trend charts respond when representative radio buttons are changed.
13. Completion Status reflects the latest representative result.
14. Execution Config remains unchanged.
15. Issue List remains unchanged.
16. Existing visual design remains unchanged.

Finally, report:

- which Scenario / Milestone was updated
- which date(s) were added or changed
- calculated Passing Rate / Error Rate / Volume
- which execution is the default representative
- whether trend charts were updated
- confirmation that historical data was preserved

Do **not** commit or push unless explicitly instructed.
