# DataAnalytics-Assessment
Data Analytics Assessment Project

Question 1: High-Value Customers with Multiple Products
Approach to Solution:
The task was to identify customers who have both funded savings and investment plans. These customers are considered high-value due to their engagement with multiple products.
•	I joined the savings transactions table with the plans and users table to get access to customer data and plan types.
•	Used CASE statements to count how many savings and investment plans a customer had.
•	Ensured uniqueness using DISTINCT to avoid multiple counts per plan.
•	Summed the confirmed_amount field to calculate how much the customer has deposited.
•	Filtered for customers who had at least one of each type of funded plan.
Outcome
This produced a list of cross-engaged users sorted by total deposit volume, useful for upsell and loyalty programs.
________________________________________
Question 2: Customer Lifetime Value (CLV) Estimation
Approach to Solution:
Marketing needed to estimate a simplified version of CLV using tenure and transaction volume.
•	Calculated account tenure in months using the TIMESTAMPDIFF function.
•	Counted the total number of transactions per user.
•	Estimated CLV using the formula:
CLV = (total_transactions / tenure) * 12 * avg_profit_per_transaction
where profit_per_transaction was assumed to be 0.1% of the transaction amount.
•	Rounded the result to two decimal places.
Outcome
The output shows customers ranked by estimated CLV, providing insight into which customers deliver the most long-term value.
________________________________________
Question 3: Inactive Account Detection
Approach to Solution:
The aim of this task is to identify accounts with no inflows for over a year.
•	Defined account types (Savings or Investment) using flags from the plans table.
•	Used a subquery to find each plan's latest confirmed inflow transaction date.
•	Calculated the number of days since the last transaction using DATEDIFF.
•	Filtered out accounts with over 365 days of inactivity or no inflows at all.
Outcome
The result highlights dormant accounts that can be targeted for reactivation campaigns.
________________________________________
Question 4: Transaction Frequency Analysis
Approach to Solution
The goal of this task was to classify customers into frequency tiers based on their average monthly transaction counts.
•	Extracted the year and month from transaction dates to group monthly activity.
•	Calculated the average number of transactions per month for each customer.
•	Categorized customers using CASE:
o	High Frequency (≥10/month)
o	Medium Frequency (3–9/month)
o	Low Frequency (≤2/month)
•	Aggregated and summarized the number of users in each category.
Outcome
This analysis supports segmentation strategies and can inform notification or reward systems based on customer activity levels.
________________________________________
Challenges encountered during this assessment:
•	Handling Zero Division in CLV Calculation: When calculating tenure, some accounts had 0 months (if they signed up very recently), which would cause a division by zero. I resolved this using NULLIF() to avoid runtime errors.
•	Ensuring Unique Plan Counts: In the high-value customer query, multiple transactions on the same plan were being double-counted. I addressed this by using DISTINCT on the plan IDs.
•	Accurate Inactivity Detection: Some accounts had no inflows at all, making their last_transaction_date null. I handled these separately in the logic to ensure they weren’t skipped.

