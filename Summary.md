
# **Task 6 – Sales Trend Analysis (MySQL)**

## **Objective**

---

## **Dataset Used**

* **Table:** `sales` (from Superstore Sales data)
* **Relevant Columns:**

  * `Order ID` – unique identifier for each order
  * `Order Date` – date when the order was placed
  * `Sales` – revenue amount for the order line

---

## **Steps Performed**

### **1. Extract Month**

**Purpose:** Retrieve the numeric month (1–12) from `Order Date`.
**Function Used:**

```sql
EXTRACT(MONTH FROM STR_TO_DATE(`Order Date`, '%m/%d/%Y'))
```

---

### **2. Extract Year & Month and Group**

**Purpose:** Separate year and month to avoid mixing months from different years.
**Function Used:**

```sql
EXTRACT(YEAR FROM STR_TO_DATE(`Order Date`, '%m/%d/%Y'))
```

**Why:** Enables proper grouping for monthly analysis.

---

### **3. Calculate Monthly Revenue**

**Purpose:** Find the total revenue for each month.
**Function Used:**

```sql
SUM(Sales)
```

**Why:** Shows overall revenue trends.

---

### **4. Count Unique Orders**

**Purpose:** Measure order volume per month.
**Function Used:**

```sql
COUNT(DISTINCT `Order ID`)
```

**Why:** Indicates customer order activity beyond just revenue.

---

### **5. Sort Results Chronologically**

**Purpose:** Arrange output in order from earliest to latest.
**Function Used:**

```sql
ORDER BY order_year, order_month
```

---

### **6. Filter for Specific Time Period**

**Purpose:** Limit analysis to a specific date range.
**Function Used:**

```sql
WHERE STR_TO_DATE(`Order Date`, '%m/%d/%Y') BETWEEN '2014-01-01' AND '2014-12-31'
```

**Why:** Focuses on one year or desired time window.
**Optional:**

```sql
LIMIT 12
```

to restrict number of rows.

---

## **Final Combined Query**

```sql
SELECT 
    EXTRACT(YEAR FROM STR_TO_DATE(`Order Date`, '%m/%d/%Y')) AS order_year,
    EXTRACT(MONTH FROM STR_TO_DATE(`Order Date`, '%m/%d/%Y')) AS order_month,
    SUM(Sales) AS monthly_revenue,
    COUNT(DISTINCT `Order ID`) AS order_volume
FROM sales
WHERE STR_TO_DATE(`Order Date`, '%m/%d/%Y') 
      BETWEEN '2014-01-01' AND '2014-12-31'
GROUP BY order_year, order_month
ORDER BY order_year, order_month
LIMIT 12;
```

---

## **Key Insights Expected**

* Monthly revenue trends and seasonality
* Order volume fluctuations
* Correlation between sales peaks and order counts
* Time periods of high or low performance

---

Do you want me to also **add a section with example output tables** so your GitHub README looks complete and visual? That would make it more professional.
