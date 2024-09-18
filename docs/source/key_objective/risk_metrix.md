# Key Risk Metrics (WIP)

## What is Risk?

Risk is a multifaceted concept that defies a single, universal definition. In Modern Portfolio Theory, for instance, risk is often equated with the variability of returns. However, this definition raises several critical questions:

1. Is it appropriate to assume that return variability follows a normal distribution?
2. Does variance remain a relevant concern for investors with extended time horizons?
3. Should we assign equal importance to downside risk and upside potential?

These questions underscore the necessity for investors to carefully define their specific risk concerns based on their unique circumstances and objectives.

In the realm of consumer finance credit risk, the concept of risk takes on a different dimension. Here, the variability of returns proves inadequate as a risk metric due to two primary factors:

1. Short-term nature: Consumer finance typically involves shorter tenures, making absolute loss a more pressing concern than return variability.
2. Limited historical data: Often, there's insufficient historical data available to reliably calculate return variability, particularly for new products or markets.

Consequently, in consumer finance credit risk management, we focus more on metrics that directly measure the probability and magnitude of potential losses, rather than on the variability of returns.

## Considerations in Defining Key Risk Metrics

### Granularity

- Portfolio Level: Encompasses all outstanding loans, providing a comprehensive view of the entire loan book.
- Loan Level: Focuses on individual loans or groups of loans aggregated by specific criteria, allowing for more detailed analysis. (Further elaborated in the subsequent section)
- Installment Level: Examines individual installments or groups of installments aggregated by certain criteria, offering the most granular view of repayment behavior.

### Aggregation

Loans or installments are typically aggregated to provide a more comprehensive and meaningful analysis of risk patterns. This aggregation is essential because the risk of individual loans or installments is less informative than the collective risk profile. Common aggregation methods include:

1. Loan Product: 
   - Different loan products (e.g., personal loans, mortgages, credit cards) have distinct risk characteristics.
   - Aggregating by product type allows for tailored risk management strategies.

2. Time Period:
   - Aggregation by specific time frames, such as:
     - Calendar month or quarter
     - First three months after disbursement
     - Vintage (loans originated in the same period)
   - Enables trend analysis and seasonality detection.

3. User Segments:
   - Categorization based on borrower characteristics, such as:
     - First-time borrowers vs. repeat borrowers
     - Credit score ranges
     - Demographics (age, income, occupation)
   - Helps in understanding risk profiles of different customer groups.

4. Geographic Location:
   - Aggregation by region, city, or country.
   - Useful for identifying location-specific risk factors.

5. Loan Purpose:
   - Grouping loans by their intended use (e.g., education, home improvement, debt consolidation).
   - Provides insights into risk associated with different loan purposes.

6. Loan Size:
   - Categorizing loans by amount (e.g., small, medium, large).
   - Helps in understanding the relationship between loan size and risk.

These aggregation methods can be used individually or in combination to gain deeper insights into risk patterns and inform targeted risk management strategies.

### Definition of Default

Default is typically defined as a missed payment for a specified number of days, denoted as $x$. Common values for $x$ include 30, 60, 90, 120, 180, and 360 days. As $x$ increases, so does the required observation period. This presents a significant challenge in credit risk management: how to effectively map short-term performance indicators to long-term outcomes. This challenge arises because:

1. Longer observation periods (larger $x$) provide more reliable indicators of true default risk but delay decision-making.
2. Shorter observation periods (smaller $x$) allow for quicker risk assessment but may not accurately reflect long-term default patterns.
3. The relationship between short-term and long-term default rates may not be linear or consistent across different customer segments or economic conditions.

This topic will be explored in greater depth in Session 3.

### Unit of Measurement

Risk metrics can be measured using various units, each providing different insights into the portfolio's performance:

1. Number of Users:
   - Measures the count of unique borrowers affected.
   - Useful for understanding the breadth of risk exposure across the customer base.
   - Example: "500 users defaulted in the last quarter."

