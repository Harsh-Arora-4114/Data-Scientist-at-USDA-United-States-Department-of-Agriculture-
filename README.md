## USDA Production Insights

**USDA Production Insights** is a structured SQL-based data science project developed to analyze U.S. agricultural commodity production. It evaluates multi-year, multi-state trends across five key commodities. The project is designed to support strategic decision-making using real-world datasets provided through a Coursera capstone.

---

### Features

* **State-by-State Production Summary**: Compare output across U.S. states.
* **Cross-Year Trend Detection**: Identify growth or decline in commodity volumes.
* **Multi-Commodity Analysis**: Covers cheese, milk, coffee, yogurt, and honey.
* **Missing Data Handling**: Filters out entries such as `(D)` and `(NA)`.
* **Numeric-Only Output**: Clean formatting for autograder compatibility (no commas).

---

### Datasets Used

* `milk_production`
* `cheese_production`
* `coffee_production`
* `honey_production`
* `yogurt_production`
* `state_lookup`

Each dataset contains state-level production figures, reported by year (and month, where applicable).

---

### Installation

1. Clone or download the project files.
2. Import each `.csv` into a relational database system (PostgreSQL, MySQL, SQLite, etc.).

```bash
# PostgreSQL import example
CREATE TABLE state_lookup (...);
COPY state_lookup FROM 'state_lookup.csv' CSV HEADER;
```

3. Repeat for each commodity dataset.

---

### Usage

Run SQL queries to:

* Summarize total cheese production in 2023 for each state.
* Find whether Delaware produced cheese in 2023.
* Track how coffee production changed across years.
* Identify states exceeding 100 million units in annual production.

---

### Example Queries

**Total Cheese Production by State (2023)**

```sql
SELECT 
  sl.State,
  SUM(CAST(REPLACE(cp.Value, ',', '') AS FLOAT)) AS total_cheese_production
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

**Coffee Production Trend**

```sql
SELECT 
  Year,
  SUM(CAST(REPLACE(Value, ',', '') AS FLOAT)) AS total_coffee_output
FROM 
  coffee_production
WHERE 
  Value NOT LIKE '(%'
GROUP BY 
  Year
ORDER BY 
  Year;
```

---

### Output Format

All numeric output must be **decimal numbers only** (e.g., `123456.78`).
❌ No commas
✅ Only digits and periods

---

### Disclaimer

This project is part of a **Coursera** Data Science specialization and is intended for **educational purposes only**. The datasets, structure, and evaluation guidelines are provided by Coursera for learning SQL, data analysis, and real-world data wrangling techniques.

Use of this project should comply with Coursera’s academic integrity policies.

---

### License

The data and project material are provided by **Coursera** and are intended for educational use under their platform terms. This project does **not claim ownership of the datasets** and is shared in accordance with Coursera’s educational license and use policy.

---

### Author

Developed by **Harsh Arora**
