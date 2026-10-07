# Functional Specification: PI Purchase V/s Profit Dashboard Module
**Document Version:** 1.0  
**Project:** BNS Sales Intelligence Platform  
**Module:** Parallel Import (PI) Purchase, Profit, Margin & Sales Analytics (`PI Purchase V/s Profit`)  
**Date:** September 2026  
**Primary Data Reference:** `PI Data File (till Jul'26) - Updated.xlsx`  
**Reference Document:** `PI Purchase vs Profit.docx`  

---

## Document Control & Approvals

| Role | Name & Designation | Signature | Date |
| :--- | :--- | :--- | :--- |
| **Author** | **Amit Porwal**<br>IT - Business Analyst | ______________________________ | 09-Sep-2026 |
| **Reviewer** | **Amit Sanandiya**<br>IT – Project Manager | ______________________________ | 09-Sep-2026 |
| **Approver** | **Commercial Director / Head of PI Purchasing**<br>BNS Group Commercial Operations | ______________________________ | 09-Sep-2026 |

---

## 1. Executive Summary & Business Objective

The **PI Purchase V/s Profit** dashboard is an enterprise-grade, managerial, operational, and commercial business intelligence module designed and built for the **BNS Sales Intelligence Platform**.

Parallel Importation (PI) within pharmaceutical distribution involves purchasing branded European pharmaceutical products across European Economic Area (EEA) member states at regulated, favorable pricing, re-packaging or re-labelling them under UK Medicines and Healthcare products Regulatory Agency (MHRA) parallel import product licences (PLPI), and distributing them to UK retail pharmacies, dispensing doctors, and wholesalers.

The module provides executive management, PI purchasing teams, buyers, and commercial leadership with end-to-end visibility across seven core operational dimensions:
1. **Procurement Commitments & Profit Margins:** Tracking monthly purchase value commitments against expected gross profit and expected margin percentages across all four dedicated purchasing buyers (Louise, Manisha, Luca, and Raffaella).
2. **Product Lifecycle Bifurcation (Old vs. New Lines):** Clear segregation between established mature lines ("Old Products" / "Regular Lines") and newly commercialized licenses ("New Products" / "New Lines").
3. **Territory & Country Sourcing Matrix:** Granular monitoring across 22 European source countries (Greece, Spain, Germany, France, Italy, Austria, Belgium, Portugal, Ireland, Netherlands, Norway, Czech Republic, Romania, Bulgaria, Slovakia, Poland, Hungary, Lithuania, Slovenia, Latvia, Croatia).
4. **Strategic Volume & High-Impact Diagnostics:** Identification of portfolio concentration risk via the "Removed Top 5 Lines" analysis.
5. **New License Commercialization Pipeline:** Real-time operational surveillance of 75 parallel import licences granted by the MHRA across 7 operational milestones (MAH Objection, Price Issue, Variation, Not On Order, Awaiting MAH, In Labelling / On Order, Stock Received).
6. **Prescription Cost Analysis (15% PCA) UK Market Surveillance:** Benchmarking BNS actual daily and month-to-date sales quantities against the UK National Health Service (NHS) Prescription Cost Analysis (PCA) baseline demand.
7. **Overstock Working Capital Surveillance:** Identification of inventory tied up in excessive stock cover (>100 to >400 days of stock).

---

## 2. Source Data Architecture & Sheet Mapping

The module uses all operational sheets in `PI Data File (till Jul'26) - Updated.xlsx` as its single source of truth:

| # | Sheet Name | Target Dashboard Section | Purpose & Metrics |
| :--- | :--- | :--- | :--- |
| 1 | `Purchase 2` | Section 3: PI Purchase vs Profit | Monthly buyer-level purchase, profit, and margin data (Jan–Aug) for Old, New, and Overall PI. |
| 2 | `Buyer` | Section 4: Buyer Performance Matrix | Country-by-buyer monthly procurement values, expected profits, and margin percentages across 22 European nations. |
| 3 | `New License` | Section 6: New License Pipeline | Status summary distribution (7 status buckets, 75 licences) and detailed product master table. |
| 4 | `Sales` | Section 7: PI Product Sales | Monthly sales revenue, gross profit, and margin % for Regular Lines, New Lines, and Overall PI. |
| 5 | `15% PCA` | Section 8: 15% PCA UK Market | Daily & MTD NHS PCA volume comparison against BNS actual sales across 55 monitored PI products. |
| 6 | `Overstock` | Section 9: Overstock Inventory | 8 overstocked inventory items with stock volume, true unit cost, stock value, and days of stock cover. |
| 7 | `Additional watch Purchase` & `Updated Summary` | Section 5: Purchase Analysis | Unique product counts, physical boxes purchased, purchase value, potential profit, and margin for Overall vs. Removed Top 5. |
| 8 | `Additional Watch Sales` | Section 7: Sales Volume Insights | Product counts, physical box sales throughput, and sales values. |

