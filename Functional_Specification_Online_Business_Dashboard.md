# Functional Specification: Online Business Dashboard
**Document Version:** 1.0  
**Project:** BNS Sales Intelligence Platform  
**Module:** Online Business & Multi-Channel Attribution  

---

## Document Control & Approvals

| Role | Name & Designation | Signature | Date |
| :--- | :--- | :--- | :--- |
| **Author** | **Amit Porwal**<br>IT - Business Analyst | ______________________________ | ____________ |
| **Reviewer** | **Mayur Patel**<br>Specials / Sales Manager | ______________________________ | ____________ |
| **Reviewer** | **Amit Sanandiya**<br>IT – Project Manager | ______________________________ | ____________ |
| **Approver** | **Shiva Kottam**<br>QA Officer / RP | ______________________________ | ____________ |

---

## 1. Introduction

The **Online Business Dashboard** is an enterprise analytical and operational module developed for **BNS Distribution** as an integral component of the **BNS Sales Intelligence Platform**. The primary objective of this dashboard is to provide real-time channel attribution, multi-source order tracking, daily performance comparison against monthly benchmarks, volume/box throughput evaluation, and profitability analytics across all ordering channels and Pharmacy Management System (PMR) integrations.

The dashboard consolidates ordering data originating from direct electronic data interchange (EDI) connections, specialized pharmacy management systems (PMRs), B2B e-commerce web portals, third-party procurement platforms, and manual telesales desks. It empowers Directors, Sales Managers, Regional Sales Managers (RSMs), and Team Leads to make data-driven decisions by monitoring daily channel variances, month-to-date (MTD) revenue contribution, product category breakdowns, and customer ordering trends across all digital and manual order capture points.

---

## 2. Scope

### In-Scope
The scope of the Online Business module includes the design, data pipeline integration, calculation engines, and interactive user interface components for the following functionalities:

1. **Multi-Channel & Order Source Attribution:** Tracking performance across ten (10) distinct ordering sources:
   - **Avibuyer** (Online pharmacy buying group & procurement platform)
   - **Cambrian** (PMR / Ordering EDI integration)
   - **Cascade** (PMR automated dispensary ordering)
   - **DC** (Distribution Centre Direct Connect / EDI Data Centre feeds)
   - **Dataplast** (PMR integration stream)
   - **PharmAssist** (PMR dispensary system)
   - **Rest PMRs** (Aggregated long-tail PMR systems)
   - **Telesales** (Direct telephone / manual order desk)
   - **Victoria** (PMR integration)
   - **Website** (BNS Online B2B web ordering portal)
2. **Daily Performance Tracking (Yesterday vs. Current Month Daily Average):**
   - Active ordering customer account count per channel.
   - Yesterday's daily sales vs. current month daily average sales benchmark.
   - Yesterday's daily profit vs. current month daily average profit benchmark.
   - Yesterday's gross margin % vs. current month daily average gross margin %.
   - Automated variance calculation with dynamic directional trend arrows (`▲` / `▼`) and visual color coding (Green for positive variance, Red for negative variance).
3. **Current Month Source Performance Detail:**
   - Month-to-date (MTD) aggregated sales revenue (£).
   - MTD total box count / units fulfilled.
   - MTD total gross profit (£).
   - Sales share percentage (%) across channels.
   - Aggregate summary TOTAL row with weighted margin calculations.
4. **Visual Analytics & Distribution:**
   - Interactive bar chart displaying Sales Share % by Order Source with channel-specific color schemes.
   - Visual trend comparison between digital channels and manual telesales.
5. **Multi-Dimensional Filter Engine:**
   - Temporal / Date Range filter (Current Month, Today - Live, Yesterday, Current Week, Previous Week, Previous Month, Quarter, Financial Year, Custom Range).
   - Product Category filter (All Categories, Generic, PI, Ethical, OTC, CD, Perfumes).
   - Order Source / Channel filter.
   - Team Leader & Sales Executive filters.
6. **Granular Drill-Down Views (Extended Tables):**
   - Source-to-Customer Account drill-down (Account No, Name, Type, Volume, Sales, Profit, Margin %).
   - Source-to-Product Category breakdown.
7. **Data Export & Reporting:**
   - One-click CSV/Excel export for downstream operational analysis.

