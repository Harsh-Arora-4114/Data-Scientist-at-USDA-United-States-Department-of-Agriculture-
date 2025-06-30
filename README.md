## Data Scientist at USDA (United States Department of Agriculture)

**USDA Production Insights** is a SQL-driven data analysis project built to support agricultural decision-making. It processes multi-year, multi-commodity datasets to track U.S. production trends across states. This tool helps generate insights for internal reports, meetings, and strategic agricultural initiatives.

---

### Features

* **State-by-State Analysis**: Generates production summaries for each U.S. state.
* **Multi-Year Trend Tracking**: Identifies year-over-year changes in output.
* **Commodity-Wise Insights**: Includes milk, cheese, coffee, honey, and yogurt.
* **Missing Data Handling**: Ignores disclosure-suppressed values like `(D)` and `(NA)`.
* **Autograder-Compatible Outputs**: All values are numeric with only decimals (no commas).

---

### Datasets Used

* `milk_production`
* `cheese_production`
* `coffee_production`
* `honey_production`
* `yogurt_production`
* `state_lookup` (for joining state names and ANSI codes)

---

### Setup

Import all CSVs into your SQL database of choice (e.g., MySQL, PostgreSQL, SQLite).

```bash
# Example for PostgreSQL
CREATE TABLE state_lookup (...);
COPY state_lookup FROM 'state_lookup.csv' CSV HEADER;

CREATE TABLE cheese_production (...);
COPY cheese_production FROM 'cheese_production.csv' CSV HEADER;
-- Repeat for other datasets
```

---

### Usage

Open your SQL editor and run the queries to:

* Analyze total cheese production by state in 2023.
* Check if Delaware produced any cheese in 2023.
* Track how coffee production changed over the years.
* Identify states producing over 100 million units of a commodity.

---

### Example Queries

**State-Level Cheese Production (2023):**

```sql
SELECT 
  sl.State,
  SUM(CAST(REPLACE(cp.Value, ',', '') AS FLOAT)) AS total_cheese_production_2023
FROM 
  state_lookup sl
LEFT JOIN 
  cheese_production cp
  ON sl.State_ANSI = cp.State_ANSI
WHERE 
  cp.Year = 2023 AND cp.Value NOT LIKE '(%'
GROUP BY 
  sl.State;
```

**Trend in Coffee Production:**

```sql
SELECT 
  Year,
  SUM(CAST(REPLACE(Value, ',', '') AS FLOAT)) AS total_coffee_output
FROM 
  coffee_production
WHERE 
  Value NOT LIKE '(%'
GROUP BY Year
ORDER BY Year;
```

---

### Output Format

All output values must be numeric. Examples:

```text
123456.00
98423.52
```

❌ No commas
✅ Only numbers and periods

---

### Disclaimer

This project is for internal analytical use within the USDA. All data and queries are used for official planning, forecasting, and operational analysis. Unauthorized use or distribution is prohibited.

---

### License

This project is internal USDA work and follows federal data usage policies.

---

### Author

Developed by **Harsh Arora**

