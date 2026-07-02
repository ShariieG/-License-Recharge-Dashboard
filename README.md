# -License-Recharge-Dashboard
A Power BI dashboard built for **Bayobab** (a sub-entity under MTN Group MANCO) that automates the quarterly recharge of Microsoft 365 and related software licensing costs back to individual departments. The dashboard turns raw Entra ID licensing data into a departmental cost allocation model, giving finance and IT stakeholders a clear, auditable view of who is using what — and what it costs.

![Uploading quarter-summary-mockup_1.svg…]()
<svg viewBox="0 0 1200 640" xmlns="http://www.w3.org/2000/svg" font-family="Segoe UI, Arial, sans-serif">
  <rect width="1200" height="640" fill="#141414"/>
  <!-- Header -->
  <rect x="0" y="0" width="1200" height="60" fill="#FFCC00"/>
  <ellipse cx="55" cy="30" rx="30" ry="16" fill="none" stroke="#141414" stroke-width="3"/>
  <text x="55" y="35" font-size="11" font-weight="bold" fill="#141414" text-anchor="middle">MTN</text>
  <text x="110" y="38" font-size="24" font-weight="bold" fill="#141414">BAYOBAB M365 LICENSE RECHARGE (SAMPLE DATA)</text>
  <text x="1180" y="24" font-size="13" font-weight="bold" fill="#141414" text-anchor="end">Q1 2026 - Recharge Period</text>
  <rect x="1040" y="34" width="140" height="20" fill="#3a3a3a"/>
  <text x="1180" y="49" font-size="12" fill="#FFCC00" text-anchor="end">ZAR/ USD 18.00</text>

  <!-- KPI section -->
  <text x="40" y="95" font-size="16" font-weight="bold" fill="#FFCC00">QUARTER SUMMARY</text>
  <g font-size="13" fill="#cccccc">
    <rect x="40" y="105" width="260" height="90" fill="#2b2b2b"/>
    <rect x="40" y="105" width="260" height="6" fill="#FFCC00"/>
    <text x="55" y="130">TOTAL LICENSED USERS</text>
    <text x="55" y="170" font-size="30" font-weight="bold" fill="#ffffff">128</text>

    <rect x="310" y="105" width="260" height="90" fill="#2b2b2b"/>
    <rect x="310" y="105" width="260" height="6" fill="#FFCC00"/>
    <text x="325" y="130">TOTAL Q1 RECHARGE (ZAR)</text>
    <text x="325" y="170" font-size="30" font-weight="bold" fill="#ffffff">R199,999K</text>

    <rect x="580" y="105" width="260" height="90" fill="#2b2b2b"/>
    <rect x="580" y="105" width="260" height="6" fill="#FFCC00"/>
    <text x="595" y="130">E5 LICENSE COUNT</text>
    <text x="595" y="170" font-size="30" font-weight="bold" fill="#ffffff">120</text>

    <rect x="850" y="105" width="310" height="90" fill="#2b2b2b"/>
    <rect x="850" y="105" width="310" height="6" fill="#FFCC00"/>
    <text x="865" y="130">LINE ITEMS BILLED</text>
    <text x="865" y="170" font-size="30" font-weight="bold" fill="#ffffff">14</text>
  </g>

  <!-- Shape of the spend -->
  <text x="40" y="240" font-size="16" font-weight="bold" fill="#FFCC00">SHAPE OF THE SPEND (SAMPLE)</text>

  <!-- Donut chart -->
  <g>
    <rect x="40" y="255" width="560" height="360" fill="#2b2b2b"/>
    <text x="60" y="285" font-size="15" fill="#ffffff" font-weight="bold">TOTAL COST BY SOFTWARE PRODUCT</text>
    <circle cx="230" cy="450" r="110" fill="none" stroke="#FFCC00" stroke-width="45" stroke-dasharray="220 471" stroke-dashoffset="0"/>
    <circle cx="230" cy="450" r="110" fill="none" stroke="#8CC63F" stroke-width="45" stroke-dasharray="140 471" stroke-dashoffset="-220"/>
    <circle cx="230" cy="450" r="110" fill="none" stroke="#F7941D" stroke-width="45" stroke-dasharray="60 471" stroke-dashoffset="-360"/>
    <circle cx="230" cy="450" r="110" fill="none" stroke="#EF4136" stroke-width="45" stroke-dasharray="30 471" stroke-dashoffset="-420"/>
    <circle cx="230" cy="450" r="110" fill="none" stroke="#F2E9A0" stroke-width="45" stroke-dasharray="21 471" stroke-dashoffset="-450"/>
    <g font-size="12" fill="#cccccc">
      <rect x="400" y="300" width="10" height="10" fill="#FFCC00"/><text x="416" y="309">Microsoft 365 E5s</text>
      <rect x="400" y="322" width="10" height="10" fill="#8CC63F"/><text x="416" y="331">Microsoft 365 Copilot</text>
      <rect x="400" y="344" width="10" height="10" fill="#F7941D"/><text x="416" y="353">Microsoft Visio</text>
      <rect x="400" y="366" width="10" height="10" fill="#EF4136"/><text x="416" y="375">Microsoft Office 365 E1</text>
      <rect x="400" y="388" width="10" height="10" fill="#F2E9A0"/><text x="416" y="397">Other Products</text>
    </g>
  </g>

  <!-- Bar chart -->
  <g>
    <rect x="615" y="255" width="545" height="360" fill="#2b2b2b"/>
    <text x="635" y="285" font-size="15" fill="#ffffff" font-weight="bold">LICENSE COST BY DEPARTMENT</text>
    <g font-size="12" fill="#cccccc">
      <text x="800" y="315" text-anchor="end">Sample Dept A</text>
      <rect x="810" y="303" width="210" height="16" fill="#FFCC00"/>
      <text x="1030" y="315">R99,900</text>

      <text x="800" y="345" text-anchor="end">Sample Dept B</text>
      <rect x="810" y="333" width="150" height="16" fill="#FFCC00"/>
      <text x="970" y="345">R59,400</text>

      <text x="800" y="375" text-anchor="end">Sample Dept C</text>
      <rect x="810" y="363" width="110" height="16" fill="#FFCC00"/>
      <text x="930" y="375">R38,200</text>

      <text x="800" y="405" text-anchor="end">Sample Dept D</text>
      <rect x="810" y="393" width="80" height="16" fill="#FFCC00"/>
      <text x="900" y="405">R24,500</text>

      <text x="800" y="435" text-anchor="end">Sample Dept E</text>
      <rect x="810" y="423" width="50" height="16" fill="#FFCC00"/>
      <text x="870" y="435">R14,100</text>

      <text x="800" y="465" text-anchor="end">Sample Dept F</text>
      <rect x="810" y="453" width="30" height="16" fill="#FFCC00"/>
      <text x="850" y="465">R8,700</text>
    </g>
  </g>
  <text x="600" y="630" font-size="11" fill="#777777" text-anchor="middle">Illustrative sample data only — not actual figures</text>
