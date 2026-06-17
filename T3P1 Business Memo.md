**Executive Summary**

Our core customer directory reveals a severe baseline churn risk, with **46.96%** of active customer profiles failing to make a purchase during our standard evaluation window. While launching an immediate, widespread retention campaign is tempting, our cross-functional data analysis indicates that an un-targeted marketing blast will result in significant capital waste and fail to fix the underlying drivers of customer attrition.

Before committing marketing capital, the company must investigate and address five critical operational, financial, and behavioural realities.

**Critical Areas for Pre-Launch Investigation**

**1\. Overhaul the Campaign Budget Allocation Model**

Our internal tracking shows a major strategic gap in how outreach funds are spent. The marketing team currently spends nearly the exact same average budget (approx **Rs 18.50** per customer) across all risk tiers:

- **Low-Risk Tier:** Churn rate of **10.04%**
- **High-Risk Tier (Critical Threat):** Churn rate of **74.72%**

**Required Action:** We must halt this uniform spending approach. Before launching any campaigns, marketing workflows must be reconfigured to redirect capital away from naturally secure segments and focus budget allocations toward high-risk groups where incentives can drive incremental revenue.

**2\. Resolve High-Friction Operational Support Bottlenecks**

Customer dissatisfaction is heavily driven by logistical and product issues. While standard service requests (such as billing or damaged items) are successfully resolved in under **21 hours**, two specific categories cause major delays and drop-offs:

- **refund_delay:** Average resolution time spikes to **36.46 hours**, driving customer sentiment down to an extreme low of **\-0.65**.
- **product_reaction:** Average resolution takes **36.54 hours**, resulting in a highly elevated ticket re-opening rate of **26.80%**.

**Required Action:** We must collaborate with the Customer Operations and Quality Assurance teams to optimize these high-friction workflows _before_ launching marketing campaigns. Sending promotional emails to customers who are currently dealing with unresolved skin reactions or delayed refunds will backfire, increasing brand annoyance and accelerating churn.

**3\. Capitalize on the "Cart Abandonment Paradox"**

Standard marketing rules often treat cart abandonment as a sign of a failing relationship. However, our behavioural data reveals a clear engagement paradox:

- Customers with **0 cart abandonments** over 30 days exhibit a high **56.07%** churn rate.
- Customers with **3+ cart abandonments** exhibit a remarkably low churn rate of just **19.44%**.

**Required Action:** High cart abandonment indicates active shopping intent and strong platform interaction, rather than a final rejection of the brand. Instead of hitting these highly engaged users with aggressive, high-cost discount campaigns, we should implement low-cost, automated checkout reminders. This allows us to save valuable retention budgets for genuinely dormant segments.

**4\. Design Custom Lifecycle-Stage Interventions**

Our transactional data highlights a clear retention milestone. One-time buyers are highly unstable, carrying a **$53.12\\%$** churn rate. However, once a customer is guided to their 4th order within a 180-day window, their churn probability plummets to just **$8.11\\%$**.

**Required Action:** Rather than launching a generic retention campaign for all users, we should build a dedicated onboarding track designed specifically to transition one-time buyers into repeat spenders. The campaign should focus entirely on guiding users from their first purchase to the 4-order loyalty milestone.

**5\. Verify Data Lookback Integrity to Avoid Faulty Targets**

From an analytical standpoint, our transactional databases contain active order entries that occur after the official snapshot date of **September 30, 2025** (totaling $1,872$ post-snapshot orders).

**Required Action:** The data science and IT teams must audit all engineering flows to ensure that no post-snapshot transactions leak into training features. If future target-window data accidentally leaks into active customer profiles, our models will generate overly optimistic projections, leading the marketing team to target the wrong users based on flawed insights.

**Summary Recommendation**

To maximize return on investment (ROI), we recommend delaying the general retention campaign until we complete a targeted, two-week operational pilot. This pilot will focus on:

1.  Fixing the refund processing delay bottlenecks.
2.  Shifting marketing budgets toward the **74.72%** high-risk priority segment.
3.  Deploying automated, low-cost cart-recovery triggers for active web/app browsers.