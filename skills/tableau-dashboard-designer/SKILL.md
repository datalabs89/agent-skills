---
name: tableau-dashboard-designer
description: Expert Tableau agent skill to create, audit, lint, and redesign Tableau dashboards (.twb/.twbx) using official Tableau Document Schemas, Document API, Visualization-Linting rules, executive layout containers, and elite Tableau Public design patterns.
---

# Tableau Dashboard Designer & Redesign Skill

This skill equips the agent to programmatically inspect, audit, build, and redesign Tableau workbooks (`.twb` and `.twbx`) according to Tableau best practices, official schemas, and award-winning Tableau Public design patterns.

## Supported Repositories & Tooling
- **`tableau/document-api-python`** (`C:\Users\User\document-api-python`): Inspects & swaps datasources, connections, fields, and workbook parameters.
- **`tableau/tableau-document-schemas`** (`C:\Users\User\tableau-document-schemas`): Official XSD schemas (`twb_2026.1.0.xsd`, `twb_2026.2.0.xsd`) for syntactic validation.
- **`tableau/Visualization-Linting`** (`C:\Users\User\Visualization-Linting`): Rules for zero-baseline preservation, non-deceptive axes, and contrast standards.
- **`tableau/tableau_langchain`** (`C:\Users\User\tableau_langchain`): Agentic workflows and query patterns.
- **`tableau_dashboard_agent`** (`C:\Users\User\tableau-dashboard-agent`): The local Python engine and CLI.

---

## 🏛️ Anatomy of an Elite Executive Dashboard (Case Study: Superstore Performance Overview)
Analysis derived from top-performing Tableau Public executive dashboards (`SuperstorePerformanceOverview_17018791727490`):

### 1. Grid Architecture & Layout Composition
* **Aspect Ratio**: Standardized 16:10 or 16:9 widescreen (e.g. 1850×1230 or 1440×900) to ensure zero horizontal/vertical scrollbars on modern executive laptops.
* **Left Navigation Rail**: Narrow vertical bar (width ~60px) housing the corporate logo, navigation icons (Overview vs. Drill-down), and filter toggles.
* **Vertical KPI Column (Inverted Pyramid)**: Left-side column (width ~320px) stacking 4 high-priority BAN cards (Sales, Profit, Quantity, Return Rate).
* **Analytical Card Matrix**: Right side containing a 2×3 or 2×2 grid of comparative charts (Category, Region, Segment, and Top N Breakdown).

### 2. High-Impact BAN Micro-Dashboard Formula
Rather than a plain number, each KPI card should function as an independent micro-dashboard containing:
1. **Metric Caption**: Small uppercase label (e.g. `SALES`).
2. **Big Ass Number (BAN)**: Prominent metric value (24–28pt `Tableau Bold`).
3. **YoY Delta Badge**: Dynamic badge with directional arrow and color-coding (`▲ +14.2%` in mint `#32B593` or `▼ -3.8%` in coral `#FE4F60`).
4. **Integrated Sparkline**: 12-month or 4-year area/line sparkline embedded directly inside the card to communicate trajectory without leaving the summary level.

### 3. Interactive Web-App UX Patterns
* **The "Tableau De-Highlight" Trick**: Tableau by default greys out other sheets when a button is clicked. Expert dashboards eliminate this by creating a dummy dimension `[H] = "H"` and binding a Highlight Action (`tsc:brush`) with `field-captions="H"` targeting the button sheet.
* **Custom Pill Buttons**: Replace standard parameter dropdowns with custom marks/sheets styled as interactive toggle pills (`button-param`, `button-year`).
* **Collapsible Filter Drawers**: Floating containers driven by boolean parameters (`Toggle Categories`, `Toggle Tops`) that expand and collapse cleanly.
* **Two-Tier Architecture**:
  * **Tab 1: Executive Overview** (High-level decision support, BANs, trends, comparative bars).
  * **Tab 2: Order Details** (Granular tabular audit view with multi-column quick filters).