2. Amount of Money:
   - Quantifies the financial impact of risk events.
   - Typically expressed in monetary terms (e.g., dollars, euros).
   - Provides a clear picture of the economic significance of risk.
   - Example: "$1 million in loans are currently past due."

3. Number of Loans/Installments:
   - Counts individual loan contracts or installments affected.
   - Less common in practice 
   - Example: "50 installments missed payment this month."

4. Percentage or Ratio:
   - Expresses risk as a proportion of the total portfolio.
   - Allows for easier comparison across different time periods or portfolio segments.
   - Example: "3% of the user is in default."

The choice of unit depends on the specific risk metric, reporting requirements, and the intended audience for the analysis.

### Observation Time

The observation time is a crucial factor in risk metrics. It determines the period over which we assess the performance of loans or portfolios. Common observation times include:

1. Point-in-Time (PIT): Measures risk at a specific moment, such as the end of a month or quarter.

2. Cumulative: Assesses risk over an extended period, often from the loan's origination to a specific point in time.

3. Vintage-based: Groups loans by their origination period and tracks their performance over time.

4. Rolling Window: Evaluates risk over a moving time frame, such as the last 3 or 12 months.

5. Maturity-based: Observes risk up to the loan's maturity date or a predefined period after origination.

The choice of observation time depends on the specific risk metric, the nature of the loan product, and the analytical objectives. For example, vintage analysis typically uses cumulative observation time, while portfolio-level metrics might use point-in-time or rolling window approaches.

## Commonly Used Risk Metrics

### First Past Due (FPD)

First Past Due (FPD) is a crucial early warning indicator in credit risk management. It measures the occurrence of the first missed payment or delay in a loan's repayment schedule. Key points about FPD include:

1. Definition:
   - FPD refers to the first instance when a borrower misses a scheduled payment.
   - It's typically measured in days, indicating how soon after loan origination the first delinquency occurs.

2. Significance:
   - Early predictor of credit risk: FPD can signal potential future delinquencies or defaults.
   - Portfolio quality indicator: A high FPD rate may suggest issues with underwriting or economic stress.

3. Calculation:
   - FPD Rate (Count-based) = (Number of loans/users with FPD within observation period) / (Total number of loans/users originated in the same period) * 100
   - FPD Rate (Amount-based) = (Total amount of loans with FPD within observation period) / (Total amount of loans originated in the same period) * 100

4. Observation Period:
   - Often measured within the first 30, 60, or 90 days after loan origination.
   - The specific period may vary based on the product type and risk management practices.

5. Applications:
   - Underwriting assessment: Helps refine credit scoring models and lending criteria.
   - Early intervention: Enables timely customer outreach and collection efforts.

6. Limitations:
   - Does not capture the severity or persistence of delinquency.
   - May be influenced by external factors (e.g., payment system issues) unrelated to borrower creditworthiness.

FPD is often used in conjunction with other metrics to provide a comprehensive view of portfolio risk and loan performance.

### First Three Past Due (3FPD)

First Three Past Due (3FPD) is an extension of the First Past Due (FPD) metric, providing a more comprehensive view of early-stage delinquency patterns. This metric focuses on the occurrence of three consecutive missed payments within a specified timeframe. Key aspects of 3FPD include:

1. Definition:
   - 3FPD refers to the instance when a borrower misses any payment in the first three months after loan origination.

2. Significance:
   - Stronger indicator of credit risk: 3FPD suggests a more persistent payment problem compared to a single missed payment.
   - Predictive power: It can be a reliable predictor of serious delinquency or default.

3. Calculation:
   - 3FPD Rate (Count-based) = (Number of loans/users with at least one missed payment in the first three months) / (Total number of loans/users originated in the same period) * 100
   
   Note: 3FPD is typically calculated at the count level (number of loans or users) rather than the amount level. This approach focuses on the frequency of early delinquencies across the portfolio, regardless of loan size.

