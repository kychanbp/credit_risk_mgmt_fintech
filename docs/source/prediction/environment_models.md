# Creating Models of the Environment

Disclaimer: The author's primary expertise is in credit risk management rather than machine learning. The theoretical content in this chapter represents personal notes that he found interesting and wishes to share with others.

## Why Does Supervised Learning Work?

In essence, "Low Training Error + Sufficient Data Relative to Model Complexity $\implies$ Low Test Error".

Supervised learning must work on the SAME distribution.

---

Note: Readers primarily interested in practical applications may safely skip the proofs in this section. These proofs are included for completeness and deeper theoretical understanding.

### Key Concepts

- **Training Error** ($\text{Train}_S(f)$): The error of a model $f$ evaluated on the training dataset $S$.

- **Test Error** ($\text{Test}_D(f)$): The expected error of $f$ on new, unseen data drawn from the same distribution $D$.

- **Hypothesis Class** ($\mathcal{F}$): The set of all models $f$ that the learning algorithm can choose from.

- **Sample Size** ($|S|$): The number of training examples.

- **Confidence Level** ($1 - \delta$): The probability that the bound holds true.

- **Degrees of Freedom**: Informally, the number of parameters or complexity of the model class $\mathcal{F}$.

### Mathematical Formulation

#### Generalization Error Bound

The generalization error bound is given by:

$$
\Pr_{S \sim D^{|S|}} \left[ \text{Test}_D(f) - \text{Train}_S(f) \leq \sqrt{\frac{\log |\mathcal{F}| + \log \frac{1}{\delta}}{|S|}} \quad \text{for all} \quad f \in \mathcal{F} \right] > 1 - \delta
$$

### Interpretation:

With probability at least $1 - \delta$, the difference between test and training error is bounded by:

$$
\sqrt{\frac{\log |\mathcal{F}| + \log \frac{1}{\delta}}{|S|}}
$$

### Implications:

1. **Sample Size Effect**
   - Larger training sample size $|S|$ results in:
     - Tighter error bounds
     - Test error closer to training error
2. **Model Complexity Effect** 
   - Larger hypothesis class size $|\mathcal{F}|$ leads to:
     - Looser error bounds
     - Potentially larger gap between test and training errors

### Proof

The proof follows these key steps:

1. **Setup**
   - Let $f \in \mathcal{F}$ be any hypothesis
   - Let $S$ be a training set of size $|S|$ drawn i.i.d. from distribution $D$
   - Let $\text{Test}_D(f)$ and $\text{Train}_S(f)$ be the test and training errors

