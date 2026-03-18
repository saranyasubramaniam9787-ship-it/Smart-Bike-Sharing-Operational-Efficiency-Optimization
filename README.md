# Smart City Bike Sharing: Operational Efficiency & Optimization
* 📊 Project Overview
This project delivers a comprehensive operational analysis of a multi-city smart bike-sharing network across Europe. The primary goal is to transform raw real-time inventory data into actionable intelligence that optimizes fleet distribution, enhances station efficiency, and ensures data integrity.
Key Business Objectives:
Operational Health Monitoring: Evaluate system performance by tracking bike availability, slot utilization, and station status (Open/Closed) across different geographies.
Data Integrity & Validation: Identify and quantify inventory mismatches where reported bike/slot counts do not align with physical capacity, pinpointing potential sensor errors or theft.
Demand Pattern Analysis: Uncover temporal trends (hourly/daily) and geographical hotspots to understand commuter behavior and peak usage windows.
Incentive Optimization: Assess the effectiveness of current reward categories (e.g., free ride minutes) in balancing supply and demand at "sink" and "source" stations.
Strategic Recommendations: Provide data-driven strategies for proactive bike redistribution, infrastructure planning for emerging markets, and maintenance prioritization to improve overall user satisfaction and system reliability.*

## 📖 Table of Contents
- [Project Overview](#-project-overview)
- [Data Source](#-data-source)
- [Tools & Technologies](#-tools--technologies)
- [Data Cleaning & Preparation](#-data-cleaning--preparation)
- [Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda)
- [Key Insights](#-key-insights)
- [Recommendations](#-recommendations)
- [How to Use](#-how-to-use)

---

## 📊 Project Overview
The objective of this project was to analyze real-time smart city bike-sharing data to evaluate system performance across different European cities. The primary business problems addressed include:
- Identifying high-performing vs. underperforming stations.
- Detecting inventory mismatches (data integrity issues).
- Analyzing geographical distribution and peak usage patterns.
- Optimizing bike redistribution and incentive programs to improve user satisfaction and operational consistency.

## 🗂️ Data Source
- **Source:** Real-time inventory data exported from a bike-sharing operator's database (provided as an Excel Workbook).
- **Scope:** Covers multiple European cities, with a heavy concentration in France (Lyon, Marseille, Toulouse), Spain, and Belgium.
- **Structure:**
  - **Fact Table (`Smart_Bike_Fact`):** Contains ~3,000+ records of real-time inventory including Station ID, Available Bikes, Available Slots, Timestamps (Date, Hour, Minutes), and Status.
  - **Dimension Tables:** `Station_Dim` (Location, Capacity, Contract) and `Bike_Dim` (Stand tracking).
- **Key Variables:** `Available_Bikes`, `Available_Bike_Slots`, `Bike_Stands`, `Reward_Category`, `Inventory_Record`, `Status`.

## 🛠️ Tools & Technologies
- **Visualization & Modeling:** Microsoft Power BI (DAX, Power Query)
- **Data Transformation:** Power Query (M Language)
- **Documentation:** Markdown (GitHub)
- **Data Source Format:** Excel (.xlsx)

## 🧹 Data Cleaning & Preparation
Extensive data cleansing was performed in **Power Query** to ensure accuracy before modeling:
1. **Standardization:**
   - Removed unreadable characters (Chinese/French artifacts) from `Station_Name` and `Address`.
   - Standardized `Status` (OPEN/CLOSED) and `Banking` (True/False → Descriptive labels).
   - Split `Position` column into distinct `Latitude` and `Longitude` for mapping.
2. **Handling Missing Values:**
   - Imputed missing addresses using city names based on geolocation coordinates.
   - Retained zero values for bikes/slots as they represent critical operational states (empty/full stations).
3. **Feature Engineering (Calculated Columns):**
   - **`Reward_Category`:** Created a dynamic incentive tier based on slot availability (e.g., "+15 Min Free Next Ride" if slots ≥ 30).
   - **`Inventory_Record`:** Validated data integrity by comparing `(Available Bikes + Available Slots)` against `Bike Stands` to flag "Mismatch," "Over Capacity," or "Correct" records.
4. **Data Modeling:** Established relationships between Fact and Dimension tables using `Station_ID`.

## 🔍 Exploratory Data Analysis (EDA)
Key questions explored during the analysis:
- **Geographical Distribution:** Which cities have the highest station density and bike availability?
- **Temporal Trends:** How does bike availability fluctuate during peak commuting hours (8–9 AM, 5–6 PM)?
- **Operational Health:** What is the rate of station closures and inventory mismatches?
- **Incentive Effectiveness:** How are reward categories distributed, and do they correlate with station efficiency?

> **Tip:** *In the actual GitHub repo, insert a screenshot of your Power BI Dashboard here showing the Map Visualization of Lyon/Marseille or the "Inventory Mismatch by Station" bar chart.*

## 💡 Key Insights
- **Market Dominance:** **Lyon** leads with 419 stations, followed by Marseille (129). France dominates the network with 4,226 available bikes, indicating a mature market compared to pilot-phase cities like Lund.
- **Peak Demand Patterns:** Bike availability dips significantly during morning (8–9 AM) and evening (5–6 PM) rush hours, confirming strong commuter-driven usage.
- **Data Integrity Issues:** Identified **3,060 inventory mismatches**, with 2,513 occurring in *Open* stations. Top problematic locations include "Cit Scolaire" and "Champvert," suggesting sensor errors or theft rather than closure issues.
- **Low Efficiency:** The average station efficiency is only **31.18%**, indicating stations are frequently either too full or too empty, failing to utilize mid-range capacity.
- **Incentive Skew:** 80.77% of stations are in Standard Zones. The most common reward is "+5 Min Free Ride," suggesting moderate imbalance but few stations reaching critical vacancy levels requiring high-value incentives.

## 🚀 Recommendations
- **Dynamic Redistribution:** Implement proactive bike redistribution just before peak hours (8 AM & 5 PM) to prevent stockouts in high-demand hubs like Lyon.
- **Audit High-Mismatch Stations:** Conduct immediate operational audits on stations like "Cit Scolaire" to fix sensor lag or hardware faults. Aim to reduce the closure rate below 5%.
- **Optimize Incentive Zones:** Analyze geographic clusters of "Incentive Zones" to identify chronic "sink" or "source" stations. Adjust reward thresholds dynamically to improve cost-efficiency.
- **Infrastructure Planning:** For smaller cities (<10 stations), conduct feasibility studies before expanding to ensure demand matches supply, avoiding over-provisioning seen in some French regions.

## ⚙️ How to Use
To explore this project or replicate the analysis:
1. **Prerequisites:**
   - Microsoft Power BI Desktop (latest version).
   - The source dataset: `Bike-Stations-Sharing-Data.xlsx`.
2. **Steps:**
   - Clone this repository.
   - Open the `.pbix` file in Power BI Desktop.
   - Update the data source path to your local copy of the Excel file if needed.
   - Refresh the data to reload the latest transformations and DAX calculations.
3. **Dependencies:** No external Python/R libraries are required; all transformations are handled natively within Power Query and DAX.


