# Underwriting or Loan Origination

## Introduction

Underwriting, also known as loan origination, is the process of assessing a borrower's creditworthiness and establishing the terms of a loan during the initial stages of the loan process. The specific scope of underwriting can differ among lenders. For instance, some may consider loans originated within the first month as part of the origination process, while treating subsequent loans as post-loan management. Others might delineate the process based on the breakeven point in a user's lifecycle.

The core objective of underwriting is to maximize the number of users and loans originated, while simultaneously minimizing cumulative losses throughout the user lifecycle. While profitability is the ultimate goal, the number of users and loans originated serves as an early indicator of the underwriting policy's success. Although the loan amount per user/loan is also a significant factor, it is secondary to the number of users/loans originated. Provided that the limit offered is competitive and user take-up rates remain consistent, the limit can be increased later during the post-loan management phase.

## Viewing Underwriting Using Decision Making Framework

- **Action Space:** The set of possible actions, such as user selection (approving or rejecting a loan application) and loan parameters (setting the credit limit, interest rate, and loan tenure).
- **State Space:** The range of potential outcomes, including default or non-default within a defined observation period.
- **Probability:** The likelihood of each outcome occurring.
- **Outcome and Utility:** The resulting profit or loss from approved loans, encompassing interest income, fees, and credit losses.

## The Iterative Process of Underwriting

### Initial Policy

Upon launching a new product, the initial underwriting policy is typically established using expert knowledge and competitor analysis. This initial policy often takes the form of a simple, rule-based system, designed to gather preliminary data and assess market viability.

This "initial policy" evolves into the current policy through iterative refinement. By evaluating the performance of each policy version, we can determine its effectiveness in achieving the desired objectives.

### Evaluation

Policy improvements can generally be categorized into three areas:

1. Increasing the overall approval rate while maintaining a constant level of risk and average loan amount per user/loan.
2. Reducing risk while maintaining a constant approval rate and average loan amount per user/loan.
3. Increasing the average loan amount per user/loan while maintaining a constant approval rate and level of risk.

To analyze policy performance, we follow the structure outlined in [General Data Analysis Techniques](../data_analysis.md):

1. **Clearly define the objective:** Does the current policy outperform the previous policy in any of the three areas mentioned above?
2. **Clearly define the metrics:**
    1. Risk: First Payment Default (FPD), 3-Month First Payment Default (3FPD), Vintage Analysis
    2. Approval rate: Number of approved users divided by the total number of unique applications.
    3. Loan amount per user/loan: Average loan amount per approved user/loan.
    4. For a comprehensive list of metrics, refer to [Commonly Used Risk Metrics](../key_objective/risk_metrics.md).
3. **Hypothesis:**
    1. During policy evaluation, various scenarios (sub-problems) may arise. For example, risk may increase, the approval rate may decrease, or the loan amount per user/loan may decrease.
    2. For each identified sub-problem, formulate a hypothesis and validate it using the methods described in [General Data Analysis Techniques](../data_analysis.md).

### Iteration and Testing

Following the identification of the root cause of policy performance-whether an improvement or a degradation-the policy can be iterated upon. This involves either reinforcing the promising direction or pivoting to a new approach.

Underwriting policies often employ a layered structure: first, a series of hard rejection rules are applied; then, user segmentation is performed; and finally, model-based segmentation is used. Subsequently, each user is assigned a risk tier. The credit limit is then determined based on the assigned risk tier, as well as other factors such as the user's income.

Policy iteration is often guided by the following questions and observations that arise during the evaluation phase:

- How can we improve our risk model to increase approval rates and/or reduce risk?
- What additional data sources can we leverage to enhance our risk model?
- Could relaxing our hard rejection rules lead to a higher approval rate?
- How can we refine user segmentation to provide more tailored experiences for different user groups?
- Would increasing the credit limit improve user conversion rates?
- Would offering longer loan tenures increase user conversion rates and/or the average loan amount per user?
- How would adjusting interest rates impact user conversion rates and risk?

After the policy is iterated, it is tested again using the same process as the initial policy evaluation.

## User Segmentation in Credit Risk Policy

### Terminology

- **Segmentation**: Segmentation, in the context of credit risk policy, refers to the process of dividing a population into distinct, business-relevant groups based on a limited set of easily interpretable characteristics. This is often done prior to or in conjunction with the development of more complex credit scoring models that utilize a larger set of variables.

### Why

The decision-making framework involves several key components:

- **Action:** The range of choices available to the decision-maker (e.g., approve or reject a loan application).
- **States of the World:** The potential outcomes or scenarios that could occur (e.g., a borrower defaults or does not default).
- **Outcome:** The consequences of a specific action given a particular state of the world (e.g., a gain of 1000 or a loss of 1000).
- **Probability:** The likelihood of each state of the world occurring.
- **Utility:** A measure of the desirability of each outcome, which in credit risk is often the financial result of the decision.