</svg>


> **Note:** Screenshots below are mockups built with illustrative sample data for public sharing — actual figures and department names are not disclosed.

## Overview

Each quarter, Bayobab needs to recharge Microsoft 365 (and related) software license costs to the departments that actually use them. This dashboard consolidates license assignment data, product unit pricing, and department mapping into a single Power BI model that produces:

- A live, self-service view of **total spend by software product**
- **Departmental cost allocation** across ~20+ Bayobab and FibreCo entities
- A full **recharge schedule** ready for finance sign-off
- A **SKU-level breakdown per department** for audit and query resolution

## Key Metrics (Q1 2026 Recharge Period)

The Quarter Summary page surfaces top-line KPIs at a glance, including total licensed users, total quarterly recharge value, E5 license count, and line items billed, with a configurable ZAR/USD conversion rate. *(Specific figures omitted here — see the live dashboard for current values.)*

## Dashboard Pages

### 1. Quarter Summary — Shape of the Spend
High-level KPIs plus two views of the same spend: total cost by software product (donut) and license cost by department (bar), so stakeholders can see both *what* is being paid for and *who* is paying for it.

![Quarter Summary (sample data)](./screenshots/quarter-summary-mockup.svg)

### 2. Recharge Schedule
The finance-ready billing table — every software product with active license count, USD unit price, USD/ZAR totals, and % of total cost — alongside a grouped view of spend by category (Productivity & Collaboration, Specialized/Data & Development, Security/Infrastructure & Creative).

![Recharge Schedule (sample data)](./screenshots/recharge-schedule-mockup.svg)

### 3. SKU Reference Chart — Department Cost Breakdown by SKU
A stacked bar chart showing exactly which SKUs make up each department's recharge total, used for detailed audit trails and resolving billing queries at the department/SKU level.

![SKU Breakdown (sample data)](./screenshots/sku-breakdown-mockup.svg)

## Data Model

The model is built around a central `Bayobab` table (license assignments at the employee level) joined to supporting dimension and reference tables:

![Data Model](./screenshots/data-model.png)

**Tables:**
- **Bayobab** — core fact table: Employee Id, Email Address, Department, Department Group, Person Type, License Cost (ZAR), Total Licenses, plus key measures (Department Total Cost, Total Licensed Users, E5 License Count)
- **Employee_Department_Table** — Employee Id → Department mapping
- **Product Summary Table** — Software Product, Product_Group, Active Count, Unit Price (USD), Total ZAR/USD, % of Total Cost, Line Items Billed
- **Software Licensing Costs** — Software Product → Unit Cost reference table
- **Total Licenses** — supporting license count table

### Modeling Notes
- Distinguishes between **assigned licenses** and **license group membership** to avoid double-counting users across bundled SKUs
- Uses **Department Group** logic to roll individual Bayobab entities (FibreCo Zambia, Nigeria, Uganda, Ghana, CIV, CAR, South Africa, etc.) up into consolidated reporting groups
- DAX measures handle cost allocation per department, per SKU, and category-level rollups (Productivity & Collaboration / Specialized, Data & Development / Security, Infrastructure & Creative)

## Tech Stack

- **Power BI** — data model, DAX measures, primary reporting dashboard
- **Entra ID** — source of license assignment data
- **Power Query** — data transformation and department mapping
- An HTML/Chart.js version of this dashboard was also built as a lightweight, shareable single-page alternative, styled in MTN's yellow-and-black brand palette

## Roadmap

- [ ] Azure Function to automate quarterly data refresh from Entra ID
- [ ] Blob Storage integration for point-in-time snapshots
- [ ] Row-level security so department heads only see their own recharge data
- [ ] Historical trend view across recharge periods

## Author

**Sharon Galela** — Junior Software Developer, Providence Software Solutions (Pty) Ltd
GitHub: [@ShariieG](https://github.com/ShariieG)