### 4. Executive Period Logic (CY vs. PY)
* Dynamic calculations linked to a `[Select Year]` parameter:
  * **Current Year (CY)**: `IF YEAR([Order Date]) = [Select Year] THEN [Sales] END`
  * **Prior Year (PY)**: `IF YEAR([Order Date]) = [Select Year] - 1 THEN [Sales] END`
  * **YoY Delta %**: `(ZN(SUM([CY])) - ZN(SUM([PY]))) / ABS(ZN(SUM([PY])))`
  * **Formatted Badge**: `IF [YoY %] >= 0 THEN '▲ +' + STR(ROUND([YoY %]*100, 1)) + '%' ELSE '▼ ' + STR(ROUND([YoY %]*100, 1)) + '%' END`

### 5. Universal Design System & Palettes
* **Typography**: Stick strictly to `Tableau Bold` (headers/metrics) and `Tableau Book` (labels/body) to ensure cross-platform fidelity across Windows, Mac, Tableau Server, and Tableau Cloud.
* **Themes Available**:
  * `executive-light`: Canvas `#F1F5F9`, Cards `#FFFFFF`, Accent `#2563EB`.
  * `executive-dark`: Canvas `#0B0F19`, Cards `#151D2F`, Accent `#38BDF8`.
  * `minimalist-slate`: Canvas `#FFFFFF`, Cards `#F8FAFC`, Accent `#0F766E`.
  * `periwinkle-executive`: Canvas `#DFE3F2`, Cards `#FFFFFF`, Accent `#1E1ACB`, Positive `#32B593`, Negative `#FE4F60`.
  * `digital-marketing`: Canvas `#F5F7FA`, Cards `#FFFFFF`, Accent `#4D56F6` (Electric Indigo), Amber `#AF8A05`, Emerald `#7ABD9A`.

---

## 📈 Case Study 2: Digital Ads Performance Dashboard (Rolling Period Engine & Funnel Matrix)
Analysis derived from high-performing marketing executive dashboards (`DigitalAdsPerformanceDashboard`):

### 1. Dynamic Rolling Period Engine (Anchored to Max Date)
* **Anchor Formula**: `{ MAX([Date]) }` — allows dynamic relative slicing regardless of whether the dataset is real-time or snapshot.
* **Period Switcher Pill Strip**: Single horizontal button strip for:
  `This Week` | `Last 7 days` | `Last 14 days` | `Last 28 days` | `Last 30 days` | `Last 90 days` | `This Year`
* **Adaptive Sparkline Time Grain**: Automatically aggregates sparklines by:
  * **Day**: When viewing < 30 days.
  * **Week**: When viewing 90 days (`DATETRUNC('week', [Date])`).
  * **Month**: When viewing full year (`DATETRUNC('month', [Date])`).
* **Dynamic Comparison Context**: Automatically calculates prior periods (e.g. `Last 7 days` vs. `Previous 7 days` (days -13 to -7)) and updates label text (`vs Previous 7 days: +0.3%`).

### 2. The 4-Stage Marketing Funnel Matrix
Customer acquisition funnel structured as a vertical flow with inline efficiency rates:
1. **Top Funnel (Click)**: Total Clicks + Cost Per Click (CPC) + Click-Through Rate (CTR).
2. **Engagement (Install)**: Total Installs + Cost Per Install (CPI) + Install Conversion Rate (Install CVR).
3. **Activation (Signup)**: Total Signups + Cost Per Acquisition (CPA) + Signup Conversion Rate (Signup CVR).
4. **Revenue (Purchase)**: Total Purchases + Cost Per Purchase (CPP/CPS) + Purchase Conversion Rate (Purchases CVR).

### 3. Diagnostic Tables with Inline Sparklines
* Combining cross-tabs with embedded micro-sparklines (`map channel table` + `map channel line`).
* Enables stakeholders to see both exact tabular KPIs (Spend, Conversions, ROAS) and the trend trajectory side-by-side without leaving the view.

---


