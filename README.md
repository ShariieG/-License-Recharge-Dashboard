# -License-Recharge-Dashboard
A Power BI dashboard built for **Bayobab** (a sub-entity under MTN Group MANCO) that automates the quarterly recharge of Microsoft 365 and related software licensing costs back to individual departments. The dashboard turns raw Entra ID licensing data into a departmental cost allocation model, giving finance and IT stakeholders a clear, auditable view of who is using what — and what it costs.

![Quarter Summary (sample data)](./screenshots/quarter-summary-mockup.svg)

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