### Out of Scope
- Direct order cart checkout engine or transaction processing within the BI reporting interface (orders are ingested post-processing from EDI/PMR/Web gateways).
- Internal database schema modifications of external third-party PMR software systems.
- Unapproved alterations to the standardized ERP 1020 Sales Report upload structure.

---

## 3. Abbreviations

| Abbreviation | Description |
| :--- | :--- |
| **PMR** | Pharmacy Management System (e.g., Dataplast, Cambrian, Cascade, Avibuyer, PharmAssist, Victoria) |
| **DC** | Distribution Centre / Direct Connect EDI Feed |
| **EDI** | Electronic Data Interchange |
| **KPI** | Key Performance Indicator |
| **MTD** | Month to Date |
| **GM / Margin %** | Gross Margin Percentage: `(Profit / Sales) * 100` |
| **RSM** | Regional Sales Manager |
| **TL** | Team Leader (Telesales & Online Channels) |
| **DT** | Drug Tariff Products |
| **NDT** | Non-Drug Tariff Products |
| **CD** | Controlled Drugs |
| **PI** | Parallel Import Products |
| **OTC** | Over-The-Counter Products |
| **NIC** | Net Ingredient Cost |
| **PNA** | Packing and Administration Charges |
| **WHF** | Wholesaler Handling Fee |
| **BNS** | B&S Group Distribution |
| **FS** | Functional Specification |
| **URS** | User Requirement Specification |
| **DS** | Design Specification |

---

## 4. User Roles & Access Permissions

The system enforces role-based access control (RBAC). User privileges and module visibility are managed dynamically from the administrative backend:

| User Role | Dashboard Permissions & Scope of Access |
| :--- | :--- |
| **Manager / Director** | Full access to all modules, financial KPIs, profit numbers, margins, all 10 order sources, and configuration masters. Ability to export full data. |
| **Regional Sales Manager (RSM)** | Access to Online Business dashboard filtered by customer accounts mapped to their assigned sales region/territory. |
| **Team Leader (TL - Telesales)** | Access to team-level channel performance, Telesales vs. Online distribution, and order volume metrics. |
| **Sales Executive / Special Buddy** | View-only access restricted to customer accounts assigned directly to their portfolio. |

---

## 5. Dashboard Layout, Filters & KPI Matrix

### 5.1 Dashboard Filters
Users can dynamically slice and dice data across the entire Online Business module using the top filter bar:

1. **Date Range (`filterDate_page_sources`):**
   - *Current Month* (Default)
   - *Today - Live* (Real-time stream)
   - *Yesterday*
   - *Current Week*
   - *Previous Week*
   - *Previous Month*
   - *Quarter*
   - *Financial Year*
   - *Custom Range* (From Date / To Date picker)
2. **Product Category (`filterCategory_page_sources`):**
   - *All Categories* (Default)
   - *Generic*
   - *PI (Parallel Import)*
   - *Ethical*
   - *OTC (Over-The-Counter)*
   - *CD (Controlled Drugs)*
   - *Perfumes*
3. **Order Source (`filterClass_page_sources`):**
   - *All Sources* (Default)
   - *Avibuyer*
   - *Cambrian*
   - *Cascade*
   - *DC*
   - *Dataplast*
   - *PharmAssist*
   - *Rest PMRs*
   - *Telesales*
   - *Victoria*
   - *Website*
4. **Team Leader & Executive Filters (`filterTeam_page_sources`, `filterExec_page_sources`):**
   - *All Team Leaders* (Amit, Sanket, Jaishali, Ayaz, Kam, Prashant)
   - *All Executives* (Filtered dynamically based on selected Team Leader)

### 5.2 Summary KPI Metrics Matrix (`sourcesKPIs`)
The dashboard displays executive-level summary cards at the top of the page:

1. **Total Online & Channel Sales (£):** Total gross revenue generated across all selected order sources.
2. **Total Boxes / Units Fulfilled:** Total quantity of physical packs/boxes dispatched.
3. **Total Gross Profit (£):** Cumulative profit earned across all channel orders.
4. **Overall Gross Margin (%):** Weighted average margin: `(Total Profit / Total Sales) * 100`.
5. **Total Active Accounts:** Count of unique customer dispensary accounts placing at least one order in the selected period.
6. **Digital vs. Manual Share (%):** Percentage of orders placed via digital/PMR/Web channels versus manual Telesales phone orders.

