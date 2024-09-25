# Estimating the Response to Interventions (WIP)

**Date:** September 2024

**Last Update:** September 2024

## Causation vs Association

In credit risk management, distinguishing between causation and association is crucial, as teams make decisions and take actions (interventions) that can alter the system and distribution. While association indicates a relationship between variables, causation implies that one variable directly influences another. This distinction is fundamental when estimating the response to interventions.

Although association can provide valuable insights, it is insufficient for making informed decisions about interventions in credit risk management for several reasons:

1. Spurious Correlations: Associations can be misleading. For instance, ice cream sales and drownings might correlate, but both are influenced by warm weather. In credit risk, the number of credit cards a person has might correlate with default likelihood, but this could be due to factors like income or financial literacy, not a direct cause-effect relationship.

2. Reverse Causality: Associations don't indicate the direction of causality. For example, a positive association between credit utilization and default risk could mean that lower utilization reduces default risk, or that people at lower risk of default tend to use less of their available credit.

3. Confounding Variables: Associations may not account for confounding variables that influence both the predictor and the outcome. For instance, the association between loan amount and default risk might be confounded by factors like income.

4. Limited Predictive Power: While associations can be useful for prediction under stable conditions, they may fail when interventions change the underlying system or distribution. For example, a credit risk model might have strong predictive power for default risk, but it may not accurately predict the effect of a limit increase on default risk or for an unseen population.

5. Inability to Inform Interventions: Associations alone cannot tell us how a system will respond to interventions. Knowing that high debt-to-income ratios are associated with higher default rates doesn't necessarily mean that helping customers reduce their debt-to-income ratio will lower default rates.

6. Lack of Counterfactual Reasoning: Associations don't allow for counterfactual thinking, which is crucial for understanding the potential outcomes of different interventions. We can't use associations to answer "what if" questions about alternative actions. For example, what if we offer a higher interest rate to customers, will it increase profit?

7. Time-Dependent Relationships: Associations may change over time or under different circumstances, limiting their usefulness for long-term decision-making or in new contexts.

Relying solely on associations for decision-making in credit risk management can lead to actions that appear logical but may be misleading or even counterproductive. Consider the following scenarios:

1. Credit Card Ownership: A negative association between the number of credit cards and default risk might suggest offering higher credit limits to customers with multiple cards. However, this could inadvertently increase their repayment burden, potentially leading to financial stress.

2. Credit Utilization: Due to reverse causality, we might offer higher credit limits to customers with high utilization, believing it will reduce default risk by lowering the utilization rate. In reality, these customers might be less likely to repay, and increasing their limit could exacerbate the problem.

3. Risk Assessment: We may be overly optimistic in offering credit limits to customers predicted to have low default risk based on their current financial snapshot. However, this assessment might not account for how their risk profile changes under a higher limit, potentially resulting in significantly increased risk.

These examples illustrate the importance of understanding causal relationships, rather than mere associations, when making decisions in credit risk management. Failure to do so can lead to unintended consequences and increased financial risk for both the lender and the borrower.

Judea Pearl, in his seminal work "The Book of Why," emphasizes the importance of causal reasoning in understanding and predicting the effects of interventions. He introduces the concept of the "Ladder of Causation," which consists of three levels:

1. Association (Seeing): This is the most basic level, where we observe correlations between variables. For example, we might notice that customers with higher credit scores tend to have lower default rates.

2. Intervention (Doing): This level involves predicting the effects of deliberate actions or interventions. In credit risk management, this could be estimating the impact of offering a higher credit limit on the likelihood of loan repayment.

3. Counterfactuals (Imagining): The highest level of causal reasoning, involving the ability to reason about what would have happened if we had acted differently in the past. For instance, would a customer who defaulted have repaid their loan if we had offered them a different repayment plan?

Traditional statistical methods often operate at the first level, while truly understanding the impact of interventions requires ascending to the second and third levels. This ascent is not always straightforward in observational studies, which are common in credit risk management due to ethical and practical constraints on experimentation. This is why the scientific community developed the field of Causal Inference, which provides tools and methodologies to bridge the gap between association and causation, enabling more informed and effective decision-making in complex domains like credit risk management.

## Fundamental Problem of Causal Inference