Segmentation enhances this framework by:

- **Expanding the action space:** By considering population characteristics, decision-makers can implement a wider array of actions, such as offering varied credit limits, interest rates, and fees.
- **Improving state of the world estimation:** Instead of applying a single probability of default to all applicants (especially in the absence of a model), segmentation allows for more precise estimations for specific borrower groups. This is particularly useful when there is heterogeneity in the population. Segmentation can also improve the estimation of other states of the world, such as credit usage.
- **Improving utility:** By tailoring actions and improving the accuracy of risk and usage predictions for each segment, lenders can optimize pricing, manage risk more effectively, and ultimately enhance profitability.

**Counter-argument: Why segment if a model already exists?**

- **The Bias-Variance Trade-off:** A global model, while exhibiting lower variance, tends to be more biased. Conversely, a local model offers greater precision but suffers from higher variance. Essentially, a global model performs adequately on average but may falter with specific borrower groups, whereas a local model excels within a particular segment but may not generalize well. This is often due to heterogeneity in risk profiles, usage patterns, and data availability.
- **Global vs. Local Models:** The effectiveness of a single global model versus multiple local models hinges on the degree of heterogeneity within the population. When heterogeneity is pronounced, local models may be more effective. However, local models may struggle to capture inter-segment relationships as well as a unified model. Furthermore, they can be susceptible to data sparsity issues.

My perspective: If a model could truly learn the underlying mechanisms of the system (a "World Model"), it should inherently account for heterogeneity, rendering further segmentation unnecessary. The need for segmentation suggests that current models are not fully capturing these underlying mechanisms and therefore require expert-driven segmentation.

Another argument for segmentation is that different segments warrant different treatments. While this is a valid point, a sufficiently robust model should inherently be able to capture these nuances, thereby negating the need for additional segmentation.

### How

Given that segmentation aims to address population heterogeneity and that tailored treatment of distinct segments can enhance decision-making utility, the subsequent question is: how can we identify this heterogeneity?

In the context of credit risk policy, we primarily focus on two dimensions: risk and usage. To uncover heterogeneity, we can employ the following approach:

1. Identify the most important predictors of both risk and usage. (For example, the top features in the global model.)
2. Formulate hypotheses regarding potential segments. Examples include:
    1. Credit history length (e.g., thin-file vs. thick-file)
    2. Demographic factors (e.g., age, location, income)
    3. Loan purpose
    4. Acquisition channel
3. Compute summary statistics (e.g., mean, median, standard deviation, percentiles) for key predictors (e.g., income, credit score, debt-to-income ratio).
4. Analyze for significant differences: Are there notable variations in the distributions and summary statistics of key variables across the hypothesized segments?

More data-driven methods, such as clustering and decision trees, can also be used to identify segments. I will elaborate on the decision tree method, as it is more commonly used in the industry.

The primary objective when splitting a node in a decision tree is to generate child nodes that exhibit greater homogeneity, or "purity," with respect to the target variable compared to their parent node. Essentially, the goal is to create groups that are more differentiated in terms of the outcome being predicted (e.g., default risk or product usage). This differentiation is quantified using metrics such as Gini impurity, entropy, or information gain. The splitting process is constrained by stopping criteria, including maximum tree depth, minimum samples required to split a node, and minimum samples required in a leaf node. Furthermore, expert knowledge can be integrated to influence the splitting process by predefining specific splits.

### When

In my experience, segmentation is most valuable when a robust risk model is either absent or inadequate, and when the sample size is sufficiently large. This situation often occurs during the early stages of a product launch. Following the launch, data collection begins, but the initial dataset may be insufficient to train multiple local models effectively. At this stage, a reasonably effective global model is likely in place, and the benefits of segmentation diminish due to increased policy complexity and reduced testing advantages. Optimizing a policy for the average customer is generally simpler than optimizing for multiple specific segments. However, in later phases, once the policy has stabilized and the sample size has grown substantially, further segmentation can become instrumental in enhancing policy utility.

Segmentation is an iterative process; a simple initial segmentation can be refined based on subsequent testing results.

## Conclusion

This document outlines the underwriting process, emphasizing its iterative nature and the importance of user segmentation. Underwriting involves assessing creditworthiness and setting loan terms, with the goal of maximizing user and loan origination while minimizing losses. The process is viewed through a decision-making framework, considering actions, states, probabilities, and outcomes. The initial policy, often rule-based, evolves through evaluation and iteration, focusing on improving approval rates, reducing risk, and increasing loan amounts. User segmentation is crucial, especially when robust risk models are lacking, allowing for tailored actions and improved risk estimation. Segmentation is an iterative process, starting simple and refining based on testing results.




