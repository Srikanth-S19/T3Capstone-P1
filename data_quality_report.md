### 1. Dataset Inspection Summary

- **`customers`**: Contains 2,400 customers with 9 columns. Key identity column is `customer_id`.

- **`orders`**: Contains 10,009 historical order line-items with 10 variables tracking amounts, dates, ratings, and return statuses.

- **`support_tickets`**: Tracks 1,921 complaints/issues detailing metrics like resolution time, channel type, and negative/positive sentiment.

- **`web_events_snapshot`**: Holds a 30-day lookback summary of user engagement across 2,400 unique accounts up to the modeling cutoff date.

- **`churn_labels`**: Matches the 2,400 user IDs with their respective data split (`train`, `validation`, `test`) and target flag.

- **`intervention_history`**: Tracks standard campaign interaction metrics for all 2,400 primary accounts.

- **`rfm_modeling_snapshot`**: A comprehensive pre-compiled analytic feature table with 29 variables mapping customer traits, behaviors, and labels into a singular data matrix.

### 2. Data-Quality Report

- **a. Missing Values:**
  
  - `customers`: `loyalty_tier` is missing $57.75\%$ of its data (1,386 instances), which represents standard non-loyalty members. `skin_type` has $16.71\%$ missing values (401 counts).
  
  - `orders`: `rating` is missing in 80 records ($0.8\%$), which represents customers who did not leave a product review.

- **b. Duplicate Records:** No pure duplicate row-entries exist. Key identifiers (`customer_id`, `order_id`, `ticket_id`) display complete uniqueness within their respective reference tables.

- **c & d. Invalid Values & Outliers:**
  
  - `orders.gross_amount`: Extreme high-end skew is observed. The 75th percentile rests comfortably at $707.43$, but the maximum value spikes to an anomalous $24,789.38$. This requires log-scaling or robust capping before feeding into parametric algorithms.
  
  - `orders.delivery_days`: Ranges uniformly between 1 and 11 days, showing no negative or invalid numbers.
  
  - `support_tickets.resolution_hours`: The maximum duration reaches up to $74.6$ hours, significantly above the median of $24.2$ hours.

- **e. Join/Key Issues:** Referential integrity is perfectly intact. $100\%$ of customer records present across transactional and interaction tables map perfectly back to the core `customers` directory table.

- **f. Date Consistency Issues:** All historical transactions and tickets occurred *after* their respective profile sign-up dates. No negative tenure values were found.

- **g. Columns causing Data Leakage (Critical Find):**
  
  The snapshot modeling target window starts on **2025-09-30** to observe churn over the next 60 days. Out of 10,009 total orders inside `orders.csv`, **1,872 orders occur after 2025-09-30** (extending up to 2025-11-29).
  
  - *Warning:* Any features generated from the `orders` table without explicitly filtering out dates $> \text{2025-09-30}$ will leak the future outcome directly into training variables, leading to over-optimistic model performance that fails in deployment.
