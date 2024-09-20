# Commonly Used Risk Metrics

**Date:** September 2024
**Last updated:** September 2024

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

This topic will be explored in greater depth in [Estimating Long-term Impact from Short-term Outcome](../prediction/long_term_impact.md).

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
   - Example: "3% of the users are in default."

The relationship between user-level and amount-level metrics is influenced by credit limits and their utilization. When amount-level metrics exceed user-level metrics, it may indicate that higher-risk users are granted larger credit limits or that they utilize a significantly greater portion of their available credit compared to the average user. 

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

### Days Past Due (DPD)

Days Past Due (DPD) is a fundamental metric in credit risk management that measures the extent of delinquency for a loan or a group of loans. It provides a snapshot of the current repayment status and is widely used in risk assessment and reporting. Key aspects of DPD include:

1. Definition:
   - DPD represents the number of days that have elapsed since a loan or installment payment was due but not paid in full.

2. Calculation:
   DPD Rate can be expressed at different levels:

   a) Loan/Installment level: 
      DPD Rate = (Number of loans/installments with DPD > 0) / (Total number of loans/installments) * 100

   b) User level:
      DPD Rate = (Number of users with at least one loan/installment with DPD > 0) / (Total number of users) * 100

   c) Amount level:
      DPD Rate = (Total outstanding amount of loans/installments with DPD > 0) / (Total outstanding amount of all loans/installments) * 100

   These can be calculated for specific DPD buckets, e.g., 
   DPD 30+ Rate (Amount level) = (Total outstanding amount of loans/installments with DPD ≥ 30) / (Total outstanding amount of all loans/installments) * 100

3. Common DPD Buckets:
   - Current (0 DPD)
   - 1-30 DPD
   - 31-60 DPD
   - 61-90 DPD
   - 90+ DPD

4. Applications:
   - Risk classification: Loans and users are often categorized into risk buckets based on their DPD.

### First Past Due (FPD)

First Past Due (FPD) is a crucial early warning indicator in credit risk management. It measures the occurrence of the first missed payment or delay in a loan's repayment schedule. Key points about FPD include:

1. Definition:
   - FPD refers to the first instance when a borrower misses a scheduled payment.

2. Significance:
   - Early predictor of credit risk: FPD can signal potential future delinquencies or defaults.
   - Portfolio quality indicator: A high FPD rate may suggest issues with underwriting or economic stress.

3. Calculation:
   FPD Rate can be calculated using two main approaches:

   a) Count-based:
      FPD Rate = (Number of loans/users with DPD > 0 for their first repayment) / (Total number of loans/users first originated) * 100

   b) Amount-based:
      FPD Rate = (Total amount of loans with DPD > 0 for their first repayment) / (Total amount of loans first originated) * 100

4. Applications:
   - Underwriting assessment: Helps refine credit scoring models and lending criteria.
   - Early intervention: Enables timely customer outreach and collection efforts.

5. Limitations:
   - Does not capture the severity or persistence of delinquency.
   - May be influenced by external factors (e.g., payment system issues) unrelated to borrower creditworthiness.

### First Three Past Due (3FPD)

First Three Past Due (3FPD) is an extension of the First Past Due (FPD) metric, providing a more comprehensive view of early-stage delinquency patterns. This metric focuses on the occurrence of any missed payment within the first three months after loan origination. Key aspects of 3FPD include:

1. Definition:
   - 3FPD refers to the instance when a borrower misses any payment in the first three months after loan origination.

2. Significance:
   - Provides a more comprehensive view of early-stage delinquency patterns compared to FPD
   - Captures medium-term risk trends, offering insights into borrower behavior over a longer period
   - Helps identify persistent payment issues that may not be apparent from a single missed payment

3. Calculation:
   - 3FPD Rate (Count-based) = (Number of loans/users with at least one missed payment in the first three months) / (Total number of loans/users originated in the same period) * 100
   
   Note: 3FPD is typically calculated at the count level (number of loans or users) rather than the amount level. This approach focuses on the frequency of early delinquencies across the portfolio, regardless of loan size.

4. Observation Period:
   - Typically measured within the first three months after loan origination.
   - The specific observation period is fixed at three months, regardless of product type or loan term, to maintain consistency with the 3FPD definition.
   - This standardized timeframe allows for more accurate comparisons across different loan products and risk management strategies.

5. Limitations:
   - May not capture borrowers who alternate between delinquency and repayment.
   - Could be affected by short-term financial difficulties that borrowers eventually overcome.