*Note: In accordance with project requirements, `Raw` and `Raw File` are backend source sheets and are not exposed as UI screens.*

---

## 3. Global Dashboard Architecture

### 3.1 Header Component
- **Module Title:** `PI Purchase V/s Profit`
- **Subtitle:** `Parallel Import Purchase, Profit, Margin & Sales Performance`
- **Last Updated Indicator:** Formatted system timestamp (`Updated: 09 Sep 2026, 10:45`).
- **Reporting Period Badge:** `Data available through Jul'26`.
- **Global Actions:**
  - `🔄 Refresh`: Resets all applied filters and returns visualizations to default baseline state.
  - `📥 Export Report`: Dropdown offering direct exports for Purchase Table (CSV), Buyer Matrix (CSV), New Licenses (CSV), 15% PCA (CSV), Overstock (CSV), and Print / Save to PDF.

### 3.2 Global Multi-Dimensional Filter Bar
Located immediately beneath the header, providing interactive cross-filtering across all dashboard components:
1. **Financial Year:** Single-select dropdown (`All Years (FY26)`, `FY 2026`).
2. **Month:** Single-select dropdown (`All Available (Jan–Aug)`, `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`).
3. **Buyer:** Multi-select/Single-select (`All Buyers`, `Louise`, `Luca`, `Manisha`, `Raffaella`).
4. **Country:** Dropdown containing all 22 sourcing countries.
5. **Product Type:** Segment selector (`Overall PI`, `Old Products`, `New Products`).
6. **Product Category:** Dropdown (`All Categories`, `Parallel Import`, `Generic to PI`, `Fridge Lines`).
7. **Search Part / Code:** Instant text search matching Lax Part Numbers, Catalog Numbers, and product descriptions.
8. **Action Buttons:** `Apply Filters` and `Reset`.

---

## 4. Section Specifications

### 4.1 Section 2: Top KPI Summary
Positioned at the top of the dashboard, displaying six compact cards engineered to fit on a single desktop row:

| KPI Card | Metric Definition | Formula | Source Sheet | Jul'26 / YTD Value | Visual Theme |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. Total PI Purchase** | Cumulative or monthly purchase value | $\sum \text{Purchase Amount}$ | `Purchase 2` | **£52.23M** (YTD) / **£8.45M** (Jul) | Primary Blue (`#1a56db`) |
| **2. Total Expected Profit** | Expected gross profit on purchased volume | $\sum \text{Expected Profit}$ | `Purchase 2` | **£18.32M** (YTD) / **£2.72M** (Jul) | Success Emerald (`#10b981`) |
| **3. Expected Margin %** | Expected purchasing margin yield | $\frac{\text{Expected Profit}}{\text{Purchase Amount}}$ | `Purchase 2` | **35.08%** (YTD) / **32.25%** (Jul) | Purple Accent (`#8b5cf6`) |
| **4. PI Sales Revenue** | Realized customer sales revenue | $\sum \text{Sales Amount}$ | `Sales` | **£4.08M** (YTD) / **£557.6K** (Jul) | Cyan Accent (`#06b6d4`) |
| **5. PI Sales Profit** | Realized customer gross profit | $\sum \text{Sales Profit}$ | `Sales` | **£458.7K** (YTD) / **£61.8K** (Jul) | Orange Accent (`#f97316`) |
| **6. Sales Margin %** | Realized sales profit margin | $\frac{\text{Sales Profit}}{\text{Sales Amount}}$ | `Sales` | **11.24%** (YTD) / **11.08%** (Jul) | Pink Accent (`#ec4899`) |

---

### 4.2 Section 3: Main Section — PI Purchase V/s PI Profit
The primary operational and managerial view of the module.

#### A. Monthly Purchase vs Profit Combination Chart
- **X-Axis:** Month (`Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`).
- **Primary Y-Axis (Left, Currency):** Total Purchase (rendered as vertical blue bars) and Expected Profit (rendered as an emerald green line with point markers).
- **Secondary Y-Axis (Right, Percentage):** Expected Margin % (rendered as a dashed purple line).
- **Interactive Toggles:**
  - `[Overall PI]`
  - `[Old Products]`
  - `[New Products]`
- **Tooltip:** Displays exact currency values formatted as `£X.XXM` or `£XXX.XK` and margin to two decimal places.

#### B. Buyer-Grouped Management Table
- **Layout:** Grouped hierarchically by Buyer with full-width dark header banners:
  - `👤 BUYER: LOUISE`
  - `👤 BUYER: MANISHA`
  - `👤 BUYER: LUCA`
  - `👤 BUYER: RAFFAELLA`
