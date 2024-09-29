Estimating the Response to Interventions (WIP)
==============================================

**Date:** September 2024

**Last Update:** September 2024

TL;DR
-----

You can safely ignore the following sections:

- The bias of using observational data to estimate causal effects
- Causal Models
- Estimating Treatment Effect If Randomized Controlled Trials Are Not Available
- State-of-the-Art Approaches and Decision Flow
- Paradox

Causation vs Association
------------------------

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

Fundamental Problem of Causal Inference
---------------------------------------

The Fundamental Problem of Causal Inference, first articulated by statistician Donald Rubin, is a core concept in causal inference that highlights the impossibility of observing the same unit under different treatment conditions simultaneously. This problem is fundamental because it applies to all causal questions and forms the basis for many challenges in causal inference.

Key aspects of the Fundamental Problem of Causal Inference include:

1. Counterfactuals: For any given unit (e.g., an individual, a company), we can only observe one potential outcome - the outcome under the treatment they actually received. We cannot observe what would have happened if they had received a different treatment. This unobserved outcome is called the counterfactual.

2. Missing Data Problem: Because we can't observe all potential outcomes for each unit, causal inference is essentially a missing data problem. We're always missing at least one potential outcome for each unit.

   Here's a table example to illustrate this missing data problem:

   +----------+--------------------------------+------------------------+----------------------------+
   | Customer | Received Credit Limit Increase | Outcome if Increased   | Outcome if Not Increased   |
   +==========+================================+========================+============================+
   | A        | Yes                            | Default                | ?                          |
   +----------+--------------------------------+------------------------+----------------------------+
   | B        | No                             | ?                      | No Default                 |
   +----------+--------------------------------+------------------------+----------------------------+
   | C        | Yes                            | No Default             | ?                          |
   +----------+--------------------------------+------------------------+----------------------------+
   | D        | No                             | ?                      | Default                    |
   +----------+--------------------------------+------------------------+----------------------------+

   In this table, '?' represents the unobserved (counterfactual) outcome. We can never know what would have happened to Customer A if they hadn't received a credit limit increase, or what would have happened to Customer B if they had.

It's important to note that all solutions to the Fundamental Problem of Causal Inference are essentially effective methods to impute the '?' in our missing data table. These methods, such as propensity score matching, difference-in-differences, instrumental variables, and randomized controlled trials, aim to estimate what would have happened in the counterfactual scenario. While these methods can't perfectly solve the missing data problem, they provide rigorous approaches to estimate causal effects under certain assumptions.

Causal Models
-------------

Causal models provide frameworks for understanding and estimating causal relationships. In the field of causal inference, two primary frameworks have emerged: the Potential Outcomes Framework and Structural Causal Models. These frameworks offer different perspectives and tools for addressing causal questions, each with its own strengths and applications.

The existence of two frameworks in causal inference is not a contradiction but rather a complementary approach to understanding causality. Here's why we have these two frameworks:

1. Different Perspectives:

   - The Potential Outcomes Framework focuses on comparing potential outcomes under different treatments.
   - Structural Causal Models emphasize the underlying mechanisms and relationships between variables.

2. Complementary Strengths:
   - Potential Outcomes are particularly useful for estimating average treatment effects and are well-suited for experimental designs.
   - Structural Causal Models excel in representing complex systems and are powerful for answering counterfactual questions.

Understanding both frameworks provides researchers and practitioners with a richer toolkit for addressing causal questions. In many cases, insights from both frameworks can be combined to provide a more comprehensive understanding of causal relationships.

Potential Outcomes Framework
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Potential Outcomes Framework, also known as the Rubin Causal Model, is a fundamental approach in causal inference. Developed by Donald Rubin, this framework provides a way to define and estimate causal effects using the concept of potential outcomes.

Key components of the Potential Outcomes Framework include:

1. Potential Outcomes: For each unit and each possible treatment, there is a potential outcome. For example, in credit risk management:

   - :math:`Y(1)`: The outcome if a customer receives a credit limit increase
   - :math:`Y(0)`: The outcome if the same customer does not receive a credit limit increase

2. Treatment Assignment: Denoted as :math:`T`, where :math:`T=1` if the unit receives the treatment and :math:`T=0` otherwise.

