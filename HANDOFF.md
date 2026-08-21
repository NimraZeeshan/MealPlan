# Checkpoint Handoff

Date: 2026-08-21
Branch: `patch-2-style-guide`
Parent baseline: `82a20a5` (`docs: add Dashboard-only STYLE_GUIDE.md`)
Checkpoint intent: preserve the approved calculation-correction baseline; no new features were added during checkpointing.

## Current approved baseline

- The product remains a single-file static application in `vitality_kpi_dashboard_webapp.html`, with embedded data and local image assets.
- The Dashboard visual baseline is governed by `STYLE_GUIDE.md`.
- The Report tab is a separately styled product surface. Its structure, typography, cards, tables, action/follow-up areas, metadata, signatures, and print/PDF rules are locked unless a future request explicitly targets the Report.
- The approved working calculation baseline uses logical menu occurrences instead of raw duplicate plan rows for occurrence-based metrics and analytics.
- No source data files, images, Report Print PDFs, or report/print styling were changed in this checkpoint.

## Work completed in this session

- Added one shared Main/Side/Unknown occurrence classifier and applied it consistently to occurrence-based dashboard analytics.
- Added logical occurrence deduplication and applied it to current-period, previous-period, weekly, and opened-report-snapshot plan collections.
- Corrected high-sodium Main and Side exposure calculations so the numerator and denominator use the same eligible dish type.
- Updated period menu diversity/repetition metrics and affected analytics to consume the corrected occurrence set/classification.
- Removed the redundant empty `nutritionSummary` card and its remaining renderer usage; no `nutritionSummary` references remain.
- Added a local `.claude/launch.json` static-server configuration for reproducible previewing on port 5173.
- Added this handoff and performed static, data-level, and real-browser verification.

## Exact files changed

- `vitality_kpi_dashboard_webapp.html`
  - Calculation and analytics consistency corrections.
  - Removal of the redundant Nutrition summary container/renderer usage.
- `.claude/launch.json`
  - Local static preview configuration (`npx --yes serve -l 5173 .`).
- `HANDOFF.md`
  - Checkpoint state, decisions, verification, constraints, and next-step guidance.

## Important design and calculation decisions

### Logical occurrence identity

- A logical occurrence key is the normalized tuple:
  `MealDate + MealTime + Unit + Chef + RecID + DishType`.
- Dates are normalized to ISO format where parseable; string key fields are trimmed and lowercased.
- The first row for a duplicate key is retained.
- `RecipeName` and `PlanID` are deliberately not part of the identity because they do not change the business occurrence represented by the tuple above.
- On the embedded full-period plan (23 May–10 Aug 2026), 888 raw rows become 884 logical occurrences; four duplicate rows are removed across 4 June, 5 June, and 7 July.

### Dish-type classification

- A non-empty `MenuSection` is authoritative.
- Exact case-insensitive values `Main`/`Main Dish` map to Main; `Side`/`Side Dish` map to Side.
- If `MenuSection` is blank, the same exact mapping is attempted against recipe metadata `Plate Category`.
- Any other value maps to Unknown. Broad substring matching was removed to avoid false classifications.
- On the full embedded plan after deduplication: Main = 362, Side = 420, Unknown = 102.

### High-sodium exposure

- Main threshold: sodium strictly greater than 600 mg/100 g.
- Side threshold: sodium strictly greater than 400 mg/100 g.
- Numerator: eligible logical occurrences above the threshold.
- Denominator: all eligible logical occurrences of the same dish type, not a composition-table total.
- Full embedded period audit: Main = 1/362 (0.28%); Side = 17/420 (4.05%). Values remain fractional internally and are formatted as percentages for display.

### Design scope

- The calculation helpers were propagated into existing analytics rather than creating a parallel metric path.
- The Report visual system and print CSS were not restyled. `openReportSnapshot` changed only to use the deduplicated filtered plan collection.
- The redundant Nutrition summary block was removed because it had no remaining analytical role and no live references.

## Unfinished work

- There is no automated unit-test harness for the embedded JavaScript calculation helpers.
- Responsive breakpoints and print/PDF output were not exhaustively regression-tested in this checkpoint.
- The 102 logical occurrences classified as Unknown should be reviewed with the data owner before changing classification rules; they may represent valid non-Main/Side categories.
- No cleanup or refactor of the large single-file HTML architecture was attempted.

## Known issues

- `assets/Braised.png` is requested by the dashboard but is missing, producing an HTTP 404 during local preview.
- `/favicon.ico` is not present and produces an HTTP 404 during local preview.
- Git reports that the working copy of `vitality_kpi_dashboard_webapp.html` may be converted from LF to CRLF the next time Git rewrites it. `git diff --check` reports no whitespace errors.
- `.claude/launch.json` uses `npx --yes serve`; the first run can require package availability/download if `serve` is not already cached.

## Tests/checks already performed

- `git diff --check`: passed; only the informational LF-to-CRLF warning appeared.
- Embedded JavaScript parse check with Node `new Function(...)`: passed.
- `.claude/launch.json` JSON parse check: passed.
- HTML shell count check: exactly one opening/closing `html`, `head`, `body`, `style`, and `script` tag pair.
- Data audit against embedded `DATA.plan` and `DATA.meta`:
  - 888 raw plan rows -> 884 logical occurrences.
  - Four duplicate rows removed.
  - Main/Side/Unknown logical counts = 362/420/102.
  - High-sodium Main = 1/362; Side = 17/420.
- Real-browser local preview:
  - Page loaded with meaningful content and no error overlay.
  - Dashboard rendered for 23 May–10 Aug 2026; visible OPS score was 83.2%.
  - Removed `nutritionSummary` container count was zero.
  - Report tab navigation succeeded and rendered non-empty content.
  - Browser console warning/error collection was empty.
  - All observed dashboard assets loaded except the known `Braised.png`; `favicon.ico` was also absent.

## Next recommended patch

Add a small, non-UI regression test harness around `excelDate`, `occurrenceDishType`, `logicalOccurrenceKey`, `deduplicatePlanOccurrences`, `periodPlanMetrics`, and the two high-sodium KPI calculations. Include fixtures for duplicate rows, blank vs non-empty `MenuSection`, Unknown categories, threshold boundary equality, current/previous periods, and report snapshots. Do this before any further dashboard feature or styling work.

## Things that must not be changed

- Do not make new feature changes from this checkpoint without explicit approval.
- Do not restyle or reorganize the Report tab, Report Action Plan, Report Follow-up, Manager Feedback, report metadata/signatures, KPI table, or print/PDF CSS as part of Dashboard work.
- Do not change RAG semantics, KPI thresholds, KPI weights, category scoring, or source data to make displayed results look better.
- Do not revert logical occurrence deduplication or restore raw plan-row counting for occurrence-based metrics without a documented business decision.
- Do not return to broad substring Main/Side matching; review Unknown values with the data owner first.
- Do not change the logical occurrence key casually; Unit, Chef, MealTime, date, RecID, and DishType all preserve business scope.
- Do not re-add the redundant `nutritionSummary` card unless a distinct approved analytical purpose is defined.
- Do not modify unrelated assets, data files, Report Print PDFs, or the locked Dashboard tokens in `STYLE_GUIDE.md`.