4. Observation Period:
   - Typically measured within the first three months after loan origination.
   - The specific observation period is fixed at three months, regardless of product type or loan term, to maintain consistency with the 3FPD definition.
   - This standardized timeframe allows for more accurate comparisons across different loan products and risk management strategies.

5. Comparison with FPD:
   - More stringent measure: 3FPD indicates a more serious repayment issue than FPD.
   - Lower occurrence rate: Typically, 3FPD rates are lower than FPD rates, but may signal higher risk.

6. Limitations:
   - May not capture borrowers who alternate between delinquency and repayment.
   - Could be affected by short-term financial difficulties that borrowers eventually overcome.

3FPD is often used in combination with other early-warning indicators to provide a nuanced understanding of portfolio risk and to trigger appropriate risk management actions.

### Days Past Due (DPD)

Days Past Due (DPD) is a fundamental metric in credit risk management that measures the extent of delinquency for a loan or a group of loans. It provides a snapshot of the current repayment status and is widely used in risk assessment and reporting. Key aspects of DPD include:

1. Definition:
   - DPD represents the number of days that have elapsed since a loan or installment payment was due but not paid in full.
   - It is calculated from the due date of each unpaid or partially paid loan or installment, not necessarily the most recent one.

2. Significance:
   

3. Calculation:
   DPD Rate can be expressed at different levels:
   a) Loan/Installment level: 
      DPD Rate = (Number of loans/installments with DPD > 0) / (Total number of loans/installments) * 100
   b) User level:
      DPD Rate = (Number of users with at least one loan/installment with DPD > 0) / (Total number of users) * 100
   c) Amount level:
      DPD Rate = (Total outstanding amount of loans/installments with DPD > 0) / (Total outstanding amount of all loans/installments) * 100

   These can be calculated for specific DPD buckets, e.g., 
   DPD 30+ Rate (Amount level) = (Total outstanding amount of loans/installments with DPD ≥ 30) / (Total outstanding amount of all loans/installments) * 100

4. Common DPD Buckets:
   - Current (0 DPD)
   - 1-30 DPD
   - 31-60 DPD
   - 61-90 DPD
   - 90+ DPD (often considered as default)

5. Applications:
   - Risk classification: Loans and users are often categorized into risk buckets based on their DPD.
   - Collection strategies: Different collection approaches may be applied based on DPD ranges.
   - Provisioning: Loan loss provisions are often tied to DPD buckets.
   - Credit scoring: DPD history is a key input in many credit scoring models.

6. Limitations:
   - May not reflect true risk for all product types: For example, credit cards with minimum payment requirements may have different risk implications.
   - Can be reset: In some cases, if a borrower makes a partial payment, it might reset the DPD counter, potentially masking ongoing repayment issues.
   - User-level DPD may not capture the full extent of delinquency for users with multiple loans.
   - Amount-level DPD might be skewed by a few large loans, potentially overshadowing issues with numerous smaller loans.

### Ever Max Days Past Due (Ever Max DPD)

Ever Max Days Past Due (Ever Max DPD) is a historical metric that captures the worst delinquency status a loan or borrower has experienced over a specified period. This metric provides valuable insights into past repayment behavior and is often used in credit risk assessment. Key aspects of Ever Max DPD include:

1. Definition:
   - Ever Max DPD represents the highest number of days past due that a loan or borrower has reached within a given time frame.
   - It can be calculated for individual loans, borrowers with multiple loans, or across an entire portfolio.

2. Significance:
   - Historical risk indicator: Ever Max DPD offers a view of the borrower's worst-case repayment behavior, which can be predictive of future default risk.
   - Complement to current status: While current DPD shows present status, Ever Max DPD provides context on past difficulties.
   - Input for credit scoring: This metric is often used in credit scoring models to assess creditworthiness.