### 5.3 Visual Analytics & Charts (`sourceRevChart`)
1. **Sales Share % by Source (Bar Chart):**
   - Visual bar chart displaying the proportional revenue contribution of each order source.
   - Dynamic bar colors mapped to channels:
     - DC: `#1a56db` (Primary Blue)
     - Telesales: `#10b981` (Emerald Green)
     - Cambrian: `#f59e0b` (Amber)
     - Dataplast: `#ef4444` (Coral Red)
     - Victoria: `#8b5cf6` (Purple)
     - Website: `#06b6d4` (Cyan)
     - PharmAssist: `#f97316` (Orange)
     - Avibuyer: `#ec4899` (Pink)
     - Cascade: `#3b82f6` (Light Blue)
     - Rest PMRs: `#14b8a6` (Teal)

---

## 6. Functional Requirements

### 6.1 Online Business Overview & KPI Cards

| 6.1 | Online Business Overview & KPI Summary |
| :--- | :--- |
| **Priority** | High |
| **Purpose** | Displays consolidated top-level business health indicators for all order sources and channels for the selected time period. |
| **Role** | Manager, RSM, Team Leader |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Total Channel Sales** | KPI Card | Displays the sum of all sales revenue across all active channels.<br>**Logic:** `SUM(Source_Sales)`<br>**Format:** `£X,XXX,XXX.XX` |
| **Total Box Volume** | KPI Card | Displays the total number of boxes/units sold across all channels.<br>**Logic:** `SUM(Source_Boxes)`<br>**Format:** Integer with thousand separators (e.g. `153,255`) |
| **Total Gross Profit** | KPI Card | Displays cumulative profit generated across all channels.<br>**Logic:** `SUM(Source_Profit)`<br>**Format:** `£XXX,XXX.XX` |
| **Average Margin %** | KPI Card | Displays the overall gross margin percentage.<br>**Logic:** `(Total Profit / Total Sales) * 100`<br>**Format:** Percentage with 1 decimal place (e.g. `18.5%`) |
| **Active Accounts Count** | KPI Card | Displays the count of distinct dispensary accounts ordering through any channel.<br>**Logic:** `COUNT(DISTINCT Account_No)` |
| **Digital Adoption Rate** | KPI Card | Percentage of orders received via electronic/PMR/Web channels compared to total.<br>**Logic:** `(Non-Telesales Sales / Total Sales) * 100` |

---

### 6.2 Sales Share by Source (Visual Analytics)

| 6.2 | Sales Share by Source Chart |
| :--- | :--- |
| **Priority** | High |
| **Purpose** | Provides an immediate graphical representation of channel revenue distribution to identify leading ordering streams and shifts in customer ordering behavior. |
| **Role** | Manager, RSM, Team Leader |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Source Name** | X-Axis Label | Displays the name of the channel / PMR (e.g., Avibuyer, Cambrian, Cascade, DC, Dataplast, PharmAssist, Rest PMRs, Telesales, Victoria, Website). |
| **Sales Share %** | Y-Axis Value | Displays the calculated revenue share percentage.<br>**Logic:** `ROUND((Individual_Source_Sales / Total_Sales) * 100, 0)` |
| **Interactive Tooltip** | Hover Box | Displays exact Sales (£), Total Boxes, Profit (£), and Margin (%) upon mouse hover. |

---

### 6.3 Daily Source Performance (Yesterday vs. Current Month Daily Average)

