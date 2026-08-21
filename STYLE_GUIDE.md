# Dashboard Style Guide

> **Scope: Dashboard tab ONLY.**
> The Report tab is explicitly out of scope for this guide and must not be
> restyled to match it. See [§0 Report Exclusion](#0-report-exclusion) below.

---

## 0. Report Exclusion

**The Dashboard style system MUST NOT automatically be applied to the Report tab.**

The Report tab (`vitality_kpi_dashboard_webapp.html`, `report-*` / `management-*`
components, Report Print assets, print/PDF CSS) has its own intentionally
customized visual system. It is a separate product surface with its own
typography, spacing, card structure, and print rules.

Preserve, unless the user makes a separate, explicit Report-specific request:

- Report structure and layout
- Report typography
- Report cards / sections
- Report KPI table
- Report Action Plan
- Report Follow-up
- Manager Feedback
- Report metadata / Report ID layout
- Signatures
- Print / PDF CSS

Do not:

- propagate Dashboard typography into the Report
- propagate Dashboard card radius into the Report
- propagate Dashboard status pills into the Report
- propagate Dashboard card styles into the Report
- modify report table density
- modify report section headings
- modify print rules
- change Report colors merely to match the Dashboard
- reorganize Report sections

Dashboard and Report may share semantic **meaning** (e.g. what "On Target" or
"Action Required" means) without sharing visual **presentation**. Any future
dashboard-standardization patch must preserve the Report tab exactly unless
the user explicitly requests a Report change.

---

## 1. Scope

This guide governs only the Dashboard tab:

- dashboard navigation context
- dashboard filters
- OPS hero
- category summaries (Nutrition, Cooking, Menu)
- KPI Performance Summary
- weekly trend
- Nutrition analytics (Energy, Protein, Fibre/Carb, Salt/Sodium, Sugar, Fat
  Quality, Nutrient Dense, Junk Food / Nutri-Score E)
- Cooking analytics (method mix, healthy cooking, deep-fried)
- Menu analytics (diversity, repetition, composition, protein rotation)
- Weekly KPI Heatmap
- Performance Rankings
- Risk / Impact / Action Plan (Dashboard instance)
- Key Insights
- Priority Signals
- other Dashboard-only analytical components

It does **not** govern the Report tab, Report KPI table, Report executive
summary, Report metadata, Report Action Plan, Report Follow-up, Manager
Feedback, Prepared By, signatures, Report ID layout, or print/PDF layout.

---

## 2. Design Principles

The Dashboard should be:

- compact
- modern
- professional
- analytical
- decision-oriented
- visually balanced
- information-dense but readable
- consistent across component families
- restrained in decoration
- not excessively rounded
- not overly spacious

Avoid:

- oversized cards
- excessive empty space
- too many font sizes
- too many icon scales
- too many border-radius values
- decorative colors without semantic meaning
- repeated KPI information without analytical value

---

## 3. Brand Colors (fixed)

**Primary Navy — `#001B33`**
Use for: OPS hero, major dashboard emphasis, navigation, high-level executive
identity.

**Brand Yellow — `#FFBF00`**
Use for: selected/active dashboard accents, focus, emphasis against navy.
Do **not** use Brand Yellow as RAG Amber.

---

## 4. Neutral Palette

| Token | Value |
|---|---|
| Page Background | `#F6F7FB` |
| Card Background | `#FFFFFF` |
| Soft Background | `#F8FAFC` |
| Primary Border | `#E7E9F0` |
| Primary Text | `#172033` |
| Secondary Text | `#64748B` |
| Muted Text | `#6F7789` |

Avoid introducing additional, visually indistinguishable neutral shades.

---

## 5. RAG System (locked, Dashboard-only)

RAG meaning must remain consistent throughout the Dashboard.

**Green / Good**

| Token | Value |
|---|---|
| Text | `#15803D` |
| Strong Text | `#14532D` |
| Soft Background | `#DCFCE7` |
| Border | `#86EFAC` |

**Amber / Needs Attention**

| Token | Value |
|---|---|
| Text | `#92400E` |
| Accent | `#D97706` |
| Soft Background | `#FEF3C7` |
| Border | `#FCD34D` |

**Red / Action Required**

| Token | Value |
|---|---|
| Text | `#991B1B` |
| Accent | `#DC2626` |
| Soft Background | `#FEE2E2` |
| Border | `#FCA5A5` |

Rules:

- RAG is semantic — never decorative
- category colors must never double as RAG colors
- do not invent per-section RAG shade variants
- the Report may use a different visual treatment for the same semantic states

---

## 6. Category Colors

| Category | Value |
|---|---|
| OPS | `#001B33` |
| Nutrition | `#3B82C4` |
| Cooking | `#269B6A` |
| Menu | `#C58A18` |

Use only for identity — icon, accent, subtle indicator, relevant chart series.
RAG status takes precedence over category identity when representing
performance.

---

## 7. Typography (compact fixed scale)

| Role | Size / Weight |
|---|---|
| OPS / Hero Value | 32px / 700 |
| Standard KPI Value | 24px / 700 |
| Dashboard Product Title | 18px / 700 |
| Section Heading | 16px / 700 |
| Subsection Heading | 14px / 600–700 |
| KPI Label / Body / Status | 12px / 400–600 |
| Helper / Annotation | 11px / 400 |

Rules:

- screen helper text must never fall below 11px
- avoid arbitrary KPI values such as 17px, 20px, 27px, 29px, 31px
- use mainly 400, 600, 700 weights; avoid widespread 800 weight
- sentence case by default; uppercase only for deliberate micro-labels

These rules do not apply to Report typography.

---

## 8. Spacing System

| Token | Value | Use |
|---|---|---|
| micro gap | 4px | |
| small gap | 8px | |
| standard internal gap | 12px | |
| main grid gap | 14px | |
| standard component padding | 16px | |
| major dashboard card padding | 18px | |
| section separation | 20px | |
| major visual separation | 24px | |

Avoid random spacing values when a defined token is sufficient. Keep the
Dashboard compact.

---

## 9. Border Radius

| Element | Radius |
|---|---|
| Main dashboard card | 16px |
| Secondary / analytical subcard | 12px |
| Small control / chip | 8px |
| Status pill | 999px |
| Circular icon | 50% |

The OPS hero may remain a defined exception. Avoid excessive rounded-square
styling. These rules do not apply to Report components.

---

## 10. Border + Shadow

- Standard border: `1px solid #E7E9F0`
- One restrained major-card shadow only
- Internal/secondary cards rely on border, subtle background, and spacing
  rather than multiple heavy shadows

---

## 11. Icon System

| Scale | Size |
|---|---|
| Small analytical icon | 24px |
| Medium icon | 32px |
| Category icon | 48px |
| Feature icon | 64–72px |

Rules:

- consistent icon family and stroke/fill language
- transparent SVG or PNG
- no arbitrary 21/23/25/27/28/30px variants
- feature icons only where the design genuinely requires larger illustration
- icons must not be enlarged simply to occupy empty space

---

## 12. Card Families

**Hero Card** — high-level executive metrics only (e.g. OPS).

**Category Summary** — Nutrition, Cooking, Menu; one consistent structure.

**Analytics Card** — default detailed analytical shell: white background,
fixed border, consistent header, internal analytical zones, standard KPI
hierarchy, controlled chart sizing. Reference: the existing Energy Analytics
structure.

**Secondary Card** — rankings, secondary diagnostics, small supporting
summaries. Reference: existing Performance Ranking cards.

**Diagnostic Matrix** — Weekly KPI Heatmap, Protein Rotation, and other
matrix-like weekly analytics. Flatter and denser than KPI cards.

**Action / Insight Card** — Dashboard-only actions, risks, insights, priority
signals. One consistent family. Never used to modify the Report Action Plan.

---

## 13. Section Headers

Standard structure: Title / optional subtitle / optional date-context
metadata.

- title: 16px / 700
- subtitle/meta: 11–12px
- consistent alignment, clean mobile wrapping
- date context stays secondary

Reference: the current `.section-head` pattern.

---

## 14. KPI Display

Primary displayed KPI is always the normal business metric (%, kcal, g, mg,
count) — never weighted contribution.

Preferred hierarchy:

1. KPI Label
2. Raw Result
3. Target
4. RAG Status
5. Optional Delta
6. Optional Weight (secondary)

---

## 15. Status Treatment

One compact RAG pill for Dashboard KPI statuses (On Target, Needs Attention,
Action Required, No Data):

- soft RAG background
- semantic RAG text
- restrained border
- compact dimensions

Does not affect existing Report status treatment.

---

## 16. Chart System

Standard structure: Header → optional controls → plot → legend → optional
annotation/summary.

Rules:

- standardize chart height by visual family; avoid unnecessary fixed height
  and large dead areas
- horizontal scrolling only for genuinely dense matrices
- a chart and a KPI card should not duplicate identical information without
  additional analytical value
- legends stay compact; title hierarchy stays consistent

---

## 17. Component Families

**Nutrition** — Energy, Protein, Fibre/Carbohydrate, Salt/Sodium, Sugar, Fat
Quality, Nutrient Dense, Junk Food/Nutri-Score E. To be standardized around a
common card shell, analytical header, icon scale, KPI value hierarchy,
spacing, RAG treatment, and diagnostic structure. Protein should not remain a
separate visual language unless explicitly approved. Nutrient Dense and Junk
Food conceptually belong under Nutrition.

**Cooking** — Method Mix, Healthy Cooking, Deep-Fried analytics, Cooking
summaries. Larger feature imagery permitted only within method tiles; normal
KPI summaries use the standard analytics hierarchy; content-driven heights;
repeated values must add new analytical context.

**Menu** — Diversity, Repetition Rate, Unique Dishes, Repetitive Dishes,
Menu Composition, Menu KPI Summary, Weekly Diversity Map, Protein Rotation.
Semantic roles: Diversity = summary, Repetition Rate = summary, Unique Dishes
= supporting evidence, Repetitive Dishes = diagnostic, Weekly Diversity =
temporal diagnostic, Protein Rotation = temporal/composition diagnostic, Menu
Composition = aggregate composition.

**Cross-KPI** — Weekly KPI Heatmap, Performance Rankings, Risk/Impact/Action
Plan, Key Insights, Priority Signals. Consistent headers, spacing, secondary
card styles, action/insight styles, semantic RAG treatment. Diagnostic
matrices stay visually distinct from normal KPI cards.

---

## 18. Duplicate Visual Rule

The same KPI may appear twice only when the second representation answers a
different question.

Valid: KPI summary + weekly trend · KPI summary + offender list · aggregate
composition + weekly matrix.

Potentially redundant: the same raw KPI number shown in two adjacent summary
blocks.

Do not remove duplicates automatically — flag them for explicit approval.

---

## 19. Responsive Rules

- content-driven card heights, minimal dead space
- logical stacking
- readable minimum typography
- horizontal scrolling only for genuinely dense diagnostics
- compact navigation
- charts adapt rather than simply shrink text

Responsive standardization comes after main component dimensions are locked.

---

## 20. Process Rule (for future Dashboard patches)

Before any Dashboard UI patch:

1. read `AGENTS.md` (if present)
2. read this `STYLE_GUIDE.md`
3. confirm the change targets the Dashboard, not the Report
4. identify the relevant Dashboard component family (§17)
5. use existing approved tokens (§3–§11)
6. avoid new colors / radii / font sizes / icon sizes unless explicitly requested
7. do not modify the Report tab
8. preserve unrelated Dashboard sections