### Learned Model: reference_digital_ads
* **Source**: Local File | **Canvas**: 1900x1050
* **Extracted Palette**: Canvas `#EEEEEF`, Accent `#B4C0E1`, Positive `#7ABD9A`, Negative `#E1AA88`
* **Key Learned Calculations**:
  * `Install var %` (Period/Date): `IF [Parameters].[매개 변수 1] = 'This Week' THEN      ((        SUM(IF DateTrunc('day'...`
  * `Date Filter` (Period/Date): `Case [Parameters].[매개 변수 1] When 'This Week' Then DateTrunc('day',[Date]) >= DateT...`
  * `Max Date` (LOD): `{ MAX([Date])}`
  * `Date Period` (Period/Date): `DATE(Case [Parameters].[매개 변수 1] When 'This Week' Then DateTrunc('day',[Date]) Whe...`
* **Interactive Actions**: 필터1 (tsc:tsl-filter)


### Learned Model: SuperstorePerformanceOverview_17018791727490
* **Source**: Tableau Public | **Canvas**: 1850x1230
* **Extracted Palette**: Canvas `#FFFFFF`, Accent `#ABB2F3`, Positive `#3A7D3C`, Negative `#C63027`
* **Key Learned Calculations**:
  * `PY Parameter DNF` (Dynamic Metric): `IF SUM([PY Sales (copy)_1064819864315519014]) < 0 THEN '-' ELSE '' END
 +
 IF [Par...`
  * `Top N Selection` (Dynamic Metric): `CASE [Parameters].[Parameter 3]
 
 WHEN 1 THEN [Customer ID]
 WHEN 2 THEN [Manufac...`
  * `Max Bar Color` (LOD): `{FIXED [Calculation_1064819864244207623]: SUM([CY Sales (copy)_1064819864314937381...`
  * `Top N Selection Name` (Dynamic Metric): `CASE [Parameters].[Parameter 3]
 
 WHEN 1 THEN [Customer Name]
 WHEN 2 THEN [Manuf...`
* **Interactive Actions**: Un-H Year Buttons (tsc:brush), Un-H NavBars (tsc:brush)


### Learned Model: RWFDCallCenterDashboard_16484804651650
* **Source**: Tableau Public | **Canvas**: 1600x900
* **Extracted Palette**: Canvas `#FFFFFF`, Accent `#4C8CAA`, Positive `#10B981`, Negative `#FF819F`
* **Key Learned Calculations**:
  * `@Sort Top Agents (copy)` (Dynamic Metric): `Case [Parameters].[Parameter 4]
 when "Average Handle Time" then [LinPack_84325527...`
  * `AHT - Avg Handle Time  YTD  (Current Year) (for trends) (copy)` (Table Calc): `IF ATTR([LinPack_133017178160914243]) <= [Parameters].[LinPack_602727554575955041]...`
  * `AHT (for selected Agent)` (LOD): `MAX( IF [Calculation_1647754575248490496] THEN {INCLUDE [Agent] : ZN([LinPack_8432...`
  * `CSAT (for selected Agent)` (LOD): `MAX( IF [Calculation_1647754575248490496] THEN {INCLUDE [Agent] : ZN([LinPack_7634...`
* **Interactive Actions**: dummy HL - talk time / agent 2 (tsc:brush), #RWFD Season 2 (unknown), dummy hl3 - aht agent 2 (tsc:brush), Filter using heatmap (tsc:tsl-filter)


### Learned Model: TableauBootcamp-BuildanEffectiveDashboard
* **Source**: Tableau Public | **Canvas**: 1300x750
* **Extracted Palette**: Canvas `#FFFFFF`, Accent `#AAAAFF`, Positive `#10B981`, Negative `#FF557F`
* **Key Learned Calculations**:
  * `❖ - Session Duration` (Dynamic Metric): `CASE [Parameters].[Parameter 1]
 WHEN "Average Session Duration (s)" THEN "❖" END`
  * `Metric CY` (Dynamic Metric): `IF [Months (copy)_2712855841805713411] = [Parameters].[Year Parameter] AND [Calcul...`
  * `Selected Dimension` (Dynamic Metric): `CASE [Parameters].[Parameter 2]
 WHEN "Web Pages" THEN [PagePath]
 WHEN "Key Actio...`
  * `Metric CY (for trends)` (Dynamic Metric): `IF [Months (copy)_2712855841805713411] = [Parameters].[Year Parameter]
 //[Months]...`