- **Columns (Grouped Multi-Level Headers):**
  - **Buyer / Month** (Sticky first column)
  - **OLD PRODUCTS:** Purchase | Profit | Margin %
  - **NEW PRODUCTS:** Purchase | Profit | Margin %
  - **OVERALL PI:** Total Purchase | Total Profit | Total Margin %
- **Subtotals & Grand Total:**
  - Each buyer section concludes with a visually highlighted subtotal row (`Louise Total`, `Manisha Total`, etc.).
  - The table concludes with the prominent `🌟 ALL BUYER OVERALL` row summing procurement commitments across all buyers.
- **Visual Styling:**
  - Sticky header row during vertical scrolling.
  - Sticky first column during horizontal scrolling on smaller screens.
  - Currency formatted to `£2.20M`, `£16K`, etc.
  - Percentage badges with conditional color styling (Green $\ge 20\%$, Blue $\ge 10\%$, Yellow $<10\%$).

---

### 4.3 Section 4: Buyer Performance Matrix
- **Source Sheet:** `Buyer`
- **Territory Coverage:** 22 European nations categorized by buyer:
  - **Louise:** Greece, Spain
  - **Luca:** Germany, France, Italy, Austria
  - **Manisha:** Belgium, Portugal, Ireland, Netherlands, Norway
  - **Raffaella:** Czech Republic, Romania, Bulgaria, Slovakia, Poland, Hungary, Lithuania, Slovenia, Latvia, Croatia
- **Columns:** `Country`, `Buyer`, `Purchase`, `Exp. Profit`, `Exp. Margin %`.
- **Interactive Capabilities:**
  - **Month Selector:** `Full Year Total`, `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`.
  - **Sorting:** By Purchase descending, Profit descending, Margin % descending, or Country alphabetical.
  - **Subtotal Rows:** Highlighted rows for `Louise Overall`, `Luca Overall`, `Manisha Overall`, `Raffaella Overall`, and `All Buyer Overall`.

---

### 4.4 Section 5: Purchase Analysis & Management Insights
- **Source Sheets:** `Updated Summary`, `Additional watch Purchase`
- **Metrics Tracked:**
  - **Unique Products:** Number of distinct parallel import SKUs procured.
  - **Total Boxes:** Total physical units/packs purchased.
  - **Purchase Value (£):** Monetary commitment.
  - **Potential Profit (£):** Forecasted commercial gross profit.
  - **Margin %:** Percentage yield.
- **Segment Toggles:**
  - `[Overall]`
  - `[Removed Top 5]`
  - `[Regular Lines]`
  - `[New Lines]`
- **Visualizations:**
  - Dual-bar monthly trend chart comparing Purchase Value vs Potential Profit (Feb to Jul).
  - **Top 5 Profit Impact Insight Card:** Dynamic analytical highlight showing the concentration of profit in the top 5 lines (e.g. in July, top 5 lines account for £734.5K or 36.2% of total profit with an 8.5% margin differential).

---

### 4.5 Section 6: New License Tracker
- **Source Sheet:** `New License`
- **Business Purpose:** Monitoring the regulatory and commercial onboarding pipeline of newly licensed PI lines.
- **7 Status Cards:**
  1. `MAH Objection` (0 products) — Regulatory challenge by Marketing Authorisation Holder.
  2. `Price Issue` (3 products) — Sourcing price exceeds commercial viability.
  3. `Variation` (3 products) — Packaging/artwork variation in progress.
  4. `Not On Order` (4 products) — Approved licence awaiting purchasing order.
  5. `Awaiting MAH` (7 products) — Pending MAH notification period.
  6. `In Labelling / On Order` (26 products) — Repackaging production or on active PO.
  7. `Stock Received` (32 products) — Successfully received in UK warehouse.
  - *Total Licences: 75 products.*
- **Interactive Filtering:** Clicking any status card immediately filters the product table below.
- **Status Distribution Chart:** Compact doughnut chart visualizing the 7-stage commercial pipeline.
- **Operational Master Table:**
  - Columns: `Country`, `Buyer`, `Lax Part No`, `Product Description`, `Granted Date`, `Buying Comments`, `Remarks`.
  - Instant text search across part number and product name.
  - Color-coded status badges for instant risk identification.

---

### 4.6 Section 7: PI Product Sales
- **Source Sheets:** `Sales`, `Additional Watch Sales`
- **Lifecycle Comparison Panels:**
  - **OLD PRODUCTS SALES:** Regular Lines sales (£3.71M cumulative, £414.2K profit, 11.17% margin).
  - **NEW PRODUCTS SALES:** New Launches sales (£372.1K cumulative, £37.7K profit, 10.13% margin).
  - **OVERALL PI SALES:** Total Portfolio sales (£4.08M cumulative, £451.9K profit, 11.07% margin).