| 6.3 | Daily Source Performance Table |
| :--- | :--- |
| **Priority** | High |
| **Purpose** | Compares yesterday’s real-time performance against the current month's daily average benchmark for each order channel. This enables managers to detect sudden drop-offs, PMR communication outages, or spikes in daily channel sales. |
| **Role** | Manager, RSM, Team Leader |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Source** | Column | Displays the ordering channel / PMR system name. |
| **Account Count** | Column | Displays the number of unique customer accounts that placed an order through this source yesterday.<br>**Logic:** `COUNT(DISTINCT Account_No WHERE Order_Date = Yesterday)`<br>**Calculation Benchmark:** Modeled as `ROUND(Total_Orders / 60)` in baseline calculations. |
| **Sales** | Column (Composite) | **Primary Value:** Yesterday's total sales revenue (`£XX,XXX.XX`).<br>**Secondary Sub-text:** Variance comparison vs. Current Month Daily Average: `▲/▼ vs avg £XX,XXX.XX`.<br>**Formulas:**<br>- `Daily_Avg_Sales = Total_Current_Month_Sales / Working_Days (25)`<br>- `Yesterday_Sales = Actual Yesterday Ingested Sales`<br>- `Variance = Yesterday_Sales - Daily_Avg_Sales`<br>**Visual Rule:** If `Yesterday_Sales >= Daily_Avg_Sales`, display green text with up arrow (`▲`), else display red text with down arrow (`▼`). |
| **Profit** | Column (Composite) | **Primary Value:** Yesterday's gross profit (`£XX,XXX.XX`).<br>**Secondary Sub-text:** Variance comparison vs. Current Month Daily Average: `▲/▼ vs avg £XX,XXX.XX`.<br>**Formulas:**<br>- `Daily_Avg_Profit = Total_Current_Month_Profit / Working_Days (25)`<br>- `Yesterday_Profit = Actual Yesterday Ingested Profit`<br>- `Variance = Yesterday_Profit - Daily_Avg_Profit`<br>**Visual Rule:** If `Yesterday_Profit >= Daily_Avg_Profit`, display green text with up arrow (`▲`), else display red text with down arrow (`▼`). |
| **Margin** | Column (Composite) | **Primary Value:** Yesterday's gross margin percentage (`XX.X%`).<br>**Secondary Sub-text:** Variance vs. Current Month Average Margin: `▲/▼ vs avg XX.X%`.<br>**Formulas:**<br>- `Yesterday_Margin_% = (Yesterday_Profit / Yesterday_Sales) * 100`<br>- `Avg_Margin_% = (Daily_Avg_Profit / Daily_Avg_Sales) * 100`<br>- `Variance_% = Yesterday_Margin_% - Avg_Margin_%`<br>**Visual Rule:** If `Yesterday_Margin_% >= Avg_Margin_%`, display green indicator (`▲`), else display red indicator (`▼`). |
| **TOTAL Row** | Summary Row | Displays aggregate metrics across all 10 sources:<br>- **Total Accounts:** `SUM(Account_Count)`<br>- **Total Yesterday Sales:** `SUM(Yesterday_Sales)` with total variance vs. `SUM(Daily_Avg_Sales)`<br>- **Total Yesterday Profit:** `SUM(Yesterday_Profit)` with total variance vs. `SUM(Daily_Avg_Profit)`<br>- **Total Weighted Margin:** `(Total_Yesterday_Profit / Total_Yesterday_Sales) * 100` with variance vs. monthly average. |

---

### 6.4 Current Month Source Performance Detail

| 6.4 | Current Month Source Performance Detail Table |
| :--- | :--- |
| **Priority** | High |
| **Purpose** | Displays comprehensive month-to-date (MTD) cumulative operational and financial figures for every channel, including box throughput, gross profit, and revenue market share. |
| **Role** | Manager, RSM, Team Leader |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Source** | Column | Displays the ordering source name (Avibuyer, Cambrian, Cascade, DC, Dataplast, PharmAssist, Rest PMRs, Telesales, Victoria, Website). |
| **Sales** | Column | Displays the total MTD sales revenue generated by the source.<br>**Source Data:** Ingested from ERP Sales Line Table (Column: `LINE_SALE`).<br>**Format:** `£X,XXX,XXX.XX` |
| **Boxes** | Column | Displays the total count of product boxes / packs ordered through this source in the current month.<br>**Source Data:** Ingested from ERP Quantity Field (Column: `ORDER_QTY`).<br>**Format:** Number formatted with commas (e.g., `74,328`). |
| **Profit** | Column | Displays the total MTD gross profit achieved through this source.<br>**Logic:** `Sales Revenue - Cost of Goods Sold (COGS)`<br>**Format:** `£XX,XXX.XX` |
| **Share %** | Column | Displays the channel's contribution percentage to overall sales revenue.<br>**Logic:** `(Source_Sales / Combined_Total_Sales) * 100`<br>**Format:** Integer percentage (e.g., `42%`). |
| **TOTAL Row** | Summary Row | Displays system-wide totals across all sources:<br>- `Total Sales = SUM(Sales)`<br>- `Total Boxes = SUM(Boxes)`<br>- `Total Profit = SUM(Profit)`<br>- `Total Share % = 100%` |

