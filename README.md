# NEXESAT-COMMUNICATION
CLV SEGEMENTATION FOR NEXESAT COMMUNICATION REVENUE GROWTH
### TOOLS USED :
- PROGRESQL SERVER FOR CLEANING AND WRITING QUERIES 

- POWER BI FOR VISUALISATION AND BUILDING DASHBOARD

### DATASET:

AMDARI [DOWNLOAD HERE](https://www.amdari.io/projects)

### BUSINESS PROBLEM

NexaSat, a telecom company, struggles with optimizing its marketing strategies due to its diverse customer base. The current one-size-fits-all approach has proven ineffective in driving engagement and increasing revenue. To remain competitive, NexaSat needs to identify high-potential customer segments and target them with personalized offers to boost average revenue per user (ARPU).

### PROJECT OBJECTIVE

The project aims to implement Customer Lifetime Value (CLV) segmentation to categorize customers based on their long-term value. By doing so, NexaSat can tailor marketing efforts, focus on high-value segments, and increase revenue through up-selling and cross-selling. The goal is to enhance customer satisfaction, loyalty, and overall profitability.

### DATA ANALYSIS STEPS

From the existing dataset, there were a number of churned customers and i wanted to work with only existing customers to get the true analysis of the Company's current database; 
hence, i created a table and a column of the cusomer lifetime value (CLV) using SQL codes. 
I then processed to update the table by  calculating the CLV scores with monthly bill 30%, tenure 40%, call duration 10%, data usage 10%, preminum 10%. 

Check out the syntax i used:

```SQL
UPDATE existing_users
SET clv_scores =
		(0.4 * monthly_bill_amount) +
		(0.3 * tenure_months) +
		(0.1 * call_duration) +
		(0.1 * data_usage) +
		(0.1 * CASE WHEN plan_level = 'Preminum'
		THEN 1 ELSE 0
		END);
 ```

and then created another column for the CLV segments by categorizing  the customers based on there respective scores.

The syntax:
```SQL
UPDATE existing_users
SET clv_segments =
				CASE WHEN clv_scores > (SELECT percentile_cont (0.85)
										WITHIN GROUP (ORDER BY clv_scores)FROM existing_users)
										THEN 'High_value'
					 WHEN clv_scores >= (SELECT percentile_cont (0.50)
										WITHIN GROUP (ORDER BY clv_scores)FROM existing_users)
										THEN 'Moderate_value'
					WHEN clv_scores >= (SELECT percentile_cont (0.25)
										WITHIN GROUP (ORDER BY clv_scores)FROM existing_users)
										THEN 'Low value'
										ELSE 'Churn_risk'
										END;
```


