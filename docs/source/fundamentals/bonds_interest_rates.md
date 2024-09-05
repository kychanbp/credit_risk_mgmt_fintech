# Fundamentals of Interest Rates

## TL;DR

- Interest rates are fundamentally about the time value of money and human impatience.
- The impatience theory of interest explains that interest rates reflect people's preference for present goods over future goods.
- Real interest rates account for inflation, while nominal rates don't.
- The time value of money formula is central to financial calculations, with five key variables: future value, present value, payment, number of periods, and rate.
- Common loan repayment plans include amortizing loans, equal principal payment loans, interest-only loans, balloon payment loans, and "tadpole" loans.
- Different repayment plans can result in varying total interest paid and monthly payment structures.
- Interest rates can be expressed as compound or simple interest rates.
- Converting between simple and compound interest rates involves using the time value of money formula and considering the specific repayment plan.

## Introduction

Have you ever wondered why there's an interest rate for a loan? Why do we need to pay interest on borrowed money? Can interest rates be negative? In this chapter, we will explore the fundamentals of interest rates and their relationship with the consumer credit industry.

*Disclaimer: I am not an economist. The following content is based on my understanding of the subject matter.*

## The Impatience Theory of Interest

> By definition, the rate of interest is the price of capital in terms of income, when both capital and income are measured in terms of the same unit, as, for instance, of money; or, what amounts to the same thing, the rate of interest is the excess above par which has to be paid for this year's money in terms of next year's money. - Irving Fisher [^1]

Irving Fisher explains the connection between capital, income, time, and rate of interest. "The rate of interest is the price of capital in terms of income" means that the interest rate reflects how much income (or return) you can expect to receive from your capital (or investment). "Measured in terms of the same unit" means that both capital and income are measured in the same unit, for example, money/dollars. "The rate of interest is the excess above par which has to be paid for this year's money in terms of next year's money" means that the interest rate is the premium you have to pay to obtain money today in exchange for repaying money in the future.

The key questions to be answered are:
- Why should there be an excess? Or why is there a rate of interest?
- What principles determine the amount of this excess?

### Theories

There are a number of theories that attempt to explain the rate of interest. I found the impatience theory of interest to be the most convincing (*Again, I am not an economist who follows interest rate theories closely*). For example, one theory suggests that the rate of interest depends on the amount of money in circulation. The more money in circulation, the lower the interest rate. The less money in circulation, the higher the interest rate. However, a plentiful money supply raises demand for loans just as much as it raises supply. The "feeling" probably comes from the observation that if bank reserves are low, banks will raise the interest rate to protect their reserves. But this is just relative scarcity from the bank's perspective, not an absolute scarcity.

Another theory is that interest is due to the productivity of capital--because 5% is what investments pay. But why does capital have a price in the first place? It is simply discounting future income, and during this process, we need to assume a rate of interest. It is a tautology.

The Agio Theory states that most of us prefer present goods over future goods of like kind and number, due to the "technical superiority of present over future goods" (Production is round-about, meaning it takes time. The same amount of input can yield a greater output in the future.), people having a natural preference for satisfying their needs and desires sooner rather than later, and uncertainty of the future. However, planting an apple tree today will yield the same or roughly the same amount of apples in a year.

The rate of interest is impatience crystallized into a market rate. It can be expressed in numbers as the premium that a person is willing to pay for this year's money over next year's money. Fundamentally, the reason for human impatience is that human life expectancy is limited. Also, humans lack the foresight to predict their future needs and wants. Those who have a high rate of impatience strive to acquire more present income at the cost of future income, tending to raise the interest rate. These are the borrowers, spenders, and sellers of assets. On the other hand, those who have a lower rate of impatience strive to acquire more future income at the cost of present income, tending to lower the interest rate. These are the lenders, savers, and investors.

There are three scenarios that can help you understand interest rates:

1. Increased impatience: the real interest rate increases and stock prices go down.
2. Increased optimism about future endowments: the real interest rate increases and stock prices go down. This is a bit counter-intuitive. The reason is that future endowments are expected to be higher, so why not spend the money today?
3. Wealth transfer from poor to rich: assuming the rich have a lower rate of impatience, the real interest rate decreases and stock prices go up.

### The Distinction between Real and Nominal Interest Rates

The nominal interest rate is the rate of interest in terms of money, without accounting for inflation. The real interest rate is the rate of interest in terms of goods, accounting for inflation. The relationship between the two is: $1+r = (1+i)/(1+\pi)$, where $r$ is the real interest rate, $i$ is the nominal interest rate, and $\pi$ is the inflation rate. 

