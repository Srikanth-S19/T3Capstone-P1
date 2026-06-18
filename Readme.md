# 

# Capstone Project: D2C Customer Churn Intelligence & Retention API

## Business Context

A D2C personal-care brand wants to reduce customer churn without blindly giving discounts to everyone. The product, marketing, and customer-support teams need a data-backed system that can:

1. understand customer behavior,
2. identify churn-risk patterns,
3. segment customers for targeted retention actions,
4. build a churn-prediction model, 
5. expose a simple API that can be used by an internal CRM tool.

You are given customer, order, support-ticket, web/app activity, campaign, and churn-label data. 

## Part 1 — Data Audit, EDA & Business Understanding

1. Load and inspect all raw datasets:
   
   1. customers,
   
   2. orders,
   
   3. support tickets,
   
   4. web/app events,
   
   5. churn labels,
   
   6. intervention/campaign history,
   
   7. any other file included in the data package.

2. Create a data-quality report covering:
   
   1. missing values,
   
   2. duplicate or duplicate-like records,
   
   3. invalid or unusual values,
   
   4. outliers,
   
   5. join/key issues,
   
   6. date consistency issues,
   
   7. columns that may cause leakage if used incorrectly.

3. Perform exploratory analysis on:
   
   1. customer demographics/profile fields,
   
   2. order behaviour,
   
   3. monetary behaviour,
   
   4. support-ticket issues,
   
   5. return/refund behaviour,
   
   6. web/app activity,
   
   7. campaign or intervention history,
   
   8. churn distribution.

4. Identify at least **five churn-risk hypotheses** from your analysis. Each hypothesis must be supported by a chart/table and a short explanation.

5. Write a short business memo explaining what the company should investigate before launching any retention campaign.

### Execution Pre-Requisites :

1. Install Python along with Jupyter Notebook / VS Code or other software to read & execute ".ipynb" files, or use cloud-based programs such as Google Colab

2. Install additional python modules given in "requirements.txt"

3. Create sub-folder structure as below :
   
            ├───data
            └───images

4. Copy the files listed in "Input Data Files" section to "data" folder

### Input Data Files (Under "data" folder)

| File Name                   | Rows   | Description                                                   |
| --------------------------- | ------ | ------------------------------------------------------------- |
| `customers.csv`             | 2,400  | Static customer profile and acquisition attributes            |
| `orders.csv`                | 10,009 | Full order-level transaction history (pre- and post-snapshot) |
| `support_tickets.csv`       | 1,921  | Customer-service interactions                                 |
| `web_events_snapshot.csv`   | 2,400  | 30-day web/app activity as of snapshot date                   |
| `churn_labels.csv`          | 2,400  | Target variable and train/val/test split assignment           |
| `rfm_modeling_snapshot.csv` | 2,400  | Pre-built, feature-engineered modeling table                  |
| `intervention_history.csv`  | 2,400  | Most recent campaign/intervention per customer                |

### Program Execution

```
Run Program "eda_audit.ipynb"
```

After running, the program will generate the files listed in sections "Output Data Files" and "Output Image Files" in the respective folders



### Output Data Files (Under "data" folder)

| File Name                                  | Description                                                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------- |
| clean_orders.csv                           | Orders file after removing duplicates and leakage entries (ordered after snapshot date) |
| monthly_revenue_by_category.csv            | Monthly revenue grouped by category                                                     |
| monthly_revenue_percentage_by_category.csv | Monthly revenue percentage per category                                                 |

### Output Image Files (Under "images" folder)

| File Name                                       | Description                                              |
| ----------------------------------------------- | -------------------------------------------------------- |
| T3P1_web_events_eda_dashboard.png               | EDA for web events data                                  |
| T3P1_support_tickets_eda_dashboard.png          | EDA for support data                                     |
| T3P1_quantity_stacked_with_return_rate_line.png | Total Order quantity and accepted / return qty over time |
| T3P1_monthly_orders_split_and_revenue.png       | Monthly orders and revenue                               |
| T3P1_intervention_history_eda_dashboard.png     | EDA for Intervention data                                |
| T3P1_hypothesis_7_cart_abandonment.png          | Churn rate by cart abandonment                           |
| T3P1_hypothesis_6_loyalty_tier.png              | Churn rate by loyalty tier                               |
| T3P1_hypothesis_5_priority_bucket.png           | Churn rate by manual priority bucket                     |
| T3P1_hypothesis_4_product_views.png             | Churn rate by product views                              |
| T3P1_hypothesis_3_purchase_frequency.png        | Churn rate by purchase frequency                         |
| T3P1_hypothesis_2_visit_recency.png             | Churn rate by App/Web Visit recency                      |
| T3P1_hypothesis_1_order_recency.png             | Churn rate by order recency                              |
| T3P1_customer_categorical_distributions.png     | Distribution of customers by categories                  |
| T3P1_churn_labels_eda_dashboard.png             | Churn distribution                                       |
| T3P1_category_quantity_and_orders_combo.png     | Average order quantity and volume by category            |

### Documents

| File Name              | Description                                                    |
| ---------------------- | -------------------------------------------------------------- |
| data_quality_report.md | Data quality issues found                                      |
| business_memo.md       | A business-facing memo, referring to specific dataset patterns |
