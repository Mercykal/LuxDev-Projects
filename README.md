# RCPA Pharmaceutical Sales Analysis Project

## Project Overview

This project involves a comprehensive analysis of Retail Chemist Prescription Audit (RCPA) data to provide actionable insights into doctor prescription performance, brand competition, and doctor conversion rates. The primary goal was to perform a complete end-to-end Power BI project, starting from raw, complex data and ending with a clean, interactive, and insightful dashboard.

The project demonstrates key skills in:
*   **Data Transformation (ETL)** using Power Query
*   **Data Modeling** with a Star Schema in Power BI
*   **Advanced DAX** for creating complex calculated columns and measures
*   **Data Visualization** to build an interactive and user-friendly report

---

## Data Sources

The analysis is based on four primary data sets:
1.  **RCPA Reporting Form:** The main transactional data containing prescription records in a wide, unpivoted format.
2.  **Product Master:** A lookup table with detailed information about each product.
3.  **Brand Targets:** A table defining the monthly prescription targets for each brand.
4.  **Expected Transformation:** A guide document outlining the desired structure for the final clean data tables.

---

## ETL Process (Power Query)

The raw data was significantly complex and required extensive cleaning and transformation in Power Query to prepare it for analysis. Key steps included:

1.  **Data Unpivoting:** The main RCPA data was unpivoted to transform it from a wide format to a tall, normalized format, making it suitable for analysis.
2.  **Splitting and Parsing:** The unpivoted "Attribute" and "Value" columns were systematically split by delimiters (line feeds, commas, colons) to extract key information into separate, clean columns.
3.  **Conditional Column Creation:** Conditional logic was used to create unified `Doctor Name` and `Chemist` columns from multiple source columns. This was a critical step to handle the structure where data for three different pharmacies was present in every row.
4.  **Data Cleaning:** Applied a robust cleaning routine (**Trim, Clean, Uppercase**) to all key columns (`Product Name`, `Brand`, `Division`) to ensure data consistency and prevent relationship errors.
5.  **Table Separation:** The cleaned data was separated into two primary fact tables as required:
    *   `RCPA Data Table`: Containing only our company's product prescription data.
    *   `Competitor RCPA Data Table`: Containing only competitor product prescription data.
6.  **Aggregation:** The `BRAND TARGETS` table was grouped by brand to create a unique target value for each, preventing "many-to-many" relationship errors.

---

## Data Model

A robust **Star Schema** was implemented to ensure efficiency, accuracy, and ease of use for creating visuals.

*   **Fact Tables:** `RCPA Data Table`, `Competitor RCPA Data Table`
*   **Dimension Tables:** `Product Dimension`, `Brand Dimension`, `PRODUCT MASTER`, `BRAND TARGETS`, and a DAX-generated `Date Table`.

The model uses clean, one-to-many relationships, with filters flowing from the dimension tables to the fact tables. This design is optimal for performance and prevents ambiguity in calculations.

*(Optional: Insert an image of your data model here by uploading the screenshot to your GitHub repository and linking to it)*
<!-- ![Data Model Diagram](Data_Model.png) -->

---

## DAX Calculations

Several key DAX calculations were created to provide advanced insights:

#### 1. Base Measures
Simple `SUM` measures for basic aggregation.
```dax
Total Our Rx = SUM('RCPA Data Table'[Rx Qty/Week])
Total Competitor Rx = SUM('Competitor RCPA Data Table'[Rx Qty/Week])
Use code with caution.
Markdown
2. Doctor Specific Target (Measure)
An advanced measure using AVERAGEX and LOOKUPVALUE to calculate the correct target for each doctor based on the specific mix of products they prescribed. This solved the "flat line" issue in the main performance chart.
Generated dax
Doctor Specific Target =
AVERAGEX(
    'RCPA Data Table',
    LOOKUPVALUE(
        'BRAND TARGETS'[Target],
        'BRAND TARGETS'[Brand],
        'RCPA Data Table'[Product Name]
    )
)
Use code with caution.
Dax
3. Doctor Conversion Status (Calculated Column & Measure)
This was the most complex calculation.
A calculated column was first created to check, on a row-by-row basis, if an RCPA marked the 3rd consecutive time a doctor met their target.
A final measure ([Final Conversion Status]) was then built to find the most recent status for each doctor, providing a clean and accurate summary for the final visual.
Visualizations
The final report consists of three main visuals designed to answer the key business questions:
Doctor Rx Performance vs. Target: A line and clustered column chart showing each doctor's total prescriptions against their specific target, with slicers for Region and Brand. A secondary Y-axis was used to make the target line clearly visible.
Doctor Conversion Status: A table visual showing the final, most recent conversion status ("Converted" or "Not Converted") for each doctor.
Brand Competition by Region: A 100% stacked column chart that clearly visualizes the market share of our products versus the total competitor volume in each region.
Challenges & Key Learnings
Data Cleaning: The initial data structure was the biggest challenge. The combination of unpivoting, splitting by multiple delimiters, and using conditional logic based on the Attribute column was key to success.
DAX Context: Encountered and solved several classic DAX issues, including the "many-to-many" relationship error and the RELATED vs. LOOKUPVALUE context problem. This highlighted the importance of a clean data model.
Iterative Development: The project required a highly iterative approach—building a visual, diagnosing an issue (like the flat target line), and going back to the data model or DAX to refine the solution.
This project was an excellent exercise in end-to-end BI development and problem-solving.