3. Observed Outcome: :math:`Y = TY(1) + (1-T)Y(0)`

4. Causal Effect: Defined as the difference between potential outcomes, e.g., :math:`Y(1) - Y(0)`

5. Average Treatment Effect (ATE): :math:`E[Y(1) - Y(0)]`

The framework relies on several key assumptions:

- Stable Unit Treatment Value Assumption (SUTVA): The potential outcomes for any unit do not vary with the treatments assigned to other units.
- Ignorability: Treatment assignment is independent of potential outcomes, given observed covariates.
- Positivity: Every unit has a non-zero probability of receiving each treatment.

The Bias of Using Observational Data to Estimate Causal Effects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The potential outcomes framework provides a foundation for understanding the bias inherent in using observational data to estimate causal effects. Let's explore this concept using the example of college attendance and its impact on mental ability.

Consider the Naive Estimator:

.. math::

   \hat{\delta} = E_N[y_i|d_i = 1] - E_N[y_i|d_i=0]

Where:

- :math:`N` is the sample size from observational data
- :math:`y_i` is the realized treatment effect for individual :math:`i`
- :math:`d_i = 1` indicates the individual received treatment (attended college)
- :math:`d_i = 0` indicates the individual did not receive treatment

This estimator suggests that the treatment effect can be calculated by subtracting the average mental ability of non-college attendees from that of college attendees. However, this approach is naive and potentially biased.

The Average Treatment Effect (ATE) is defined as:

.. math::

   E[\delta]=E[Y^1] - E[Y^0]

Where :math:`Y^1` and :math:`Y^0` are random variables representing outcomes with and without treatment, respectively. Let :math:`\pi` be the proportion of the population receiving treatment. We can expand the ATE as:

.. math::

   E[\delta]=\{\pi E[Y^1|D=1]+(1-\pi)E[Y^1|D=0]\} - \{\pi E[Y^0|D=1]+(1-\pi)E[Y^0|D=0]\}

For a large sample size :math:`N`:

- :math:`E_N[y_i|d_i = 1] \to E[Y^1|D=1]`
- :math:`E_N[y_i|d_i = 0] \to E[Y^0|D=0]`
- :math:`E_N[d_i] \to \pi`

However, :math:`E[Y^1|D=0]` and :math:`E[Y^0|D=1]` remain unknown counterfactuals, making it unclear whether the Naive Estimator equals the ATE.

To understand when they differ, let's rearrange the ATE formula:

Let :math:`E[\delta]=e`, :math:`E[Y^1|D=1]=a`, :math:`E[Y^1|D=0]=b`, :math:`E[Y^0|D=1]=c`, and :math:`E[Y^0|D=0] = d`. 

After algebraic manipulation, we arrive at:

.. math::

   a - d = e + (c - d) + (1 - \pi)[(a - c) - (b - d)]

The Naive Estimator :math:`(a - d)` differs from the true ATE :math:`(e)` when:

1. Baseline bias :math:`(c - d) \neq 0`:
   :math:`E[Y^0|D=1] - E[Y^0|D=0]` represents the inherent difference between those who attend college and those who don't, regardless of treatment. Those who attend college might have been smarter in the first place.

2. Differential treatment effect bias :math:`[(a - c) - (b - d)] \neq 0`:
   :math:`(E[Y^1|D=1] - E[Y^0|D=1]) - (E[Y^1|D=0] - E[Y^0|D=0]) = E[\delta|D=1] - E[\delta|D=0]` 
   This represents the difference in treatment effect between the two groups. The mental ability of those who attend college may increase more than it would for those who did not attend college if they had instead attended college

These biases highlight the challenges in using observational data for causal inference and underscore the importance of careful consideration of potential confounding factors in such analyses.

*Originally from my blog post* `here <https://www.zhizhi-gewu.com/naive-estimator-using-obsevational-data-and-when-it-differs-from/>`_

Structural Causal Models
~~~~~~~~~~~~~~~~~~~~~~~~

Structural Causal Models (SCMs), also known as Structural Equation Models (SEMs), provide a framework for representing and analyzing causal relationships between variables. Developed by Judea Pearl and others, SCMs offer a powerful tool for understanding complex causal systems.