---

### 6.5 Extended Table: Source-wise Customer Account Breakdown

| 6.5 | Extended Customer Account Breakdown |
| :--- | :--- |
| **Priority** | High |
| **Purpose** | Accessible by clicking on any specific **Source Name** or **Account Count** cell. Displays the list of all customer accounts utilizing that specific channel, allowing sales managers to evaluate customer-level digital channel adoption. |
| **Role** | Manager, RSM, Team Leader, Sales Executive |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Account No** | Column | Displays the BNS dispensary customer account number (e.g. `ACC-10492`). |
| **Account Name** | Column | Displays the registered legal name of the pharmacy / dispensary. |
| **Account Type** | Column | Identifies whether the account is an **Independent Pharmacy** or part of a **Group Account**. |
| **Post Code** | Column | Displays the postal code of the pharmacy location. |
| **Assigned RSM** | Column | Displays the name of the Regional Sales Manager overseeing the account. |
| **Assigned Team Leader** | Column | Displays the Telesales Team Leader mapped to the account. |
| **Source / PMR Version** | Column | Displays the exact PMR system or software version used by the customer. |
| **MTD Orders Count** | Column | Number of distinct order transactions placed through this source in the month. |
| **MTD Boxes** | Column | Total quantity of boxes ordered by the account via this source. |
| **MTD Sales (£)** | Column | Total sales value generated by the account through this source. |
| **MTD Profit (£)** | Column | Total gross profit generated by the account through this source. |
| **Gross Margin %** | Column | Gross profit margin percentage: `(MTD Profit / MTD Sales) * 100`. |
| **Last Order Date** | Column | Date and time stamp of the most recent order submitted via this channel. |

---

### 6.6 Extended Table: Source-wise Product Category Performance

| 6.6 | Extended Product Category Performance Table |
| :--- | :--- |
| **Priority** | Medium |
| **Purpose** | Evaluates product mix and purchasing preferences per channel (e.g., whether PMRs predominantly drive Generic/Ethical volume vs. Web driving OTC/Perfumes). |
| **Role** | Manager, RSM |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Category** | Column | Product category name (Generic, PI, Ethical, OTC, CD, Perfumes). |
| **Source Name** | Column | Ordering channel name. |
| **Units / Boxes Sold** | Column | Quantity of packs sold in this category via the channel. |
| **Category Sales (£)** | Column | Gross sales revenue for the category through this channel. |
| **Category Profit (£)** | Column | Gross profit for the category through this channel. |
| **Category Margin %** | Column | Profit margin achieved: `(Category Profit / Category Sales) * 100`. |
| **Category Share %** | Column | Proportion of channel revenue contributed by this category. |

---

### 6.7 Digital Channel vs. Telesales Comparison

| 6.7 | Digital Channel vs. Telesales Comparison View |
| :--- | :--- |
| **Priority** | Medium |
| **Purpose** | Compares automated digital ordering streams (Avibuyer, Cambrian, Cascade, DC, Dataplast, PharmAssist, Rest PMRs, Victoria, Website) against manual telephone desk (Telesales) orders to track digital transformation KPIs. |
| **Role** | Manager, Director |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Channel Group** | Column | Group classification: `Digital / Automated Channels` vs. `Manual Telesales Desk`. |
| **Total Revenue (£)** | Column | Consolidated sales revenue for the group. |
| **Total Boxes** | Column | Consolidated box count fulfilled. |
| **Total Profit (£)** | Column | Consolidated gross profit. |
| **Average Order Value (£)** | Column | Average value per order: `Total Revenue / Total Orders`. |
| **Profit Margin %** | Column | Weighted margin percentage for the channel group. |
| **Cost per Order Estimate** | Column | Operational cost metric associated with channel order processing. |

---

### 6.8 Data Export & Reporting Functionality

| 6.8 | Data Export & Reporting |
| :--- | :--- |
| **Priority** | Medium |
| **Purpose** | Enables authorized users to export filtered dataset snapshots for offline analysis, executive reviews, and finance reconciliation. |
| **Role** | Manager, RSM |

| Name | Type | Description |
| :--- | :--- | :--- |
| **Export Button** | Action Button | Triggers direct download of the currently active table view. |
| **Export Format** | Dropdown / Modal | Options for `.CSV` and `.XLSX` (Excel format). |
| **Export Payload** | Dataset | Exports all filtered rows with complete numerical precision (unrounded currency and quantity values), timestamp of export, and applied filter criteria. |

