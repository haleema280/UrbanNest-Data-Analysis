Executive Summary

This dashboard analyzes Urban Nest's e-commerce performance to identify the factors behind the revenue decline between August and September.
The business generated a Total Revenue of 89.72M from 20,570 orders, with an Average Order Value (AOV) of 4,361.62. Monthly revenue showed a noticeable decline before recovering, indicating fluctuations in customer purchasing behavior. The SAVE30 discount campaign contributed the highest discount amount, totaling 5,038,765.11. While discounts may have supported sales, their impact on profitability requires further evaluation.
The analysis suggests that the revenue decline was primarily driven by a reduction in order volume rather than a decrease in average order value.

Key Insights

1-Total Revenue: 89.72M
2-Total Orders: 20,570
3-Average Order Value (AOV): 4,361.62
4-Total Discount Given: 5,038,765.11
5-Top Discount Code: SAVE30
6-Revenue declined by 20.27% from August to September.
7-Order volume decreased by 3%, making it the primary contributor to the revenue decline.

Business Questions & Answers

1. By what percentage did revenue decrease from August to September?
Answer: Revenue decreased by 20.27%.
SQL QUERY:
SELECT 
((SUM(CASE WHEN MONTH(order_date)=9 THEN net_revenue END) - 
  SUM(CASE WHEN MONTH(order_date)=8 THEN net_revenue END)) / 
  NULLIF(SUM(CASE WHEN MONTH(order_date)=8 THEN net_revenue END),0)) * 100 
AS Revenue_Decrease_Percent
FROM `RAW-DATA`;

2. How much did order volume decrease?
Answer: Order volume decreased by 3%.
SQL QUERY:
SELECT
((COUNT(CASE WHEN MONTH(order_date)=9 THEN order_id END) - 
  COUNT(CASE WHEN MONTH(order_date)=8 THEN order_id END)) / 
  NULLIF(COUNT(CASE WHEN MONTH(order_date)=8 THEN order_id END),0)) * 100 
AS Order_Decrease_Percent
FROM `RAW-DATA`;

3. What was the primary driver of the revenue decline?
Answer: The decline was mainly caused by lower order volume rather than a decrease in Average Order Value.
SQL QUERY:
-- Check AOV
SELECT 
SUM(net_revenue)/COUNT(order_id) as AOV
FROM `RAW-DATA`
WHERE MONTH(order_date) IN (8,9);

4. Which discount code generated the highest discount amount?
Answer: SAVE30 generated the highest total discount.
SQL QUERY:
SELECT discount_code, SUM(discount_amount) as Total_Discount
FROM `RAW-DATA`
GROUP BY discount_code
ORDER BY Total_Discount DESC
LIMIT 1;

5. What was the total discount amount?
Answer: 5,038,765.11
SQL QUERY:
SELECT SUM(discount_amount) as Total_Discount_Budget FROM `RAW-DATA`;

Recommendations

1-Evaluate the ROI and profitability of the SAVE30 discount campaign before making budget decisions.
2-Investigate the reasons behind the decline in order volume during September.
3-Track additional KPIs such as Profit Margin, Conversion Rate, and Repeat Purchase Rate for deeper business insights.
4-Analyze sales performance by product category, customer segment, and marketing channel to identify growth opportunities.
5-Continue monitoring monthly revenue trends to detect early signs of performance decline.

 
