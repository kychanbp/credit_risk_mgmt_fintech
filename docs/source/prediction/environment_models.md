# Creating Models of the Environment (WIP)

Disclaimer: The author is not a machine learning expert. His primary experience is in credit risk management. The theoretical part of this chapter is a note for himself which he found interesting and wants to share with others.

## Why Supervised Learning Works?

In short, "Low Training Error + Suffient Data Relative to Model Complexity $\implies$ Low Test Error". 

Supervised learning must work on the SAME distribution.

---

Note: Readers can safely skip the proofs in this section if they are primarily interested in practical applications. The proofs are included for completeness and deeper theoretical understanding.


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
   - Larger training sample size $|S|$ leads to:
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

In short, when choosing the hypothesis class $\mathcal{F}$, we face a tradeoff, between a larger, or more complex, class that is more likely to have a small approximation error, and a more restrictive, or simpler, class that would guarantee that the estimation error is small. **Prior knowledge about the problem restricts the hypothesis class.** For example, in credit risk modeling, if we know that the relationship between a borrower's debt-to-income ratio and default probability is generally monotonic (higher ratios lead to higher default risk), we can restrict our hypothesis class to monotonic functions only. This prior knowledge eliminates many possible hypotheses that would violate this relationship, reducing model complexity while maintaining or improving real-world performance.

**Theorem. (No-Free-Lunch)** Let $A$ be any learning algorithm for the task of binary classification with respect to the 0–1 loss over a domain $\mathcal{X}$. Let $m$ be any number smaller than $|\mathcal{X}|/2$, representing a training set size. Then, there exists a distribution $\mathcal{D}$ over $\mathcal{X} \times \{0,1\}$ such that:

1. There exists a function $f : \mathcal{X} \rightarrow \{0,1\}$ with $L_{\mathcal{D}}(f) = 0$.
2. With probability of at least $1/7$ over the choice of $S \sim \mathcal{D}^m$, we have that $L_{\mathcal{D}}(A(S)) \geq 1/8$.

This theorem states that for every learner, there exists a task on which it fails, even though that task can be successfully learned by another learner (I intentionally skipped the details explaination and proof here. For more details, please refer to the Reference section below).

## Feature Selection

So far, we have discussed abstract model of learning, in which the prior knowledge utilized by the learner is fully encoded by the choice of the hypothesis class $\mathcal{F}$. However, there is another modeling choice: how do we represent the instance space $\mathcal{X}$?

## Excels and Tabular Data

In the financial industry, we often deal with tabular data. This data typically comes in the form of spreadsheets or databases containing structured information like:

- Customer demographics (age, income, employment history)
- Transaction records (amounts, dates, types)
- Credit history (payment records, credit scores, defaults)
- Market data (prices, volumes, volatility)
- Risk metrics (VaR, exposure amounts, ratings)

The structured nature of this data makes it well-suited for traditional machine learning approaches, particularly for tasks like:

1. Credit risk assessment
2. Fraud detection
3. Customer segmentation

However, working with financial tabular data presents unique challenges including:

- Handling missing values
- Dealing with imbalanced classes (e.g., rare fraud cases)
- Managing temporal dependencies
- Ensuring data quality and consistency

## Commonly Used Models

The intention of this section is not to delve into the technical details of each model, but rather to highlight their practical limitations and considerations, as this training material is primarily targeted at risk management practitioners rather than data scientists.

### Logistic Regression

### XGBoost

### LightGBM

## Unstructured Data

## Model Evaluation Checklist

## References

- Shalev-Shwartz, Shai, and Shai Ben-David. Understanding Machine Learning: From Theory to Algorithms. New York: Cambridge university press, 2014.

