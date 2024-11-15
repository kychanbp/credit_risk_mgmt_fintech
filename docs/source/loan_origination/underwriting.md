# Underwriting (WIP)

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