3. Calculation:
   - For a single loan: Ever Max DPD = Maximum DPD reached during the observation period
   - For a borrower with multiple loans: Ever Max DPD = Maximum DPD across all loans during the observation period
   - For a portfolio: Can be expressed as a distribution or average of Ever Max DPD across all loans/borrowers

4. Observation Period:
   - The time frame for Ever Max DPD can vary based on the lender's policies and the specific use case.
   - Common periods include:
     - Since origination (for the entire loan life)
     - Last 12 months
     - Last 24 months

5. Applications:
   - Risk segmentation: Grouping borrowers based on their Ever Max DPD for targeted risk management strategies.
   - Underwriting decisions: Used in loan approval processes, especially for returning borrowers.
   - Pricing models: Can influence interest rates or loan terms offered to borrowers.
   - Early warning systems: Helps identify borrowers who may be at higher risk of future delinquency.

6. Limitations:
   - May not reflect recent improvements: A borrower might have had a high Ever Max DPD in the past but has since improved their financial situation.
   - Sensitive to observation period: The chosen time frame can significantly impact the metric's value and interpretation.
   - Doesn't capture frequency: It doesn't show how often a borrower has been delinquent, only the worst instance.

Ever Max DPD is a powerful tool in the credit risk manager's toolkit, offering a glimpse into a borrower's or portfolio's past repayment challenges. However, it should be used in conjunction with other metrics to form a comprehensive view of credit risk.

### Current Days Past Due (Current DPD)

Current Days Past Due (Current DPD) is a metric that indicates the present delinquency status of loans that are not fully repaid. It provides a snapshot of repayment behavior for loans that still have outstanding balances. Key aspects of Current DPD include:

1. Definition:
   - Current DPD represents the number of days a loan payment is overdue for loans that have not been fully repaid.
   - It is typically calculated for each loan with an outstanding balance and can be aggregated for borrowers with multiple such loans or across portfolios.

2. Significance:
   - Active loan indicator: Current DPD offers a view of repayment status for loans that are still in the repayment phase.
   - Risk assessment tool: It's used for identifying potential issues in the portion of the loan book that is not yet fully settled.
   - Performance metric: Helps in evaluating the ongoing repayment behavior of borrowers with active loans.

3. Calculation:
   - Current DPD = Current Date - Due Date of Oldest Unpaid Installment (for loans not fully repaid)
   - For borrowers with multiple active loans: Can be expressed as the highest Current DPD across all loans with outstanding balances.

4. Applications:
   - Portfolio monitoring: Used in dashboards and reports for assessing the repayment status of active loans.
   - Early warning system: Helps identify loans that may be at risk of default before they reach critical delinquency levels.
   - Collection strategies: Informs the prioritization and approach for collection efforts on loans with outstanding balances.
   - Risk segmentation: Allows for grouping of active loans based on their current repayment status.

5. Limitations:
   - Doesn't reflect full loan history: Only shows the current status, not past repayment behavior.
   - May not capture partial payments: Depending on the calculation method, it might not accurately reflect partial repayments made.
   - Not applicable to fully repaid loans: This metric is only relevant for loans with remaining balances.

Current DPD for loans that are not fully repaid is a crucial metric in credit risk management, providing real-time insights into the repayment status of active loans. It serves as an important tool for monitoring portfolio health, guiding collection efforts, and identifying potential risks in the active loan book. However, it should be used in conjunction with other metrics to form a comprehensive view of credit risk across the entire loan lifecycle.

### Vintage

### Flow Rate

### Net Portfolio Loss (NPL)

Net Portfolio Loss (NPL) is a crucial metric in credit risk management that quantifies the actual losses incurred by a lender due to defaulted loans. It is commonly reported in financial statements. Key aspects of NPL include:

1. Definition:
   - NPL represents the total amount of loans that are deemed uncollectible, typically after exhausting all recovery efforts.

