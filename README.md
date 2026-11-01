# PowerBI_Data_Modeling
# Power BI End-to-End Data Modeling Portfolio Project

## 📌 Project Overview
This project transforms a chaotic database architecture consisting of 23 unstructured tables into a high-performance **Star Schema (Galaxy Schema)**. By applying formal dimensional modeling guidelines, advanced Power Query extractions, and data warehouse engineering standards, this model guarantees data integrity, performance scalability, and corporate data security.

## 🛠️ Skills & Concepts Applied
* **Power Query backend engineering:** Query architecture isolation (`Staging`, `Dimensions`, `Facts`, `Support`).
* **Advanced Extractions:** Exploding comma-separated lists into rows, data cleansing, whitespace trimming, and text value standardization.
* **Dimensional Modeling Architecture:** Fact-Dimension separation, Junk Dimensions, Factless Facts, Accumulating Snapshots, Role-Playing Dimensions.
* **Analytical Foundation:** Explicit measure groups, automated calendar generation via DAX, and Row-Level Security (RLS).

## 📐 The Problem: "Nightmare Data Model"
The source framework featured critical architecture anti-patterns:
* Broken, cyclic many-to-many paths and bidirectional filters causing incorrect financial numbers.
* Mixed record granularity combining macro header attributes directly with granular detail dimensions.
* High volume of space-wasting technical strings (such as hash keys) degrading analytical evaluation speeds.

## 🚀 The Solution: Step-by-Step Implementation

### Phase 1: Infrastructure Isolation
Divided queries into functional workspace folders within Power Query:
1. `stage`: Main raw ingested data files.
2. `dimensions`: Core analytical master components.
3. `facts`: Low-level structural data transaction tables.
4. `support`: Meta configurations and security mapping.

### Phase 2: Dimensional Cleaning & Enrichment
* Built independent `dim_customer` and `dim_product` dimensions, scrubbing test keys and system entries.
* Unified mismatched tracking structures to resolve data grain fan-outs.
* Extracted structural status flags into a single consolidated junk dimension called `order_flags`.

### Phase 3: Advanced Fact Engineering
* **Fact Sales:** Built at the absolute lowest record detail layer to preserve numeric accuracy.
* **Fact Promotion Coverage (Factless Fact):** Configured a zero-metric map to evaluate marketing campaign reach across products without polluting core accounting stats.
* **Fact Order Process (Accumulating Snapshot):** Flattened independent phase tables into a unified row tracking cycle milestones: Order Date $\rightarrow$ Ship Date $\rightarrow$ Delivery Date $\rightarrow$ Invoice Date $\rightarrow$ Payment Date.

### Phase 4: Enterprise-Grade Polishing
* **Chronological Base:** Generated a shared date engine utilizing the `CALENDARAUTO()` function.
* **Unified Metrics:** Bound central KPI calculations (such as active client ratios, cycle duration averages, distinct orders) to an explicit `_Measures` table.
* **Row-Level Security (RLS):** Wired active security tables on top of dimensions with cross-filtering paths using dynamic identity criteria:
  ```dax
  [region] = LOOKUPVALUE(security[region], security[user_email], USERPRINCIPLENAME())
  ```

## 📊 Modeling 
### Before (The Chaos)

### After (Clean Star Schema Architecture)
<img width="1917" height="1017" alt="Screenshot 2026-11-01 135507" src="https://github.com/user-attachments/assets/a7c2d67a-819e-40f5-b960-bbe3cd36e9ef" />

### 📊 Visualization Dashboard And KPIS
<img width="1917" height="1017" alt="Screenshot 2026-11-01 135236" src="https://github.com/user-attachments/assets/91041d6a-ee5a-43a1-ad46-44ccaa3bfe66" />


## 💡 Engineering Insights
1. **Drop the Noise Early:** Removing useless high-cardinality values reduces file size instantly and improves reporting speeds.
2. **Details First:** Always anchor fact tables at the finest available transaction details; macro horizons can always be aggregated up cleanly through DAX.
