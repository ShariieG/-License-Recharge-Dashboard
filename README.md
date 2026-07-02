# -License-Recharge-Dashboard
A Power BI dashboard built for **Bayobab** (a sub-entity under MTN Group MANCO) that automates the quarterly recharge of Microsoft 365 and related software licensing costs back to individual departments. The dashboard turns raw Entra ID licensing data into a departmental cost allocation model, giving finance and IT stakeholders a clear, auditable view of who is using what — and what it costs.

<img width="2400" height="1280" alt="quarter-summary-mockup" src="https://github.com/user-attachments/assets/c6cc108c-df91-494a-986b-57542aabd02d" />


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

<img width="2400" height="1280" alt="quarter-summary-mockup" src="https://github.com/user-attachments/assets/75496c58-1404-4b80-8ddb-caee04420414" />


### 2. Recharge Schedule
The finance-ready billing table — every software product with active license count, USD unit price, USD/ZAR totals, and % of total cost — alongside a grouped view of spend by category (Productivity & Collaboration, Specialized/Data & Development, Security/Infrastructure & Creative).

<img width="2400" height="1320" alt="recharge-schedule-mockup" src="https://github.com/user-attachments/assets/94693eb2-e489-440f-bc2e-59088f496c1e" />


### 3. SKU Reference Chart — Department Cost Breakdown by SKU
A stacked bar chart showing exactly which SKUs make up each department's recharge total, used for detailed audit trails and resolving billing queries at the department/SKU level.

<img width="2400" height="1240" alt="sku-breakdown-mockup" src="https://github.com/user-attachments/assets/cdb64344-6f7b-4f70-a2e9-c5242ac726fb" />


## Data Model

The model is built around a central `Bayobab` table (license assignments at the employee level) joined to supporting dimension and reference tables:


<img width="355" height="1142" alt="data-model" src="https://github.com/user-attachments/assets/f8b3d2ed-0cc1-45df-bcd7-45bccba7b0e1" />


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
### Key DAX Formulas

**License Cost (ZAR)** — maps raw license names to standardized product names, looks up the unit cost, converts USD → ZAR, and sums across all rows:

```dax
License Cost (ZAR) = 
VAR _ExchangeRate = 18
RETURN
    SUMX(
        Bayobob,
        VAR _RawProduct = Bayobob[Total Licenses]
        VAR _MappedProduct =
            SWITCH(
                TRUE(),
                _RawProduct = "GitHub", "GitHub User",
                _RawProduct = "Microsoft 365 E5", "Microsoft 365 E5s",
                _RawProduct = "Microsoft 365 E5 Nopstnconf", "Microsoft 365 E5s",
                _RawProduct = "Office 365 E1", "Microsoft Office 365 E1",
                _RawProduct = "Powerapps Per User", "PowerApps Per User",
                _RawProduct = "Project Online Essentials", "Microsoft Project Essentials",
                _RawProduct = "Project Online Premium", "Microsoft Project Premium",
                _RawProduct = "Project Online Professional", "Microsoft Project Professional",
                _RawProduct
            )
        VAR _UnitCost =
            LOOKUPVALUE(
                'Software Licensing Costs'[Unit Cost],
                'Software Licensing Costs'[Software Product], _MappedProduct
            )
        RETURN
            _UnitCost * 3 * _ExchangeRate
    )
```

**Product Summary Table** — a calculated table built with `UNION`/`ROW` that normalizes raw license names into standardized software product names and counts active licenses per product, used as the base for the Recharge Schedule and SKU breakdown visuals:

```dax
Product Summary Table = UNION(
    ROW(
        "Software Product", "Adobe CC", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Adobe CC")) + 0
    ),
    ROW(
        "Software Product", "Adobe Pro", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Adobe Pro")) + 0
    ),
    ROW(
        "Software Product", "Enterprise Mobility + Security E3", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Enterprise Mobility + Security E3")) + 0
    ),
    ROW(
        "Software Product", "GitHub User", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "GitHub")) + 0
    ),
    ROW(
        "Software Product", "Microsoft 365 Copilot", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Microsoft 365 Copilot")) + 0
    ),
    ROW(
        "Software Product", "Microsoft 365 E5s", 
        "Active Count", COUNTROWS(FILTER('Total Licenses','Total Licenses'[Total Licenses] = "Microsoft 365 E5 Nopstnconf" || 'Total Licenses'[Total Licenses] = "Microsoft 365 E5")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Defender Threat Intelligence", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Microsoft Defender Threat Intelligence")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Visio", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Microsoft Visio")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Workplace Analytics", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Microsoft Workplace Analytics")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Office 365 E1", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Office 365 E1")) + 0
    ),
    ROW(
        "Software Product", "Power Automate Per User", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Power Automate Per User")) + 0
    ),
    ROW(
        "Software Product", "PowerApps Per User", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Powerapps Per User")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Project Essentials", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Project Online Essentials")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Project Premium", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Project Online Premium")) + 0
    ),
    ROW(
        "Software Product", "Microsoft Project Professional", 
        "Active Count", COUNTROWS(FILTER('Total Licenses', 'Total Licenses'[Total Licenses] = "Project Online Professional")) + 0
    )
)
```
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