- **Monthly Sales Trend Chart:**
  - Segment selector: `[Old Products]`, `[New Products]`, `[Overall PI]`.
  - Metric selector: `[Sales]`, `[Profit]`, `[Margin %]`.
- **Secondary Sales Volume Strip:** Displays Unique Lines (451), Boxes Sold (378K), Total Sales (£8.64M), Total Profit (£987.5K), and Margin (11.42%) for July 2026.

---

### 4.7 Section 8: 15% PCA (Prescription Cost Analysis)
- **Source Sheet:** `15% PCA`
- **Business Purpose:** Identifying total UK market volume demand from NHS Prescription Cost Analysis and measuring BNS actual sales volume achievement.
- **KPI Summary Strip:**
  - `Monitored Products`: 55 Lines.
  - `Products Below PCA`: 52 lines currently operating below expected NHS volume.
  - `Products Meeting PCA`: 3 lines achieving or exceeding 100% PCA target.
  - `Average MTD Achievement`: 42.8%.
- **Operational Table (Grouped Headers):**
  - **Product Information:** `Catalog No`, `Part Description`, `Category`, `Current Stock`.
  - **DAILY:** `Daily PCA`, `Qty`, `Difference` ($\text{Daily PCA} - \text{Qty}$).
  - **MTD:** `15% PCA`, `MTD Qty`, `Difference` ($15\% \text{ PCA} - \text{MTD Qty}$).
  - **PCA ACHIEVEMENT:** `MTD %` ($\frac{\text{MTD Qty}}{15\% \text{ PCA}}$).
- **Visual Shortfall Badges:**
  - Negative difference = Shortfall (Red badge `badge-danger`).
  - Positive difference = Target achieved or exceeded (Green badge `badge-success`).
- **Filters:** Category filter (`Parallel Import`, `Generic to PI`, `Fridge Lines`), Achievement level filter (`Shortfall`, `Meeting`), and Catalog Search.

---

### 4.8 Section 9: Overstock Inventory Surveillance
- **Source Sheet:** `Overstock`
- **Business Purpose:** Eliminating working capital stagnation and minimizing inventory expiry risk.
- **Summary Cards:**
  - `Overstock Products`: 8 lines requiring commercial clearance.
  - `Total Stock Units`: 14,019 physical packs.
  - `Total Stock Value`: £112,368.42 tied-up working capital.
  - `Highest Days Stock`: 421 Days (`5119C` - Onbrez Inhaler 300mcg).
- **Top Overstock Bar Chart:** Horizontal bar chart visualizing top overstocked products by total stock value.
- **Inventory Clearance Table:**
  - Columns: `Code`, `Description`, `Category`, `Stock Units`, `True Cost`, `Stock Value`, `No. of Days Stock`.
  - Default sort: `No. of Days Stock` descending.
  - Extreme overstock (>200 days) highlighted with urgent red warning badges.

---

## 5. Technical Implementation & Delivery Files

| File Name | Location | Description |
| :--- | :--- | :--- |
| `pi_data.json` | Workspace root | Consolidated, validated JSON dataset extracted from all 8 Excel sheets. |
| `pi_purchase.html` | Workspace root | Self-contained, responsive standalone dashboard application with embedded dataset and Chart.js visuals. |
| `index.html` | Workspace root | Master BNS Sales Intelligence Platform integrating the module into the main sidebar navigation. |
| `Functional_Specification_PI_Purchase_vs_Profit.md` | Workspace root | Formal technical specification document. |

---

## 6. Verification & Quality Assurance Checklist

- [x] All 8 workbook sheets integrated without placeholder or synthetic figures.
- [x] All 6 desktop KPI cards fit in a single row with period comparisons and up/down indicators.
- [x] Monthly Purchase vs Profit combo chart supports toggles for Overall, Old, and New lines.
- [x] Buyer-grouped management table contains all 4 buyers (Louise, Manisha, Luca, Raffaella) with subtotals and Grand Total.
- [x] Sourcing matrix maps all 22 European nations with dynamic sorting and subtotal rows.
- [x] Strategic volume analysis accurately models Top 5 concentration risk.
- [x] 7 clickable status cards dynamically filter the 75-record New License master table.
- [x] 15% PCA operational table incorporates grouped headers and automated shortfall color indicators.
- [x] Overstock surveillance highlights extreme days stock (>200d) and renders top value bar chart.
- [x] Multi-format report export (CSV, Print/PDF) fully functional.