Key components of Structural Causal Models include:

1. Variables: Endogenous (determined within the model) and exogenous (determined outside the model).

2. Functional Relationships: Equations that describe how variables are determined by other variables.

3. Directed Acyclic Graph (DAG): A graphical representation of the causal relationships between variables.

4. Structural Equations: Mathematical expressions that define each endogenous variable as a function of its direct causes and an error term.

5. do-operator: A mathematical tool for intervening on variables and computing counterfactuals.

Example in credit risk management:

Variables:

- credit_limit: The maximum amount of credit extended to a customer
- utilization: The proportion of credit limit being used
- bill_amt: The total amount billed to the customer
- tenure: The duration of the loan (loan tenure)
- acard: Application scorecard (a tool used to evaluate credit applications)
- risk: The level of credit risk associated with the customer
- bcard: Behavioral scorecard (a tool used to assess ongoing customer behavior)

Causal Relationships:
(Represented as directed edges in the DAG)

.. mermaid::

   graph TD
       acard[acard] --> credit_limit[credit_limit]
       acard --> risk[risk]
       bcard[bcard] --> risk
       bill_amt[bill_amt] --> risk
       credit_limit --> utilization[utilization]
       credit_limit --> bill_amt
       utilization --> bill_amt
       utilization --> bcard
       tenure[tenure] --> bill_amt

Functional Relationships:
(Using placeholder functions to represent the relationships)

- :math:`credit\_limit = f_{credit\_limit}(acard)`
- :math:`risk = f_{risk}(acard, bcard, bill\_amt)`
- :math:`utilization = f_{utilization}(credit\_limit)`
- :math:`bill\_amt = f_{bill\_amt}(credit\_limit, utilization, tenure)`
- :math:`bcard = f_{bcard}(utilization)`

These functional relationships form the structural equations of the SCM, defining how each variable is determined by its direct causes. In this representation, we've omitted the error terms (ε) for simplicity, though in practice, they would be included to account for unobserved factors.

SCMs incorporate important graph structures and criteria that aid in identifying and estimating causal effects:

1. Mediator Junction (A -> B -> C): Represents a chain of causality where A affects C through B. Controlling for B blocks the causal path from A to C.

2. Fork Junction (A <- B -> C): Represents a common cause B for both A and C. Controlling for B removes the spurious association between A and C (deconfounding).

3. Collider Junction (A -> C <- B): Represents a common effect C of both A and B. Controlling for C can create a spurious correlation between A and B.

Key Implication:

- Controlling for variables is not always beneficial and can sometimes introduce bias.

Advantages of SCMs:

1. Explicit representation of causal mechanisms
2. Capability to answer a wide range of causal queries
3. Seamless integration of domain knowledge into the model
4. Ability to reason about interventions and counterfactuals

Challenges:

1. Reliance on strong assumptions about the causal structure
2. Increasing complexity for large-scale systems
3. Sensitivity to model misspecification

Treatment Effect
----------------

In this section, we will explore various types of treatment effects and their definitions. These concepts are crucial for understanding the impact of interventions in causal inference:

1. ITE (Individual Treatment Effect):

   - Measures the causal effect of a treatment on a specific individual.
   - Represents the difference in potential outcomes for an individual under treatment vs. control.
   - Challenging to estimate directly due to the fundamental problem of causal inference.
   - Formula: :math:`ITE_i = Y_i(1) - Y_i(0)`
     Where :math:`Y_i(1)` is the outcome for individual i if treated, and :math:`Y_i(0)` if not treated.

2. CATE (Conditional Average Treatment Effect):

   - The average treatment effect for a subgroup with specific characteristics.
   - Useful for understanding heterogeneous treatment effects across different populations.
   - Often estimated using machine learning methods for personalized predictions.
   - Formula: :math:`CATE(X) = E[Y(1) - Y(0) | X]`
     Where X represents the conditioning variables.

3. ATE (Average Treatment Effect):

   - The average causal effect of a treatment across the entire population.
   - Represents the expected difference in outcomes between treated and control groups.
   - Commonly used in randomized controlled trials and observational studies.
   - Formula: :math:`ATE = E[Y(1) - Y(0)]`