2. **Hoeffding's Inequality**
   For a single hypothesis $f$:
   $$
   \Pr_S[|\text{Test}_D(f) - \text{Train}_S(f)| > \epsilon] \leq 2e^{-2|S|\epsilon^2}
   $$

   **Note on [Hoeffding's Inequality](https://en.wikipedia.org/wiki/Hoeffding%27s_inequality):**

   In probability theory, Hoeffding's inequality provides an upper bound on the probability that the sum of independent random variables deviates from its expected value. 

3. **Union Bound**
   - Apply to all hypotheses $f \in \mathcal{F}$:
   $$
   \Pr_S[\exists f \in \mathcal{F}: |\text{Test}_D(f) - \text{Train}_S(f)| > \epsilon] \leq |\mathcal{F}| \cdot 2e^{-2|S|\epsilon^2}
   $$

4. **Set Failure Probability**
   - Let right side equal $\delta$:
   $$
   |\mathcal{F}| \cdot 2e^{-2|S|\epsilon^2} = \delta
   $$

5. **Solve for $\epsilon$**

   $$
   \begin{align*}
   e^{-2|S|\epsilon^2} &= \frac{\delta}{2|\mathcal{F}|} \\
   -2|S|\epsilon^2 &= \ln(\frac{\delta}{2|\mathcal{F}|}) \\
   \epsilon^2 &= \frac{\ln(2|\mathcal{F}|/\delta)}{2|S|} \\
   \epsilon &= \sqrt{\frac{\ln(2|\mathcal{F}|/\delta)}{2|S|}}
   \end{align*}
   $$

6. **Final Result**

   Since $\Pr_S[\exists f \in \mathcal{F}: |\text{Test}_D(f) - \text{Train}_S(f)| > \epsilon] \leq \delta$, it follows that the probability that all hypotheses satisfy the inequality is at least $1-\delta$: $\Pr_S[\forall f \in \mathcal{F}: |\text{Test}_D(f) - \text{Train}_S(f)| \leq \epsilon] \geq 1 - \delta$.

   Thus, with probability at least $1-\delta$, the difference between test and training error is bounded by:

   $$
   |\text{Test}_D(f) - \text{Train}_S(f)| \leq \sqrt{\frac{\log |\mathcal{F}| + \log \frac{1}{\delta}}{|S|}}
   $$

This proves that with high probability, the difference between test and training error is bounded by a term that depends on the model complexity ($|\mathcal{F}|$) and training set size ($|S|$).

In other words, **supervised learning _must_ work on the _SAME_ distribution** for these bounds to hold.

## The Bias-Complexity Tradeoff

When selecting the hypothesis class $\mathcal{F}$, we face a tradeoff between a larger, more complex class that is likely to have a small approximation error, and a more restrictive, simpler class that ensures a small estimation error. **Prior knowledge about the problem constrains the hypothesis class.** For example, in credit risk modeling, if we know that the relationship between a borrower's debt-to-income ratio and default probability is generally monotonic (higher ratios correspond to higher default risk), we can restrict our hypothesis class to monotonic functions only. This prior knowledge eliminates many possible hypotheses that would violate this relationship, reducing model complexity while maintaining or improving real-world performance.

**Theorem. (No-Free-Lunch)** Let $A$ be any learning algorithm for binary classification with respect to the 0–1 loss over a domain $\mathcal{X}$. Let $m$ be any number smaller than $|\mathcal{X}|/2$, representing a training set size. Then, there exists a distribution $\mathcal{D}$ over $\mathcal{X} \times \{0,1\}$ such that:

1. There exists a function $f : \mathcal{X} \rightarrow \{0,1\}$ with $L_{\mathcal{D}}(f) = 0$.
2. With probability of at least $1/7$ over the choice of $S \sim \mathcal{D}^m$, we have that $L_{\mathcal{D}}(A(S)) \geq 1/8$.

This theorem states that for every learner, there exists a task on which it fails, even though that task can be successfully learned by another learner.

While a comprehensive discussion of model selection techniques is beyond the scope of this section, several key methods deserve mention:

- AIC (Akaike Information Criterion): Balances model fit against complexity by penalizing the number of parameters
- BIC (Bayesian Information Criterion): Similar to AIC but with a stronger penalty for complexity
- MDL (Minimum Description Length): Selects models based on their ability to compress the data efficiently
- VC Dimension (Vapnik–Chervonenkis Dimension): Measures the capacity of a model class to fit arbitrary data
- CV (Cross-Validation): Empirically estimates model performance on unseen data through repeated train-test splits

For a detailed treatment of these methods, readers should consult the references provided below.

Among these approaches, cross-validation has become the de facto standard when sufficient data is available. However, it's crucial to note that proper cross-validation requires setting aside validation data before performing any data preprocessing or feature selection steps. While this principle may seem straightforward, it is frequently overlooked in practice, potentially leading to optimistic bias in performance estimates.

## Feature Selection and Manipulation

### Feature Selection

Our discussion so far has focused on abstract models of learning, where the prior knowledge utilized by the learner is fully encoded by the choice of the hypothesis class $\mathcal{F}$. However, another crucial modeling choice exists: how do we represent the instance space $\mathcal{X}$? While there are common techniques for feature selection and learning, the No-Free-Lunch theorem still applies. Here are some widely used approaches:

- Filtering: Select the $k$ features with the highest scores (based on any chosen metric of interest) independently of other features.
- Forward Greedy Selection: Start with an empty feature set and iteratively add features that yield the highest performance gain.
- Backward Elimination: Start with all features and iteratively remove features whose removal results in the highest performance gain.

Constraining the hypothesis class $\mathcal{F}$ to use a small subset of features can reduce estimation error and thus prevent overfitting. Additionally, in practical applications, obtaining and processing each feature often incurs computational and financial costs that must be considered.

### Feature Manipulation

Feature manipulation or normalization transforms features into a new space, often to improve learning algorithm performance. When considering feature representation, we should relate the choice to both the learning algorithm and our prior knowledge about the problem.

A common example in credit risk modeling is the Weight of Evidence (WOE) transformation. WOE converts categorical and continuous variables into a standardized scale by comparing the proportion of good and bad credit outcomes in each category or bin. While WOE can improve model performance by handling non-linear relationships and outliers, its widespread adoption in the financial industry, in the author's opinion, is primarily driven by regulatory requirements for model interpretability and transparency. The clear relationship between WOE values and default rates makes it easier to explain model decisions to stakeholders and regulators, even though other transformations may achieve similar or better predictive performance.

The use of WOE involves a transformation of data that requires binning. A binning process should follow these principles:

- Missing values should be grouped separately
- Each bin should contain at least 5% of the total observations
- No bin should have zero good or bad outcomes
- Establish a monotonic relationship between independent variable and target variable

The Weight of Evidence (WOE) for a bin is calculated as:

$$
WOE_i = \ln\left(\frac{\%\text{ of Good Customers}_i}{\%\text{ of Bad Customers}_i}\right)
$$

Where:

- $i$ represents a specific bin
- $\%\text{ of Good Customers}_i = \frac{\text{Number of Good Customers in bin }i}{\text{Total Number of Good Customers}}$
- $\%\text{ of Bad Customers}_i = \frac{\text{Number of Bad Customers in bin }i}{\text{Total Number of Bad Customers}}$

The WOE transformation has several useful properties:

1. It creates a linear relationship with the log odds of the target variable when using logistic regression
2. The values are symmetric around zero:
   - WOE = 0 indicates the proportion of good and bad customers is equal
   - WOE > 0 indicates more good than bad customers
   - WOE < 0 indicates more bad than good customers
3. Monotonicity: The WOE values are monotonic with respect to the independent variable
4. Using proportions instead of counts helps avoid the influence of sample size on the transformation
5. The logarithmic nature accentuates the difference between the proportions of good and bad, highlighting bins with strong discriminative power

A related measure, Information Value (IV), can be used to assess the overall predictive power of a variable:

$$
IV = \sum_{i=1}^{n} (\%\text{Good}_i - \%\text{Bad}_i) \times WOE_i
$$

Where $n$ is the total number of bins.

IV is closely related to the concept of [Kullback-Leibler Divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence), which measures the difference between two probability distributions:

$$
D_{\text{KL}}(P \| Q) = \sum_{i} P(x_i) \ln \left( \frac{P(x_i)}{Q(x_i)} \right)
$$

$$
\text{IV} = \sum_{i} (P_i - Q_i) \times \ln \left( \frac{P_i}{Q_i} \right)
$$

The only difference between IV and KLD is the weighting factor.

## Commonly Used Models

This section highlights the commonly used models in credit risk modeling rather than delving into their technical details. Once we have established that supervised learning works and sufficient data is available, model selection becomes primarily a matter of empirical performance comparison. The most prevalent models in credit risk assessment include:

- Logistic Regression: A traditional but robust choice, offering high interpretability
- XGBoost: Currently the most widely adopted model in practice, known for its performance
- LightGBM: Another powerful gradient boosting framework gaining popularity

Based on industry experience, XGBoost has emerged as the dominant choice due to its balance of performance, scalability, and relative interpretability.

## Unstructured Data

As the meme humorously points out, "The entire finance industry runs on Excel." However, relying solely on structured tabular data has significant limitations when modeling customer behavior:

1. **Loss of Event Order**: Classical tabular models aggregate data over time periods, losing the temporal sequence of actions. Two customers with identical transactions in different orders would appear the same to the model, despite potentially meaningful differences in their behavior patterns.

2. **Ignoring Temporal Interactions**: These models fail to capture how events interact over time. For example, a large purchase followed by an unusual withdrawal could indicate different risk levels compared to the reverse sequence, but tabular aggregations would treat them identically.

3. **Independent Predictions**: Each prediction is made independently, without considering the sequence of past events. This prevents the model from identifying behavioral patterns that develop over time.

To address these limitations, incorporating unstructured and sequential data can provide additional insights beyond traditional tabular approaches. Sequential models can capture temporal dependencies and patterns that may be crucial for accurate risk assessment.

The field of learning from unstructured data continues to evolve rapidly, and industry adoption will take time. However, the author believes that the use of unstructured data will become increasingly prevalent in credit risk modeling.

## Reject Inference

A fundamental assumption in supervised learning is that the training and test data come from the same distribution. However, in credit risk modeling, we often face a significant challenge: we typically only have data from approved applications, not the entire applicant population. This creates what is known as **sample selection bias**, where our training data distribution differs from the true population distribution. This poses a particular challenge for policy-making, as we need to make decisions that will affect the entire population, not just the approved subset.

Reject inference comprises techniques developed to address this challenge by attempting to estimate model performance on the full population using only the approved sample data. These methods try to infer the likely outcomes for rejected applications based on patterns in the approved data. While promising in theory, implementing reject inference effectively requires careful consideration of assumptions and methodology. As this is an evolving area of practice, the author looks forward to exploring these techniques in greater depth in future work.

## Model Evaluation Checklist

When evaluating a credit risk model, use the following checklist to ensure the model is robust, compliant, and effective:

1. **Data Assessment**
   - **Data Quality**
     - Verify the accuracy and completeness of the data
     - Handle missing values and outliers appropriately
   - **Data Quantity**
     - Ensure sufficient sample size relative to model complexity
     - Confirm data representativeness of the target population
   - **Data Distribution**
     - Verify training and testing data come from the same distribution
     - Monitor for covariate shifts or changes in underlying data over time

2. **Feature Engineering**
   - **Relevance and Permissibility**
     - Include features that are relevant and permissible under regulatory guidelines
     - Exclude features that could introduce bias or violate privacy laws
   - **Transformation Techniques**
     - Apply appropriate transformations such as Weight of Evidence (WOE)
     - Ensure transformations maintain monotonic relationships with target variables
   - **Variable Selection**
     - Use Information Value (IV) or other metrics to assess predictive power
     - Remove low-performing variables to simplify the model and reduce overfitting

3. **Model Evaluation**
   - **Performance Metrics**
     - Evaluate using relevant metrics (e.g., AUC-ROC, KS Statistic, Gini Coefficient)
     - Assess performance across different customer segments
   - **Benchmarking**
     - Compare in-sample and out-of-sample performance
     - Compare performance across time periods
     - Compare against baseline models or industry standards
     - Analyze improvements over previous approaches

4. **Interpretability and Explainability**
   - **Transparency**
     - Ensure model decisions can be explained clearly
     - Provide insights into feature importance and influence
   - **Regulatory Compliance**
     - Meet explainability requirements per regulatory guidelines
     - Document rationale behind model choices and predictions

5. **Validation and Testing**
   - **Stress Testing**
     - Evaluate performance under various economic scenarios
   - **Sensitivity Analysis**
     - Analyze how input changes affect predictions

6. **Monitoring and Maintenance**
   - **Post-Deployment Monitoring**
     - Implement real-time performance monitoring
     - Track metrics to detect data drift or model degradation
   - **Periodic Review**
     - Schedule regular assumption and performance reviews
     - Update model based on new data or changing conditions

7. **Ethical and Legal Considerations**
   - **Fairness and Bias**
     - Assess for potential biases against protected groups
     - Implement bias mitigation strategies
   - **Privacy Compliance**
     - Ensure compliance with data protection regulations
     - Apply appropriate data anonymization

## Cycle of Model Development

Understanding that supervised learning must work on the SAME distribution, that the choice of hypothesis class $\mathcal{F}$ is crucial, and that feature representation influences model performance, we can derive the following development strategy:

| Data Amount | Prior Knowledge | Stage | Data Accumulation Strategy | Model Development Strategy |
|------------|----------------|--------|---------------------------|--------------------------|
| Limited | Without Prior Belief | Early Stage | • Random population sampling where feasible<br>• Use domain knowledge for representative sampling | • Focus on simple models<br>• Rapid iteration to validate assumptions |
| Limited | With Prior Belief | Early Stage | • Leverage external expertise<br>• Utilize internal knowledge<br>• Random population sampling where feasible | • Restrict hypothesis class based on prior beliefs<br>• Feature selection guided by domain expertise |
| Sufficient | Without Prior Belief | Mature Stage | • Systematic data collection across segments<br>• Comprehensive quality controls<br>• Active pursuit of new data sources | • Begin with interpretable models<br>• Increase complexity while monitoring performance |
| Sufficient | With Prior Belief | Mature Stage | • Strategically aligned data collection<br>• Rigorous quality standards | • Restrict hypothesis class based on knowledge<br>• Domain-driven feature engineering |

## References

- Shalev-Shwartz, Shai, and Shai Ben-David. Understanding Machine Learning: From Theory to Algorithms. New York: Cambridge university press, 2014.
- Hastie, Trevor, Robert Tibshirani, and Jerome H. Friedman. The Elements of Statistical Learning: Data Mining, Inference, and Prediction. Second edition. Springer Series in Statistics. New York, NY: Springer, 2017.
