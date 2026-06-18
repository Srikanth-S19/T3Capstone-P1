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
  
  - *Warning:* Any features generated from the `orders` table without explicitly filtering out dates $> \text{2025-09-30}$ will leak the future outcome directly into your training variables, leading to over-optimistic model performance that fails in deployment.

### 3. Exploratory Analysis Highlights

- **a. Customer Profile & Demographics:**
  
  - **Geography:** Highly represented by Tier 1 ($41.88\%$) and Tier 2 ($36.25\%$) cities; Tier 3 accounts for $21.88\%$.
  
  - **Age Profile:** Skewed heavily toward young-to-mid adults, with ages 25-34 comprising $43.54\%$ of the user base.
  
  - **Acquisition Channel:** Social and search driven: `Instagram` ($21.54\%$), `Google Search` ($19.42\%$), and third-party `Marketplace` platforms ($19.00\%$) dominate signups.
  
  - **Loyalty status:** Standard users without tiers make up $57.75\%$, followed by Silver ($24.58\%$), Gold ($13.29\%$), and Platinum ($4.38\%$).
  
  - **Preference & Skin:** `Skin Care` ($30.46\%$) and `Hair Care` ($21.13\%$) are preferred. Skin types are evenly split among Oily, Dry, Sensitive, Combination, and Normal (roughly $16\%$ each).
  
  - **Marketing Consent:** Highly positive, with $73.33\%$ opting in.

- **b & c. Order & Monetary Behaviour:**
  
  - Average single-order gross cost sits at $743.90$, while the median sits lower at $597.06$, showcasing a heavy right tail.
  
  - Discounts applied to items average $27.41\%$.
  
  - Product demand volume is driven directly by `Skin Care` ($26.98\%$) and `Hair Care` ($21.89\%$).

- **d & e. Support Tickets & Product Returns:**
  
  - The primary operational bottlenecks are logistics and accounting: `late_delivery` ($19.63\%$) and `refund_delay` ($17.96\%$) make up the bulk of support cases.
  
  - *Severe Friction Point:* Both `product_reaction` and `refund_delay` require double the resolution time ($\sim 36.5$ hours vs. the normal baseline of $\sim 20$ hours), driving sentiment scores down to highly negative territory ($\sim -0.60$ and $-0.65$ respectively) and leading to high ticket re-opening rates ($>22\%$).
  
  - Product return rates hover consistently around $5\%$ to $8\%$, with `Makeup` seeing the highest return risk ($8.16\%$) and `Wellness` the lowest ($5.02\%$).

- **f. Web/App Activity (Past 30 Days):**
  
  - Active users average $5.46$ sessions and look at $23.02$ items per month.
  
  - Cart addition averages $1.56$ items, but abandonment rates sit at $0.67$ occurrences per user, signaling a drop-off friction point in checkout flows.

- **g. Campaign / Interventions:**
  
  - Marketing communication is distributed uniformly across `new_launch`, `bundle_discount`, `free_shipping`, and `welcome_offer` (roughly $19-21\%$ each), leaving a clean $21.13\%$ baseline control group who received `none`.
  
  - Costs remain steady across all communication types, averaging between $17.27$ and $19.52$ monetary units.

- **h. Target Churn Distribution:**
  
  - The business faces a significant churn risk: **$46.96\%$ of active customers churned** (failed to make an order) within the 60-day window following 2025-09-30.
  
  - The modeling datasets are divided proportionally and reflect balanced churn frequencies across all analytical segments:
    
    - **Train Set:** 916 Non-Churners / 812 Churners
    
    - **Validation Set:** 189 Non-Churners / 147 Churners
    
    - **Test Set:** 168 Non-Churners / 168 Churners (Exactly balanced 50/50 split)