4. LATE (Local Average Treatment Effect):

   - The average treatment effect for compliers in instrumental variable settings.
   - Applicable when there's imperfect compliance with treatment assignment.
   - Provides insights into the effect of treatment on those influenced by the instrument.
   - Formula: :math:`LATE = E[Y(1) - Y(0) | compliers]`

5. ATT (Average Treatment Effect on the Treated):

   - The average effect of treatment specifically for those who received the treatment.
   - Useful when treatment effects may differ between treated and untreated populations.
   - Often relevant in policy evaluation where we want to know the impact on those who actually received an intervention.
   - Formula: :math:`ATT = E[Y(1) - Y(0) | T = 1]`
     Where :math:`T = 1` indicates the treated group.

6. QTE (Quantile Treatment Effect):
   - Measures the treatment effect at different quantiles of the outcome distribution.
   - Useful for understanding how treatment impacts vary across the outcome spectrum.
   - Provides a more comprehensive view of treatment effects beyond averages.
   - Formula: :math:`QTE(\tau) = Q_{Y(1)}(\tau) - Q_{Y(0)}(\tau)`
     Where :math:`Q_{Y(1)}(\tau)` and :math:`Q_{Y(0)}(\tau)` are the :math:`\tau`-th quantiles of the potential outcomes under treatment and control, respectively.

In industry applications, the Individual Treatment Effect (ITE) is the most crucial treatment effect to measure, as it allows for personalized interventions tailored to individuals, such as in determining credit limits, pricing, and voucher allocations. However, the ITE is not directly observable. Instead, we typically estimate the Conditional Average Treatment Effect (CATE) based on a set of features X, and use this to make personalized treatment recommendations for groups of individuals sharing similar feature values.

Interestingly, the best estimator for the CATE is also the best estimator for the ITE. This relationship can be demonstrated mathematically:

.. math::

   \text{CATE}(x) = \mathbb{E}[Y(1) - Y(0) \mid X = x] = \mathbb{E}[\text{ITE} \mid X = x]

Since CATE is the expected value of ITE given certain covariates, any error in estimating ITE (:math:`\widehat{\text{ITE}} - \text{ITE}`) will propagate into the CATE estimation. Mathematically:

.. math::

   \text{CATE}(x) = \mathbb{E}[\widehat{\text{ITE}} \mid X = x]

Minimizing the estimation error in ITE (:math:`\widehat{\text{ITE}} - \text{ITE}`) directly reduces the error in CATE estimation.

Randomized Controlled Trials
----------------------------

We have discussed the bias inherent in using observational data to estimate causal effects. Now, let's demonstrate how randomized controlled trials (RCTs) can provide unbiased estimates of these effects. Recall that the bias in observational data stems from two main sources:

1. Baseline bias: :math:`E[Y^0|D=1] - E[Y^0|D=0] \neq 0`
   This occurs when the control outcomes differ between treatment and control groups.

2. Differential treatment effect bias: :math:`E[\delta|D=1] - E[\delta|D=0] \neq 0`
   This arises when the treatment effect varies between those who receive the treatment and those who don't.

RCTs address these biases by ensuring that the potential outcomes :math:`(Y^1, Y^0)` are independent of the treatment assignment :math:`D`. This independence is achieved through randomization, which balances both observed and unobserved confounding factors across treatment and control groups.

By design, RCTs create comparable groups, eliminating baseline differences and ensuring that any observed differences in outcomes can be attributed to the treatment effect. This makes RCTs the gold standard for causal inference, providing a robust foundation for estimating treatment effects across various domains, including credit risk management.

RCTs and A/B Testing are commonly used in consumer lending to estimate the effect of a treatment on an outcome, such as the effect of a limit increase on default risk.

Estimating Treatment Effect If Randomized Controlled Trials Are Available
-------------------------------------------------------------------------

The Unreasonable Effectiveness of Linear Regression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Frisch-Waugh-Lovell Theorem (FWL):

Uplift Models
~~~~~~~~~~~~~

Estimating Treatment Effect If Randomized Controlled Trials Are Not Available
-----------------------------------------------------------------------------

- Matching
- Difference-in-Differences
- Instrumental Variables