2. Significance:
   - Direct measure of credit risk: NPL directly reflects the financial losses due to credit risk.
   - Performance indicator: It serves as a key performance indicator for the effectiveness of credit risk management strategies.
   - Profitability impact: NPL directly affects the lender's profitability and capital adequacy.

3. Calculation:
   - NPL = (Total value of defaulted loans - Recoveries) / Total loan portfolio value * 100
   - This calculation can be done for a specific period (e.g., monthly, quarterly, annually) or cumulatively.

4. Components:
   - Defaulted loans: Loans that have been classified as unlikely to be repaid, often after a specific period of delinquency.
   - Recoveries: Any amounts collected from defaulted loans through various recovery methods (e.g., collateral liquidation, debt collection).

5. Applications:
   - Setting risk appetite: NPL helps in defining acceptable loss levels for different product lines or customer segments.
   - Provisioning: It guides the process of setting aside reserves for expected losses.
   - Strategy adjustment: High NPL rates may trigger reviews and adjustments in lending strategies or risk policies.

6. Limitations:
   - Lagging indicator: NPL is a backward-looking metric and may not immediately reflect changes in portfolio quality.
   - Influenced by write-off policies: Different institutions may have varying policies on when to write off loans, affecting NPL comparability.

NPL is a critical metric for financial institutions, regulators, and investors as it provides clear insight into the actual losses incurred due to credit risk. Regular monitoring and analysis of NPL trends are essential for maintaining a healthy loan portfolio and ensuring the financial stability of lending institutions.

### Cost of Risk (CoR)

### Roll Rate

Roll Rate is a dynamic metric used in credit risk management to measure the likelihood of loans transitioning from one delinquency status to another over a specific time period. It provides valuable insights into the deterioration or improvement of loan portfolio quality. Key aspects of Roll Rate include:

1. Definition:
   - Roll Rate represents the percentage of loans that "roll" or move from one delinquency bucket to another in a given time frame.
   - It can measure both forward movement (worsening) and backward movement (improvement) in delinquency status.

2. Significance:
   - Predictive power: Roll Rates help forecast future delinquencies and potential losses.
   - Early warning indicator: Increasing Roll Rates can signal deteriorating portfolio quality before it's reflected in other metrics.
   - Strategy evaluation: It helps assess the effectiveness of collection strategies and risk management policies.

3. Calculation:
   Roll Rate = (Number of loans moving from bucket A to bucket B) / (Total number of loans in bucket A at the start of the period) * 100

   Example:
   30-60 DPD Roll Rate = (Loans moving from 30 DPD to 60 DPD) / (Total loans at 30 DPD at period start) * 100

4. Common Roll Rate Transitions:
   - Current to 30 DPD
   - 30 DPD to 60 DPD
   - 60 DPD to 90 DPD
   - 90 DPD to 120 DPD (or Default)

5. Applications:
   - Loss forecasting: Roll Rates are used in models to project future losses.
   - Risk-based pricing: Higher Roll Rates may lead to increased interest rates for certain risk segments.
   - Collection resource allocation: Areas with high Roll Rates may require more intensive collection efforts.
   - Credit policy adjustments: Persistent high Roll Rates might trigger tightening of credit policies.

6. Limitations:
   - Assumes consistent behavior: Roll Rates may not capture sudden changes in economic conditions or borrower behavior.
   - Requires sufficient data: Accurate Roll Rate calculation needs a large sample size and historical data.
   - May oversimplify: Roll Rates don't always capture the complexity of factors influencing loan performance.

Roll Rate analysis is a powerful tool in credit risk management, providing a dynamic view of portfolio behavior. When used in conjunction with other metrics like DPD and Vintage analysis, it offers a comprehensive understanding of credit risk trends and helps in proactive risk management.

### Summary Table

|Metric|Granularity|Aggregation|Unit of Measurement|Observation Time|
|------|-----------|-----------|------------------|----------------|
|