## Critical Tableau XML Architecture & Diagnostic Rules
1. **Worksheet Unique Identity Constraints**: Every worksheet `<simple-id>` must have a unique UUID formatted with standard hyphens `f"{{{str(uuid.uuid4()).upper()}}}"` matching schema pattern `\{[0-9A-Fa-f]{8}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{12}\}`. Duplicating simple-ids when cloning worksheets causes fatal identity constraint violations.
2. **Mandatory Zone Attributes**: Tableau Document Schema strictly requires all 5 attributes on every `<zone>`: `id` (unsignedInt), `x` (int), `y` (int), `w` (int), and `h` (int). Omitting `x, y, w, h` causes Tableau Desktop to abort workbook load.
3. **Dashboard Child Element Order**: Schema content model for `<dashboard>` is strictly `(((layout-options?)|(repository-location?)),style?,size?,datasources,datasource-dependencies*,zones,devicelayouts?,simple-id)`. `<simple-id>` must ALWAYS be positioned after `<zones>`.
4. **Workbook Root Child Sequence**: Schema content model requires `worksheets -> dashboards -> windows -> thumbnails? -> external`. Re-attaching `<windows>` after `<external>` violates root schema sequence.
5. **Calculated Field Derivation Prefix**: When referencing user-defined aggregate measures (`SUM([Profit]) / SUM([Sales])`), the column-instance name prefix is `usr:` (e.g. `[usr:Calculation_...:qk]`), NOT `user:`.


### Learned Model: Consumerdutyscorecard
* **Source**: Tableau Public | **Canvas**: 1380x820
* **Extracted Palette**: Canvas `#F9FAFD`, Accent `#7F9BFE`, Positive `#43CA86`, Negative `#EF4444`
* **Key Learned Calculations**:
  * `line label` (LOD): `if DATETRUNC('month',[Calculation_445293471865778217])
 = {fixed DATETRUNC('quarte...`
  * `Order date 2` (Period/Date): `DATEADD('year',3,[Order Date])`
  * `Max month -1` (Period/Date): `[Calculation_445293471865778217]=
 DATEADD('year',-1,{MAX([Calculation_44529347186...`


### Learned Model: CustomerSupportCaseDemo
* **Source**: Tableau Public | **Canvas**: 1500x820
* **Extracted Palette**: Canvas `#EFEFF8`, Accent `#1CD6E6`, Positive `#05AF7F`, Negative `#E5592E`
* **Key Learned Calculations**:
  * `Days open` (Period/Date): `if [Calculation_1900237581220421637]!='Severe' then ROUND( (DATEDIFF('day',[Orde...`
  * `ref` (LOD): `{FIXED  [Region] ,[Calculation_1900237581209280512] :max( ({INCLUDE  [Calculation_...`
  * `WINDOW_MAX(COUNTD(Order ID))` (Table Calc): `WINDOW_MAX(COUNTD([Order ID]))`
  * `Last 12 months` (Period/Date): `[Order Date]> DATEADD('year',-1, {MAX([Order Date])})`
* **Interactive Actions**: Filter1 (tsc:tsl-filter), Filter2 (tsc:tsl-filter)

## Quick CLI Reference
```bash
# 1. Audit / Lint
python -m tableau_dashboard_agent.cli lint "<file.twb|twbx>"

# 2. Visual Design Scorecard
python -m tableau_dashboard_agent.cli scorecard "<file.twb|twbx>"

# 3. Apply Theme (Light / Dark / Minimalist / Periwinkle / Digital Marketing)
python -m tableau_dashboard_agent.cli theme-apply "<file.twb|twbx>" --theme digital-marketing -o "marketing.twbx"

# 4. Redesign into Executive Layout
python -m tableau_dashboard_agent.cli redesign "<file.twb|twbx>" --output "redesigned.twbx" --theme periwinkle-executive

# 5. Validate against official Tableau XSD
python -m tableau_dashboard_agent.cli validate "<file.twb>"
```

