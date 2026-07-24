# User Engagement & Business Performance Analytics (SQL / BigQuery)

This repository contains a suite of advanced SQL scripts designed for product funnel analytics, email marketing performance analysis, cumulative financial metrics tracking, and query optimization.


##  Repository Contents & Technical Details

### 1.  A/B Testing & Product Funnel Analysis (`ab_testing_product_funnel.sql`)
* **Objective:** Consolidate and standardize product funnel data (sessions, orders, custom events, and new accounts) to evaluate A/B test results.
* **Technical Highlights:**
  * Implemented sequential **CTEs** (`sesion_info`, `sesion_with_orders`, `events`, `account`) to structure data flows.
  * Consolidated disparate user action metrics into a unified view using **`UNION ALL`**.
  * Multi-dimensional segmentation across geography (`country`, `continent`), device types (`device`), and acquisition channels (`channel`).

### 2. Cumulative Revenue & Prediction Performance Tracker (`cumulative_revenue_tracker.sql`)
* **Objective:** Track running total revenue (Cumulative Revenue) and benchmark actual performance against predicted targets.
* **Technical Highlights:**
  * Created data abstraction layers using a **SQL View** (`Students.v_CHIGUR_view_task`).
  * Handled missing/null data gracefully with `COALESCE(v.daily_revenue, 0)`.
  * Utilized **window functions** (`SUM(...) OVER (ORDER BY report_date)`) to calculate running totals.
  * Employed `SAFE_DIVIDE` for error-free percentage tracking of target fulfillment (`fulfillment_pct`).

### 3.  Query Optimization & Architecture Refactoring (`sql_query_optimization.sql`)
* **Objective:** Refactor inefficient legacy SQL queries evaluating email campaign performance (Open Rate, CTR, CTOR) to significantly reduce database load.
* **Technical Highlights:**
  * **"Before" Issue:** Expensive nested subqueries combined with redundant table `JOIN`s resulted in row multiplication and costly `COUNT(DISTINCT)` operations.
  * **"After" Optimization:** Streamlined execution plan by pushing filter conditions (`a.is_unsubscribed = 0`) directly into `JOIN` clauses and eliminating unnecessary subqueries.

### 4.  User Behavior & Email Engagement Analytics (`user_behavior_tracking.sql`)
* **Objective:** Build an aggregated analysis of user activity and email engagement, concluding with regional market rankings.
* **Technical Highlights:**
  * Separated account-level and email-level engagement metrics into modular CTEs prior to unification.
  * Applied advanced nested window functions with aggregation: `SUM(SUM(...)) OVER (PARTITION BY country)`.
  * Ranked top-performing markets using **`DENSE_RANK()`** and filtered for **Top-10** key markets.

---

## Tech Stack
* **DBMS / Dialect:** Google BigQuery / ANSI SQL
* **Key Concepts & Methods:** Common Table Expressions (CTEs), Window Functions (`SUM OVER`, `DENSE_RANK`), `UNION ALL`, `SAFE_DIVIDE`, Aggregations, Query Refactoring & Optimization.