---

## 7. Masters & System Integrations

### 7.1 Order Source Master & Channel Configuration
The system shall maintain a centralized **Order Source Master** to configure and map incoming order streams:

| Field Name | Data Type | Description & Validation Rules |
| :--- | :--- | :--- |
| **Source_ID** | Integer (PK) | Unique internal identification number for the source channel. |
| **Source_Code** | VARCHAR(20) | Unique system code (e.g. `SRC_DC`, `SRC_CAMBRIAN`, `SRC_WEB`, `SRC_TELE`). |
| **Source_Name** | VARCHAR(50) | Display name (Avibuyer, Cambrian, Cascade, DC, Dataplast, PharmAssist, Rest PMRs, Telesales, Victoria, Website). |
| **Channel_Type** | Enum | Classification: `PMR_EDI`, `DIRECT_EDI`, `WEB_PORTAL`, `MANUAL_DESK`, `BUYING_GROUP`. |
| **Integration_Protocol**| VARCHAR(30) | Communication protocol (e.g. `AS2`, `FTP/SFTP`, `REST_API`, `DATABASE_LINK`). |
| **Status** | Boolean | `Active` or `Inactive`. Inactive sources are hidden from the primary dashboard. |
| **Color_Code** | VARCHAR(10) | Hex color code assigned for chart visualizations. |

### 7.2 Working Days & Operational Calendar Master
To accurately compute daily benchmarks and variances, the system maintains a calendar master:
- **Default Working Days per Month:** 25 working days (configurable per calendar month).
- **Working Day Formula:** `Total Working Days = Total Calendar Days - (Sundays + Bank Holidays)`.
- **Benchmark Calculation:**
  $$\text{Daily Benchmark Sales} = \frac{\text{Current Month MTD Sales}}{\text{Configured Working Days}}$$
  $$\text{Daily Benchmark Profit} = \frac{\text{Current Month MTD Profit}}{\text{Configured Working Days}}$$

### 7.3 Data Pipeline & Ingestion Architecture
1. **Primary ERP Sales Report (Report 1020):** Daily automated feed providing line-level transaction records including `ACCOUNT_NO`, `LINE_SALE`, `LINE_PROFIT`, `ORDER_QTY`, `SOURCE_ID`, and `PRODUCT_CATEGORY`.
2. **EDI & PMR Ingestion Gateway:** Automated message queue capturing incoming orders from Cambrian, Dataplast, Victoria, Cascade, PharmAssist, and DC.
3. **Web Ordering Database:** Synchronized live order stream capturing B2B portal orders.
4. **Data Sync Frequency:**
   - Real-time/Intraday sync for *Today - Live* view (every 15 minutes).
   - Nightly batch aggregation at 00:30 AM for finalized *Yesterday* and *MTD* tables.

---

## 8. Non-Functional Specifications

### 8.1 Availability & Reliability
- **System Uptime:** The dashboard shall ensure 99.9% uptime (24x7x365), excluding planned maintenance windows.
- **Data Latency:** MTD and Daily Source tables shall load within $\le 1.5$ seconds upon filter selection.
- **Real-Time Stream:** The *Today - Live* filter feed shall reflect new orders within 15 minutes of ERP posting.

### 8.2 Capacity Limits & Concurrency
- **Concurrent Users:** System shall support at least 250 concurrent active users without performance degradation.
- **Single Session Control:** The application shall prevent simultaneous logins using the same user credentials on multiple devices.

### 8.3 Usability & Interface Standards
- **Responsive Layout:** The dashboard interface shall be fully responsive across desktop monitors (1920x1080, 1366x768), laptops, and tablets.
- **Data Formatting:** All currency values shall be formatted to the British Pound (`£X,XXX.XX`) with two decimal places. Box quantities shall be formatted with standard comma thousand separators.
- **Visual Usability:** Directional variance indicators (`▲` / `▼`) shall be clearly contrasted with `#10b981` (Green) and `#ef4444` (Red) to ensure rapid executive readability.
- **Accessibility:** Color palettes shall meet WCAG 2.1 AA accessibility standards for color contrast.

---
*End of Functional Specification Document*
