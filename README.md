# RCPA Reporting & Doctor Performance Analysis (Power BI)
## 🔍 Overview

This project demonstrates a complete **ETL and Visualization pipeline** using **Power Query and Power BI**. It focuses on analyzing prescription data gathered from a **Retail Chemist Prescription Audit (RCPA)** to evaluate brand performance, doctor conversion rates, and competitor analysis.

## 🗃️ Datasets Used

1. **RCPA Reporting Form**  
2. **Product Master**  
3. **Brand Targets**  
4. **Expected Transformation Sheet**

Each dataset plays a critical role in transforming raw prescription data into actionable insights.

## ⚙️ ETL Process (Power Query)

The following steps were implemented in **Power Query (within Power BI)**:

### 1. RCPA Data Table
- Imported and cleaned the RCPA Reporting Form.
- Unpivoted brand columns into a normalized structure.
- Merged with Product Master to enrich brand metadata.
- Filtered to include only in-house brands.

### 2. Competitor RCPA Data Table
- Reused the same source but filtered for competitor brands only.
- Ensured format aligned with the Expected Transformation sheet.

## 📈 Visualizations (Power BI)

Three primary visuals were developed:

1. **📊 Doctor Rx Performance**
   - Tracks prescription quantity vs targets per brand, per Med Rep, per region.
   - Data merged with Brand Targets.

2. **📈 Doctor Conversion Status**
   - Evaluates if a doctor meets/exceeds target Rx quantities for **3 or more consecutive RCPAs**.
   - Binary flag indicating conversion status per doctor.

3. **📉 Brand Competition per Region**
   - Compares total prescriptions of our product vs competitors.
   - Visualized by region to reveal market penetration.

## 🧾 Key Definitions

| Term | Description |
|------|-------------|
| **Rx** | Prescription |
| **Doctor Conversion** | A doctor who prescribes the target quantity in 3 or more consecutive audits |
| **Brand Competition** | Market share comparison between our brand and competitors |
| **RCPA** | Retail Chemist Prescription Audit |

## 💡 Tools & Technologies

- **Power BI Desktop**
- **Power Query (M Language)**
- **Excel (as source files)**

## 📂 Repository Structure

```
|-- 📁 datasets/
|     |-- RCPA_Reporting_Form.xlsx
|     |-- Product_Master.xlsx
|     |-- Brand_Targets.xlsx
|     |-- Expected_Transformation.xlsx
|
|-- 📁 powerbi/
|     |-- RCPA_Report.pbix
|
|-- README.md
```

## ✅ How to Run

1. Open `RCPA_Report.pbix` using Power BI Desktop.
2. Refresh all queries to reload data and transformations.
3. Navigate through the Report pages to explore visualizations.

