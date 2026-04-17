# 📊 Sales Performance Dashboard

## 📌 Overview

This project was built to track sales performance and goal achievement by seller, using Power BI and DAX.

The dashboard integrates multiple data sources and provides a reliable view of:

* Total sales volume (MWh)
* Monthly targets
* Achievement percentage
* Seller ranking

---

## 🚧 Problem

The main challenge was combining two different datasets:

* Sales data (`btx_deal_negocios`)
* Monthly targets (`meta_fronts`)

Issues included:

* Inconsistent seller names across tables
* Missing targets for some months
* Risk of duplicated values due to incorrect relationships

---

## ⚙️ Solution

### Data Modeling

* Created a **calendar table** to standardize time analysis
* Built relationships using **seller + month/year**
* Applied a **star schema approach** to avoid ambiguity

### Key DAX Measures

```DAX
Volume Total = SUM(btx_deal_negocios[volume_mwh])

Meta Mensal = SUM(meta_fronts[meta])

Atingimento (%) = DIVIDE([Volume Total], [Meta Mensal], 0)
```

### Ranking Logic

Used `RANKX` with virtual tables (`ADDCOLUMNS`) to dynamically rank sellers based on performance.

---

## ⚠️ Edge Cases Handled

* Division by zero when no target exists
* Sellers with inconsistent naming (handled in Power Query)
* Months with no sales (handled via calendar table)
* Multiple records per seller (aggregation control)

---

## ❌ What Could Go Wrong

* Incorrect relationships → duplicated values
* Missing calendar table → broken time analysis
* Poor DAX context handling → wrong KPIs
* No data validation → unreliable dashboard

---

## ✅ Results

* Fully automated reporting
* Eliminated manual Excel tracking
* Improved decision-making with reliable KPIs