### Ever Max Days Past Due (Ever Max DPD)

Ever Max Days Past Due (Ever Max DPD) is a historical metric that captures the worst delinquency status a loan or borrower has experienced over a specified period. This metric provides valuable insights into past repayment behavior and is often used in credit risk assessment. Key aspects of Ever Max DPD include:

1. Definition:
   - Ever Max DPD represents the highest number of days past due (DPD instead of DPD Rate) that a borrower has reached within a given time frame.

2. Significance:
   - Historical risk indicator: Ever Max DPD offers a view of the borrower's worst-case repayment behavior, which can be predictive of future default risk.

3. Calculation:
   - For a borrower with multiple loans: Ever Max DPD = Maximum DPD across all loans during the observation period

4. Observation Period:
   - The time frame for Ever Max DPD can vary based on the lender's policies and the specific use case.
   - Common periods include:
     - Since origination (for the entire loan life)
     - Last 12 months
     - Last 24 months

5. Applications:
   - Risk segmentation: Grouping borrowers based on their Ever Max DPD for targeted risk management strategies.
   - Underwriting decisions: Used in loan approval processes, especially for returning borrowers.

6. Limitations:
   - May not reflect recent improvements: A borrower might have had a high Ever Max DPD in the past but has since improved their financial situation.
   - Sensitive to observation period: The chosen time frame can significantly impact the metric's value and interpretation.
   - Doesn't capture frequency: It doesn't show how often a borrower has been delinquent, only the worst instance.

### Current Days Past Due (Current DPD)

Current Days Past Due (DPD instead of DPD Rate) is a metric that indicates the present delinquency status of loans that are not fully repaid. It provides a snapshot of repayment behavior for loans that still have outstanding balances. Key aspects of Current DPD include:

1. Definition:
   - Current DPD represents the number of days a loan payment is overdue for active loans with outstanding balances.
   - For borrowers with multiple active loans, it's often calculated as the highest Current DPD across all their loans.

2. Significance:
   - Active loan indicator: Current DPD offers a view of repayment status for loans that are still in the repayment phase.
   - Risk assessment tool: It's used for identifying potential issues in the portion of the loan book that is not yet fully settled.

3. Calculation:
   - Current DPD = Current Date - Due Date of Oldest Unpaid Installment (for loans not fully repaid)
   - For borrowers with multiple active loans: Can be expressed as the highest Current DPD across all loans with outstanding balances.

4. Applications:
   - Portfolio monitoring: Used in dashboards and reports for assessing the repayment status of active loans.
   - Risk segmentation: Allows for grouping of active loans based on their current repayment status.

5. Limitations:
   - Doesn't reflect full loan history: Only shows the current status, not past repayment behavior.
   - May not capture partial payments: Depending on the calculation method, it might not accurately reflect partial repayments made.
   - Not applicable to fully repaid loans: This metric is only relevant for loans with remaining balances.

### Vintage

Vintage analysis is a crucial tool in credit risk management that groups loans based on their origination period and tracks their performance over time. This method allows lenders to compare the performance of different loan cohorts and identify trends or issues in risk management practices. Key aspects of Vintage analysis include:

1. Definition:
   - Vintage refers to a group of loans originated during a specific time period, typically a month or quarter.

2. Significance:
   - Performance comparison: Allows comparison of loan performance across different origination periods.
   - Early warning indicator: Can signal potential issues in recent loan vintages before they fully mature.

3. Calculation:

   - Default Rate for Vintage X at Time T = (Number of defaulted loans in Vintage X at Time T) / (Total number of loans in Vintage X) * 100
   - The denominator is the total number of loans originated in Vintage X (Jan 2022, Feb 2022, etc.). It is a constant number.
   - The numerator is the number of defaulted loans originated in Vintage X at Time T. It is a snapshot number at a specific time point.

   Vintage analysis is often presented in a matrix or chart format:

   |Vintage|Month 1|Month 2|Month 3|...|Month 12|
   |-------|-------|-------|-------|---|--------|
   |Jan 2022|0.5%|1.0%|1.5%|...|3.0%|
   |Feb 2022|0.4%|0.9%|1.4%|...|2.8%|
   |Mar 2022|0.6%|1.1%|1.6%|...|3.2%|

4. Applications:
   - Trend analysis: Identifying patterns in loan performance across different vintages.
   - Risk forecasting: Projecting future performance based on the behavior of similar vintages.