State-of-the-Art Approaches and Decision Flow
---------------------------------------------

There are many approaches to estimate treatment effect, the following is a flow chart to choose the most appropriate method: `Treatment Effect Estimation Flowchart from EconML <https://econml.azurewebsites.net/spec/flowchart.html>`_

Applications in Credit Risk Management
--------------------------------------

Adjustment of Limit and Pricing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Non Performing Account Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Paradox
-------

Paradoxes challenge our intuition and inspire us to think more critically about our assumptions and methodologies. I have collected a few paradoxes that is relevant to causal inference.

Simpson's Paradox
~~~~~~~~~~~~~~~~~

Simpson's Paradox is a statistical phenomenon where a trend appears in several groups of data but disappears or reverses when these groups are combined. This paradox highlights the importance of considering confounding variables and the potential pitfalls of aggregating data without careful consideration of underlying factors.

Let's consider an example in the context of credit risk management:

Suppose a bank is analyzing the effectiveness of a new credit counseling program on reducing default rates. They look at the data for two customer segments: high-risk and low-risk borrowers.

+------------+---------+-------------------+----------+--------------+
| Risk Level | Program | Total Customers   | Defaults | Default Rate |
+============+=========+===================+==========+==============+
| High Risk  | Yes     | 1000              | 200      | 20%          |
+------------+---------+-------------------+----------+--------------+
| High Risk  | No      | 500               | 150      | 30%          |
+------------+---------+-------------------+----------+--------------+
| Low Risk   | Yes     | 500               | 25       | 5%           |
+------------+---------+-------------------+----------+--------------+
| Low Risk   | No      | 1000              | 40       | 4%           |
+------------+---------+-------------------+----------+--------------+

Looking at each risk level separately, the program appears to be effective:

- For high-risk customers, the default rate decreased from 30% to 20%.
- For low-risk customers, the default rate increased slightly from 4% to 5%, but this could be due to random variation.

However, if we aggregate the data:

+---------+-------------------+----------+--------------+
| Program | Total Customers   | Defaults | Default Rate |
+=========+===================+==========+==============+
| Yes     | 1500              | 225      | 15%          |
+---------+-------------------+----------+--------------+
| No      | 1500              | 190      | 12.67%       |
+---------+-------------------+----------+--------------+

Surprisingly, the overall default rate is higher for those who participated in the program (15%) compared to those who didn't (12.67%). This is Simpson's Paradox in action.

The paradox arises because the program was disproportionately applied to high-risk customers. While it improved outcomes within each group, the aggregate result appears to show the opposite effect due to the different group sizes and baseline risk levels.

This example demonstrates why it's crucial to:

1. Consider confounding variables (in this case, the risk level of customers).
2. Analyze data at appropriate levels of granularity.
3. Be cautious when interpreting aggregated data, especially when dealing with heterogeneous groups.

In credit risk management, Simpson's Paradox underscores the importance of stratified analysis and the need to control for relevant factors when assessing the effectiveness of interventions or policies. It also highlights the potential dangers of making decisions based solely on aggregate data without considering underlying group differences.

Berkson's Paradox
~~~~~~~~~~~~~~~~~

Lord's Paradox
~~~~~~~~~~~~~~

References
----------

Theoretical Foundations
~~~~~~~~~~~~~~~~~~~~~~~

- Morgan, Stephen L., and Christopher Winship. Counterfactuals and Causal Inference Methods and Principles for Social Research. Second edition. New York, NY: Cambridge University Press, 2015.

Practical References
~~~~~~~~~~~~~~~~~~~~

- Facure, Matheus. Causal Inference in Python: Applying Causal Inference in the Tech Industry. Beijing Boston Farnham Sebastopol Tokyo: O'Reilly Media, 2023.

For General Readers
~~~~~~~~~~~~~~~~~~~

- Pearl, Judea, and Dana Mackenzie. The Book of Why: The New Science of Cause and Effect. First trade paperback edition. New York: Basic Books, 2020.

Packages for Causal Inference
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- `CausalML <https://github.com/uber/causalml>`_
- `EconML <https://github.com/microsoft/EconML>`_
- `DoWhy <https://github.com/microsoft/dowhy>`_