The interest we usually talk about at work is the nominal interest rate.

### Further Reading

If you are interested in the theory of interest in mathematical terms, I recommend reading the note prepared by Jonathan Levin, an American economist and the 13th President of Stanford University, on [General Equilibrium](https://web.stanford.edu/~jdlevin/Econ%20202/General%20Equilibrium.pdf). In short, Fisher's theory of interest is a reduction to the general equilibrium model. I also found the [Financial Theory Course from Yale University](https://oyc.yale.edu/economics/econ-251) to be very useful.

### The Moral Aspect of Interest Rates

It's also interesting to mention some moral views on interest rates, as I have heard some of our colleagues express discomfort about charging interest.

> The most hated sort [of wealth-getting], and with the greatest reason, is usury, which makes a gain out of money itself, and not from the natural use of it. For money was intended to be used in exchange, but not to increase at interest. - Aristotle, Politics

> "But love your enemies, do good to them, and lend to them without expecting to get anything back." - Luke 6:35, Bible

> "Those who consume interest cannot stand [on the Day of Resurrection] except as one stands who is being beaten by Satan into insanity. That is because they say, 'Trade is [just] like interest.'" - Quran 2:275, Islam

> "You shall not charge interest on loans to your brother, interest on money, interest on food, interest on anything that is lent for interest. You may charge a foreigner interest, but you may not charge your brother interest." - Deuteronomy 23:19-20, Judaism

According to Fisher, interest is just a price of impatience. Also, the nominal interest rate is irrelevant. The real interest rate can be negative, challenging the idea that all interest is inherently exploitative.

## The Computations Behind Time Value of Money Formula -- fv, pmt, nper, pv and rate

Most financial professionals are familiar with the concept of the time value of money and the respective formulas to derive future value, present value, rate, etc. While Excel, Google Sheets, or financial calculators offer convenient functions, not everyone knows what equation is being solved and how it is solved.

The core equation is the following:

$$fv + pv \cdot (1+r)^{nper} + pmt \cdot (1+r \cdot w) \cdot \frac{(1+r)^{nper}-1}{r}=0$$

where $fv$ is the future value, $pv$ is the present value, $pmt$ is the payment, $nper$ is the number of periods, $r$ is the rate, and $w$ is the type of payment (0 for end of period, 1 for beginning of period). The sign of $fv$ is the opposite of $pv$ and $pmt$.

Moving $fv$ to the right side of the equation, the first term on the left is the future value of the present value. The second term is the future value of a series of regular equal payments ([Annuity](https://en.wikipedia.org/wiki/Annuity)). Since there are 5 variables, we can expect to have 5 corresponding formulas to solve for each variable:

- `FV(rate, number_of_periods, payment_amount, [present_value], [end_or_beginning])`: solving for future value is straightforward (move all other terms except $fv$ to the right side of the equation).
- `PV(rate, number_of_periods, payment_amount, [future_value], [end_or_beginning])`: solving for present value is straightforward (move all other terms except $pv$ to the right side of the equation).
- `PMT(rate, number_of_periods, present_value, [future_value], [end_or_beginning])`: solving for payment is straightforward (move all other terms except $pmt$ to the right side of the equation).

Solving for $nper$ and $r$ is more complicated. Let's start with $nper$: `NPER(rate, payment_amount, present_value, [future_value], [end_or_beginning])`. Let $z$ = $pmt \cdot (1+r \cdot w)/r$. Grouping terms involving $(1 + r)^{nper}$, we have:

$$\begin{aligned}
    fv - z + \left(pv + z\right) \cdot (1 + r)^{nper} &= 0 \\
    nper &= \frac{\log\left(\frac{z - fv}{pv + z}\right)}{\log(1 + r)}
\end{aligned}$$

The `RATE` formula is the most complicated. When using the RATE function in Excel, there is an argument called "guess". Most of us will just leave it as default or even not understand why there is such a thing. It looks impossible to write the equation with $r$ on one side. To find the root of this non-linear equation, we use the Newton-Raphson method. The formula is: 

$$x_{n+1} = x_n - \frac{g(x_n)}{g'(x_n)}$$
until a sufficiently precise value, that is $g_{n+1} - g_n < \epsilon$, is reached.

![Newton Method](newton_method.png)

We start with our initial guess $x_n$. Then the tangent line at $x=x_n$ intercepts the x-axis at $x_{n+1}$, which is a better approximation of the root. The slope of the tangent line is $g'(x_n) = \frac{g(x_n)}{x_n - x_{n+1}}$. Solving for $x_{n+1}$, we have $x_{n+1} = x_n - \frac{g(x_n)}{g'(x_n)}$. If the difference between $x_{n+1}$ and $x_n$ is less than a certain threshold, we stop the iteration.

Similar mechanics apply to the `IRR(cashflow_amounts, [rate_guess])` function.

## Types of Repayment Plans

### Amortizing Loan (等额本息)

The word "amortizing" comes from the Latin word "mortis", meaning death. In the context of a loan, it means that the loan will be paid off in equal installments over a period of time. The amortizing loan is user-friendly as the monthly payment is fixed, making it easier to budget and plan.

Consider a loan of $10,000 with a monthly interest rate of 3% and a tenure of 12 months. The repayment plan is as follows:

| Period # | Payment Amount | Principal Amount | Interest Amount | Balance Owed |
|----------|----------------|-------------------|-----------------|--------------|
| 1        | 1,004.62       | 704.62            | 300.00          | 9,295.38     |
| 2        | 1,004.62       | 725.76            | 278.86          | 8,569.62     |
| 3        | 1,004.62       | 747.53            | 257.09          | 7,822.09     |
| 4        | 1,004.62       | 769.96            | 234.66          | 7,052.13     |
| 5        | 1,004.62       | 793.06            | 211.56          | 6,259.07     |
| 6        | 1,004.62       | 816.85            | 187.77          | 5,442.22     |
| 7        | 1,004.62       | 841.35            | 163.27          | 4,600.87     |
| 8        | 1,004.62       | 866.59            | 138.03          | 3,734.28     |
| 9        | 1,004.62       | 892.59            | 112.03          | 2,841.69     |
| 10       | 1,004.62       | 919.37            | 85.25           | 1,922.32     |
| 11       | 1,004.62       | 946.95            | 57.67           | 975.37       |
| 12       | 1,004.63       | 975.37            | 29.26           | 0.00         |

The key concept of interest is that interest is accrued on the remaining balance of the loan. The remaining balance at month 0 is $10,000$. The interest for month 1 is $10,000 * 3\% = 300$. The remaining balance at month 1 is $9,295.38$. The interest for month 2 is $9,295.38 * 3\% = 278.86$, and so on.

To calculate the monthly payment, we can calculate using the Annuity formula, $pmt = \frac{pv \cdot r}{1-(1+r)^{-nper}}$. If you need more information about the formula, please refer to the [wikipedia page](https://en.wikipedia.org/wiki/Annuity).

### Equal Principal Payment Loan (等额本金)

Consider the same loan as above, but the repayment plan is as follows:

| Period # | Payment Amount | Principal Amount | Interest Amount | Balance Owed |
|----------|----------------|-------------------|-----------------|--------------|
| 1        | $1,133.33      | $833.33           | $300.00         | $9,166.67    |
| 2        | $1,108.33      | $833.33           | $275.00         | $8,333.34    |
| 3        | $1,083.33      | $833.33           | $250.00         | $7,500.01    |
| 4        | $1,058.33      | $833.33           | $225.00         | $6,666.68    |
| 5        | $1,033.33      | $833.33           | $200.00         | $5,833.35    |
| 6        | $1,008.33      | $833.33           | $175.00         | $5,000.02    |
| 7        | $983.33        | $833.33           | $150.00         | $4,166.69    |
| 8        | $958.33        | $833.33           | $125.00         | $3,333.36    |
| 9        | $933.33        | $833.33           | $100.00         | $2,500.03    |
| 10       | $908.33        | $833.33           | $75.00          | $1,666.70    |
| 11       | $883.33        | $833.33           | $50.00          | $833.37      |
| 12       | $858.37        | $833.37           | $25.00          | $0.00        |

As the name suggests, the principal payment is equal in each period. Similarly, the interest is accrued on the remaining balance of the loan. The interest for month 1 is $10,000 * 3\% = 300$. The remaining balance at month 1 is $10,000 - 833.33 = 9,166.67$. The interest for month 2 is $9,166.67 * 3\% = 275.00$, and so on.

### Interest-Only Loan (先息后本)

Consider a loan of $10,000$ with a monthly interest rate of 3% and a tenure of 12 months. The interest-only period is months 1 to 11. The repayment plan is as follows:

| Period # | Payment Amount | Principal Amount | Interest Amount | Balance Owed |
|----------|----------------|-------------------|-----------------|--------------|
| 1        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 2        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 3        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 4        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 5        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 6        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 7        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 8        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 9        | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 10       | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 11       | $300.00        | $0.00             | $300.00         | $10,000.00   |
| 12       | $10,300.00     | $10,000.00        | $300.00         | $0.00        |

### Balloon Payment Loan (气球贷)

It is similar to the interest-only loan. The purpose is to defer the principal payment to the end of the loan tenure. Usually, it will be advertised as "a 5-year loan with a 10-year repayment plan". In the first 5 years, the borrower only needs to pay the monthly payment equivalent to a 10-year amortizing loan. However, the borrower needs to pay the remaining principal at the end.

### "Tadpole Loan" (蝌蚪贷)

It is the reverse of the balloon payment loan. The borrower needs to pay a large portion of the principal in the early period, and the remaining principal plus the interest for the latter period. This kind of repayment plan is used in, for example, Indonesia where there is regulatory pressure on lowering the interest rate.

This also reminds us that given the same loan amount and tenure, the interest rate can be different in different repayment plans because of the different timing of the principal payments. We will discuss more on this in the next section.

### Comparison of Repayment Plans

|Types|Total Interest Paid|Total Amount Paid|Monthly Payment Range|Monthly Payment Trend|
|-----|-------------------|-----------------|---------------------|---------------------|
|Amortizing Loan| 2055.45 | 12055.45 | 1004.62 | Same|
|Equal Principal Payment Loan| 1950.00 | 11950.00 |~850-1133| Decreasing|
|Interest-Only Loan| 3600.00 | 13600.00 | 300, 10300 | Flat then sudden increase|
|Balloon Payment Loan| N.A. | N.A. | N.A. | Flat then sudden increase|
|Tadpole Loan| N.A. | N.A. | N.A. | Large in the beginning then decreasing|

If the principal is paid off earlier, the total interest paid is less. 

Colleagues in the consumer credit industry may be confused about why the repayment plan affects the interest rate (e.g., in Tadpole Loan). This confusion likely stems from our familiarity with deriving payment amounts from interest rates. However, even when the total interest paid remains constant, different repayment plans can yield different interest rates. For instance, if the total interest paid in an "Equal Principal Payment Loan" matches that of an "Amortizing Loan" at 1950, the "Amortizing Loan" interest rate (2.85%) is actually lower than the "Equal Principal Payment Loan" rate (3%). This may seem counterintuitive, as we typically associate earlier principal repayment with less total interest paid. In the "Equal Principal Payment Loan," the borrower does indeed pay off the principal earlier, so shouldn't this result in a lower interest rate? The key is understanding that the interest rate is calculated based on the loan's remaining balance. If a borrower pays off the principal earlier but the total interest paid remains the same, the interest rate must necessarily be higher to compensate for the reduced time the lender holds the full principal.

## Commonly Used Interest Rate Metrics

Of all the variations of interest rates, they fundamentally boil down to the difference between compounded and simple interest rates, and the period of time interest is accrued.

### Compounded Rate of Interest

*Terms: Effective Interest Rate (EIR)* 

We need to use Time Value of Money Formula to calculate the compounded rate of interest.

### Simple Rate of Interest

*Terms: Simple Interest Rate, Nominal Interest Rate, Annual Percentage Rate (APR)*

- Simple Interest Rate (Nominal Interest Rate) per period $n$: $r = \text{Interest}/\text{Principal}$
- Annual Percentage Rate (APR): $r = \text{Interest}/\text{Principal} / \text{days} \cdot 365$

### Conversion from Simple Interest Rate to Compounded Interest Rate

To calculate the compounded rate of interest, we need to know the cash flow (payment) of each period, the principal, and the tenure. The cash flow is influenced by the repayment plan and the simple rate of interest. Typically, if the loan contract stipulates the simple rate of interest, the repayment plan is amortizing, as the interest payment is fixed and based on the principal.

The cash flow in each period is equal to $CF = (PV/n + PV \cdot r)$, given that the payment is fixed.
We can then use the Annuity formula to solve for the rate: $PV = CF \cdot \frac{1-(1+r)^{-n}}{r}$.

It's worth noting that as $n$ (the tenure) increases, the effective interest rate may decrease. Consider a scenario where $n$ increases from 10,000 to 10,001; the $CF$ remains almost unchanged. Consequently, the second term of the equation must change very little as $n$ increases, resulting in a decrease in the effective interest rate.

## References

[^1]: Fisher, Irving. The ‘Impatience Theory’ of Interest; a Study of the Causes Determining the Rate of Interest ... Bologna, Nicola Zanichelli, 1911. http://archive.org/details/cu31924013755909.
