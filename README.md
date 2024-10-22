# NEXESAT-COMMUNICATION
CLV SEGEMENTATION FOR NEXESAT COMMUNICATION REVENUE GROWTH


## TABLE OF CONTENTS
 - [TOOLS USED](tools-used)
 - [DATASET](dataset)
 - [BUSINESS PROBLEM](business-problem)
 - [PROJECT OBJECTIVE](project-objective)
 - [DATA ANALYSIS STEPS](data-analysis-steps)
 - [DATA OVERVIEW](data-overview)
 - [PROJECT FINDINGS](project-findings)
 - [RECOMMENDATION FOR NEXESAT MARKETING STRATEGY](recommendation-for-nexesat-marketing-strategy)


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

### DATA OVERVIEW

We will analyze NexaSat’s July 2023 customer data, which includes key variables like:
 
 1. Customer demographics (e.g., gender, partner status, dependents).
 2. Service usage (call duration, data usage).
 3. Plan details (type and level).

### PROJECT FINDINGS

The analysis of NexaSat's customer data from June 2023 revealed several important insights. Out of 7,043 total users, 2,771 customers have churned, leaving 4,272 current users for analysis. Key findings include:
  - User Distribution by Plan Level
     -  Premium Users: 3,015
     - Basic Users: 1,275
  - Revenue Breakdown:
    Total revenue from all users amounted to $1,054,953.70, with plan-specific revenue as follows:
     - Premium Plan: $522,948.15
     - Basic Plan: $150,026.00
  - Customer Categories and Revenue:
    - Postpaid Premium: $319,836.15
    - Prepaid Premium: $203,112.00
    - Postpaid Basic: $107,502.00
    - Prepaid Basic: $42,524.00
  - Customer Lifetime Value (CLV) Segmentation: Based on key factors like monthly bill, tenure, call duration, data usage, and plan type, users were categorized into four segments:
    - High Value: Average monthly charges of $311.85 with 641 users generating $6,449,883.15.
    - Moderate Value: Average monthly charges of $159.37 with 1,495 users generating $7,715,584.50.
    - Low Value: Average monthly charges of $120.87 with 1,068 users generating $3,684,117.10.
    - Churn Risk: Average monthly charges of $99.05 with 1,068 users generating $1,636,504.60.
  -  Upselling and Cross-Selling Strategy:

     - Cross-Selling: Offer tech support services to senior citizens and users with dependents/partners but no multiple lines.

     - Upselling: Target churn-risk Basic users to upgrade to Premium plans with longer lock-in times, increasing ARPU.

     - Reward Strategy: Provide additional call time and data to high-value and moderate-value customers as a loyalty incentive.

 ### RECOMMENDATION FOR NEXESAT MARKETING STRATEGY

 To address the issues with the current marketing approach, NexaSat should adopt a more personalized, data-driven strategy based on the Customer Lifetime Value (CLV) segmentation findings. Here are the key 
 recommendations:

  1. **Focus on High-Value and Moderate-Value Customers:**

     - **Loyalty Programs:** Introduce a reward system that offers additional call time, data, or exclusive discounts to high-value and moderate-value customers. This will encourage continued usage and enhance 
        customer loyalty, ultimately increasing ARPU.

     - **Exclusive Offers:** Provide early access to new services or products, and create exclusive bundles tailored to their usage patterns, encouraging further engagement and spending.

  2. **Upsell to Churn-Risk Users:**

     - **Targeted Upgrading:** Implement campaigns to convert churn-risk Basic users to Premium plans. Emphasize benefits like better rates on data and call usage, and longer lock-in times to secure continued 
        subscription and reduce churn rates.

     - **Incentivize Upgrades:** Offer incentives such as a discounted first month or added data packages for users who upgrade to higher-tier plans, making the transition more attractive.

  3. **Cross-Sell Opportunities for Diverse Segments:**
     - **Tech Support for Specific Groups:** Promote tech support services to senior citizens and users with dependents/partners who lack multiple lines. This personalized approach will increase engagement and 
         drive additional revenue through value-added services.
     - **Bundled Packages:** Encourage multi-line plans for households, providing discounts when adding lines or additional services. This not only increases revenue but also helps to secure customer loyalty 
         across multiple users within a household.

  4. **Personalized Communication:**

     - **Segmented Marketing Campaigns:** Develop customized marketing campaigns that speak directly to the needs of each customer segment. Use insights from their service usage, demographics, and previous 
         behavior to craft messages that resonate, increasing the likelihood of engagement.

     - **Proactive Engagement:** Anticipate customer needs based on their usage patterns and lifecycle stage. Reach out to users before they reach the churn-risk segment with special offers or service 
        improvements to prevent churn.

   By focusing on targeted, data-driven marketing strategies and customer engagement, NexaSat can maximize its revenue, reduce churn, and build stronger, long-lasting customer relationships.


 
    

  




