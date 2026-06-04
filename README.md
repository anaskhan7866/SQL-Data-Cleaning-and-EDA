# World Layoffs SQL Project: Data Cleaning & Exploratory Data Analysis (EDA)

## 📌 Project Overview
This project is a comprehensive, two-part SQL study focused on cleaning and analyzing a global dataset of tech industry layoffs. Utilizing MySQL, the project first meticulously cleans raw data to ensure accuracy and consistency, followed by an in-depth Exploratory Data Analysis (EDA) to uncover patterns, trends, and key insights regarding global workforce reductions.

The raw dataset used for this project is sourced from Kaggle: [Layoffs Dataset](https://www.kaggle.com/datasets/swaptr/layoffs-2022).

---

## 📂 Project Structure
*   **`Data_Cleaning.sql`**: Contains the SQL script used to stage, deduplicate, standardize, and trim the raw data.
*   **`EDA_Queries.sql`**: Contains the SQL queries used to uncover trends, rankings, and rolling totals.
*   **`layoffs.csv`**: The primary, raw data file referenced and imported into the database for processing.

---

## 🛠️ Phase 1: Data Cleaning
The primary objective of this phase was to transform a messy, raw dataset into a reliable format ready for analysis without altering the initial raw data.

### Key Steps Taken:
1.  **Staging Data:** Created a staging table (`layoffs_staging`) to preserve the integrity of the original `layoffs.csv` data.
2.  **Deduplication:** Used `ROW_NUMBER()` window functions partitioned across all core columns to identify and delete duplicate entries securely.
3.  **Data Standardization:**
    *   Unified industry variants (e.g., standardizing `Crypto Currency` and `CryptoCurrency` into `Crypto`).
    *   Fixed trailing punctuation bugs (e.g., trimming trailing periods from `United States.`).
    *   Populated missing `industry` data by performing self-joins on matching company profiles (e.g., fixing blank values for Airbnb).
4.  **Date Formatting:** Converted the text-based date column into a proper SQL `DATE` format using `STR_TO_DATE()` and altered the column schema.
5.  **Null Value & Garbage Row Removal:** Safely dropped records where both `total_laid_off` and `percentage_laid_off` were completely null, as they provided no analytical value.

---

## 📊 Phase 2: Exploratory Data Analysis (EDA)
With a clean dataset, the analysis moved toward answering high-impact questions about how, where, and when these layoffs occurred.

### Key Insights Uncovered:
*   **Company Fatalities:** Identified companies that laid off 100% of their staff (mostly startups), filtering them by total funds raised to find massive failures (e.g., Quibi, BritishVolt).
*   **Top 10 Layoffs:** Grouped and ranked metrics to find the absolute highest layoffs by individual **Companies**, **Locations (Cities)**, **Countries**, **Industries**, and **Funding Stages**.
*   **Yearly Metrics:** Uncovered chronological progression showing the macroeconomic impact across individual years.
*   **Advanced Analytics & Window Functions:**
    *   **Top 3 Companies Per Year:** Utilized Common Table Expressions (CTEs) paired with `DENSE_RANK()` to isolate the top 3 companies responsible for the heaviest layoffs within each distinct calendar year.
    *   **Rolling Totals:** Created a month-over-month rolling total of global layoffs using continuous aggregates to visualize the speed and acceleration of workforce reductions over time.

---

## 🚀 How to Run This Project
1.  **Setup Database:** Open your MySQL Workbench or preferred SQL client and create a schema named `world_layoffs`.
2.  **Import Raw Data:** Import the `layoffs.csv` file into a table named `layoffs`.
3.  **Run Scripts:** 
    *   Execute the `Data_Cleaning.sql` script first to generate the final, fully optimized `layoffs_staging2` table.
    *   Execute `EDA_Queries.sql` on the cleaned table to generate the analytical reports.

---

## 💻 Tech Stack
*   **Database Engine:** MySQL
*   **Concepts Applied:** Advanced Joins, Window Functions (`ROW_NUMBER()`, `DENSE_RANK()`), CTEs (Common Table Expressions), Data Modification (`ALTER`, `UPDATE`, `DELETE`), String Manipulation (`TRIM`).