The Fundamental Problem of Causal Inference, first articulated by statistician Donald Rubin, is a core concept in causal inference that highlights the impossibility of observing the same unit under different treatment conditions simultaneously. This problem is fundamental because it applies to all causal questions and forms the basis for many challenges in causal inference.

Key aspects of the Fundamental Problem of Causal Inference include:

1. Counterfactuals: For any given unit (e.g., an individual, a company), we can only observe one potential outcome - the outcome under the treatment they actually received. We cannot observe what would have happened if they had received a different treatment. This unobserved outcome is called the counterfactual.

2. Missing Data Problem: Because we can't observe all potential outcomes for each unit, causal inference is essentially a missing data problem. We're always missing at least one potential outcome for each unit.

   Here's a table example to illustrate this missing data problem:

   | Customer | Received Credit Limit Increase | Outcome if Increased | Outcome if Not Increased |
   |----------|--------------------------------|-----------------------|--------------------------|
   | A        | Yes                            | Default               | ?                        |
   | B        | No                             | ?                     | No Default               |
   | C        | Yes                            | No Default            | ?                        |
   | D        | No                             | ?                     | Default                  |

   In this table, '?' represents the unobserved (counterfactual) outcome. We can never know what would have happened to Customer A if they hadn't received a credit limit increase, or what would have happened to Customer B if they had.

3. Assumptions: All methods for causal inference rely on assumptions to bridge the gap created by the Fundamental Problem. Common assumptions include:
   - Stable Unit Treatment Value Assumption (SUTVA): The treatment of one unit doesn't affect the outcomes of others.
   - Ignorability: Treatment assignment is independent of potential outcomes, given observed covariates.
   - Positivity: Every unit has a non-zero probability of receiving each treatment.

It's important to note that all solutions to the Fundamental Problem of Causal Inference are essentially effective methods to impute the '?' in our missing data table. These methods, such as propensity score matching, difference-in-differences, instrumental variables, and randomized controlled trials, aim to estimate what would have happened in the counterfactual scenario. While these methods can't perfectly solve the missing data problem, they provide rigorous approaches to estimate causal effects under certain assumptions.

## Causal Models

Causal models provide frameworks for understanding and estimating causal relationships. In the field of causal inference, two primary frameworks have emerged: the Potential Outcomes Framework and Structural Causal Models. These frameworks offer different perspectives and tools for addressing causal questions, each with its own strengths and applications.

The existence of two frameworks in causal inference is not a contradiction but rather a complementary approach to understanding causality. Here's why we have these two frameworks:

1. Different Perspectives:
   - The Potential Outcomes Framework focuses on comparing potential outcomes under different treatments.
   - Structural Causal Models emphasize the underlying mechanisms and relationships between variables.

2. Complementary Strengths:
   - Potential Outcomes are particularly useful for estimating average treatment effects and are well-suited for experimental designs.
   - Structural Causal Models excel in representing complex systems and are powerful for answering counterfactual questions.

Understanding both frameworks provides researchers and practitioners with a richer toolkit for addressing causal questions. In many cases, insights from both frameworks can be combined to provide a more comprehensive understanding of causal relationships.

### Potential Outcomes Framework

### Structural Causal Models

## Treatment Effect

ITE: Individual Treatment Effect

CATE: Conditional Average Treatment Effect

ATE: Average Treatment Effect

Why the best estimator for the CATE is also the best estimator for the ITE?

## Randomized Controlled Trials

## No Free Lunch in Causal Inference

https://p-hunermund.com/2018/06/09/no-free-lunch-in-causal-inference/

## Estimating Treatment Effect If Randomized Controlled Trials Are Available

## Estimating Treatment Effect If Randomized Controlled Trials Are Not Available

- Matching
- Difference-in-Differences
- Instrumental Variables

## State-of-the-Art Approaches and Decision Flow

https://econml.azurewebsites.net/spec/flowchart.html

## Applications in Credit Risk Management

### Adjustment of Limit and Pricing

### Non Performing Account Management

## Paradox

- Simpson's Paradox

## References

### Theoretical Foundations

### Practical References

### For General Readers

### Packages for Causal Inference

- [CausalML](https://github.com/uber/causalml)
- [EconML](https://github.com/microsoft/EconML)
- [DoWhy](https://github.com/microsoft/dowhy)
