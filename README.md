# Project: User Behavior Analysis & A/A/B Testing for Food Startup

## Business Context
This project focuses on the Analytics Department of a food products startup. The primary challenge was to investigate the sales funnel to identify where users drop off and to evaluate the impact of a UI font redesign on conversion rates through rigorous statistical testing.

## 🔍 Research Objectives
The analysis addresses critical business and technical questions:

* **Funnel Optimization:** At what stage of the purchase process do we lose the most users?
* **User Retention:** What percentage of users complete the entire journey from the first event to successful payment?
* **A/A/B Testing:** Does a global font change in the application affect user behavior or conversion?
* **Statistical Rigor:** How to maintain the integrity of results when performing multiple simultaneous hypothesis tests?

## 📊 Datasets Overview
The project analyzes event logs with the following structure:
* **EventName:** User action (MainScreenAppear, OffersScreenAppear, CartScreenAppear, PaymentScreenSuccessful, Tutorial).
* **DeviceIDHash:** Unique user identifier.
* **EventTimestamp:** Unix timestamp of the event.
* **ExpId:** Experiment group ID (246 and 247 for Control, 248 for Test).

## 🛠️ Analytical Roadmap

### 1. Data Engineering & Quality Assurance
* **ETL Process:** Converted timestamps to datetime objects and standardized column names to `snake_case`.
* **Data Integrity:** Performed a critical check to identify and **exclude users present in multiple experiment groups**, ensuring zero contamination.
* **Timeframe Optimization:** Identified and filtered out incomplete historical data, focusing on the period where logs were fully recorded (Aug 1st - Aug 7th, 2019).

### 2. Funnel Analysis (Customer Journey)
* **Sequence Identification:** Mapped the logical purchase flow: Main Screen → Offers → Cart → Payment.
* **Conversion Velocity:** Calculated the conversion rate for each individual stage and the cumulative retention from start to finish.
* **Drop-off Diagnosis:** Identified the "Initial Friction" point where the highest percentage of users leave the app.

### 3. A/A/B Testing & Statistical Rigor
* **Automated Z-Tests:** Developed a reusable Python function to compare proportions between groups for every event in the funnel.
* **A/A Validation:** Compared the two control groups (246 vs 247) to ensure the splitting mechanism was functioning correctly.
* **Bonferroni Correction:** Implemented a significance level adjustment ($\alpha_{adj} = \alpha / n$) to control the Family-Wise Error Rate across 16 simultaneous hypothesis tests.

## 🚀 Business Impact & Recommendations
The analysis provided a data-backed roadmap for the design and product teams:

* **Safe UI Implementation:** Confirmed that the font change had no statistically significant impact on conversion. The design team can proceed with the update for branding purposes without risking revenue.
* **Strategic Focus:** Recommended shifting development resources from "look and feel" tweaks to the **Main Screen**, where a **38% user drop-off** was detected.
* **Methodological Framework:** Established a robust testing pipeline that can be reused for future product experiments, ensuring that decisions are driven by data rather than intuition.