5. Considerations:
   - Seasoning effect: Newer vintages may appear to perform better simply because they haven't had time to develop issues.
   - Economic factors: External economic conditions can impact vintage performance, making direct comparisons challenging.
   - Product changes: Modifications to loan products or underwriting criteria should be considered when comparing vintages.

### Flow Rate

Flow Rate is a crucial metric in credit risk management that measures the rate at which outstanding balances move between different delinquency buckets, typically calculated at the portfolio level at month-end. It provides insights into the dynamics of overall portfolio quality and helps predict future delinquencies. Key aspects of Flow Rate include:

1. Definition:
   - Flow Rate represents the percentage of the total outstanding balance that transitions between any delinquency buckets.

2. Significance:
   - Portfolio-wide analysis: Flow Rates show the aggregate movement of outstanding balances across all delinquency statuses, revealing broader trends in credit quality.
   - Monthly performance indicator: Provides a regular snapshot of portfolio dynamics, allowing for timely adjustments to risk management strategies.
   - Holistic early warning system: Can indicate overall deterioration or improvement in credit quality before it's reflected in static metrics.

3. Calculation (Example):

    |DPD Bucket|Outstanding Balance at 2021-12-31|Outstanding Balance at 2022-01-31|
    |----------|-----------------------------|-----------------------------
    |Current|68|70|
    |DPD 1-30|20|21|
    |DPD 31-60|13|14|
    |DPD 61-90|12|13|
    |DPD 90+|11|12|
    
    |Flow Rate|2021-12-31|2022-01-31|
    |----------|----------|----------|
    |Current to DPD 1-30||21/68|
    |DPD 1-30 to DPD 31-60|| 14/20|
    |DPD 31-60 to DPD 61-90|| 13/13|
    |DPD 61-90 to DPD 90+||12/12|

4. Applications:
   - Monthly portfolio monitoring: Regular tracking of Flow Rates helps identify trends in overall portfolio quality based on outstanding balances.
   - Strategic decision-making: Informs high-level credit policy and risk management strategy adjustments.
   - Performance benchmarking: Allows comparison of portfolio performance across different time periods or against industry standards.

5. Limitations:
   - Aggregation effects: Portfolio-level calculation may mask sub-segment trends or individual loan behaviors.

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

   |DPD Bucket|Outstanding Balance at 2021-12-31|Outstanding Balance at 2022-01-31|
   |----------|-----------------------------|-----------------------------
   |Current|68|70|
   |DPD 1-30|20|21|
   |DPD 31-60|13|14|
   |DPD 61-90|12|13|
   |DPD 90+|11|12|

   - NPL at 2021-12-31 (default defined as 90+ DPD) = 11/(68+20+13+12+11) = 11/124 = 8.87%
   - NPL at 2022-01-31 (default defined as 90+ DPD) = 12/(70+21+14+13+12) = 12/130 = 9.23%

4. Components:
   - Defaulted loans: Loans that have been classified as unlikely to be repaid, often after a specific period of delinquency.
   - Recoveries: Any amounts collected from defaulted loans through various recovery methods (e.g., collateral liquidation, debt collection).

5. Applications:
   - Financial reporting: Utilized in financial statements to provide a snapshot of portfolio risk at specific reporting dates.
   - Regulatory compliance: Often required by regulatory bodies for assessing a financial institution's stability.
   - Investor communication: Provides transparency to investors about the quality of the loan book.

6. Limitations:
   - Lagging indicator: NPL is a backward-looking metric and may not immediately reflect changes in portfolio quality.
   - Influenced by write-off policies: Different institutions may have varying policies on when to write off loans, affecting NPL comparability.

### Roll Rate / Recovery Rate

Similar to flow rate, roll rate is also a dynamic metric that measures the likelihood of loans transitioning from one delinquency status to another. The difference is that roll rate usually looks at the loans that are already in default and is calculated at the loan or installment level.

### Cost of Risk (CoR)

Cost of Risk (CoR) is an annualized metric that measures risk expressed as a percentage of the loan's outstanding balance. It is reported in financial statements and used in provisioning for credit loss. It will be covered in detail in [Estimating Long-term Impact from Short-term Outcome](../prediction/long_term_impact.md).

## Knowing vs. Doing

The above document provides a comprehensive overview of the key risk metrics commonly used in credit risk management. However, in practice, writing the code to calculate these metrics can be challenging. The best way to learn the precise definition and calculation of these metrics is to read the source code or write the code yourself. Also, the above definitions do not contain the exact logic on what's included and excluded in the calculation of these metrics, which largely depends on the risk management team's definition.
