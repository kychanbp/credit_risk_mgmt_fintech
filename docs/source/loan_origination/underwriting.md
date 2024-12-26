# Underwriting (WIP)

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

---

## Viewing Underwriting as a RL Problem

For a detailed discussion of reinforcement learning in credit risk management, see [Decision Making](../fundamentals/decision_making.md).

|Component|Description|
|---------|-----------|
|Objective|Maximize the long-term cumulative profitability of the loan portfolio while maintaining acceptable risk levels|
|Reward Signal|The realized profit or loss from approved loans, including interest income, fees, and credit losses|
|State Space|Applicant characteristics (demographics, financials, credit history) and risk assessment metrics (application score, bureau data)|
|Action Space|Lending decisions (approve/reject) and loan parameters (credit limit, interest rate, tenure)|
|Policy|A decision-making framework that maps applicant states to lending actions|

### Trial-and-Error Search

The underwriting process involves significant amount of trial-and-error search. Since new applicants have no relationship with the company, it is more "clean" to test new underwriting criteria on them compared to existing customers.

While there are theoretically infinite possible underwriting criteria to evaluate, effective search requires a systematic approach guided by data analysis, historical performance, and competitive intelligence. Similar to gradient descent optimization in mathematics, successful underwriting policy development relies on building intuition about promising directions to explore. This intuition comes from deep domain expertise and experience analyzing lending outcomes - skills that are challenging to codify or teach directly.

## Typical Analysis Patterns
