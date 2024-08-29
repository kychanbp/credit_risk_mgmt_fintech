# Fundamentals of Interest Rates (WIP)

## TL;DR

## Introduction

Have you ever wondered why there exists an interest rate for a loan? Why do we need to pay interest on borrowed money? (Can interest rates be negative?) In this chapter, we will explore the fundamentals of interest rates and their relationship with the consumer credit industry.

*Disclaimer: I am not an economist. The following content is based on my understanding of the subject matter.*

## The Impatience Theory of Interest

> By definition, the rate of interest is the price of capital in terms of income, when both capital and income are measured in terms of the same unit, as, for instance, of money; or, what amounts to the same thing, the rate of interest is the excess above par which has to be paid for this year's money in terms of next year's money. - Irving Fisher [^1]

The English is a bit archaic. Irving Fisher explains the connection between, capital, income, time, and rate of interest. "the rate of interest is the price of capital in terms of income" means that interest rate reflects how much income (or return) you can expect to receive from your capital (or investment). "measured in terms of the same unit" means that both capital and income are measured in the same unit, for example, money/dollars. "the rate of interest is the excess above par which has to be paid for this year's money in terms of next year's money" means that interest rate is the premium you have to pay to obtain money today in exchange for repaying money in the future.

The key questions to be answered are:
- Why should there be an excess? Or Why is there a rate of interest?
- What principals determine the amount of this excess?

### Theories

There are number of theories that attempt to explain the rate of interest. I found the impactience theory of interest to be the most convincing (*Again, I am not an economist who follows interest rate theories closely.*). For example, one of the theories is that the rate of interest depends on the amount of money in circulation. The more money in circulation, the lower the interest rate. The less money in circulation, the higher the interest rate. However, plentiful of money raises demand of loan just as much as it raises supply. The "feeling" probably comes from the observation that if bank reserve is low, bank will raise the interest rate to pretect the reserve. But, this is just relative scarcity from the bank's perspective, not an absolute scarcity. Another theory is that interest is due to productivity of capital--because 5% is what investments pay. But why the capital worths a price at the first place? It is simply discounting the future income, and during the process, we need to assume a rate of interest. It is a tautology. Agio Theory states that most of us prefer present goods over future goods of like kind and number, due to "technical superiority of present over future goods" (Production is round-about, meaning it takes time. The same amount of input can yield a greater output in the future.), people having a natural perference for satisfying their needs and desires sonner rather than latter, and uncertainty of the future. However, planting an apple tree today will yield the same/ rougly the same amount of apples in a year latter.

The rate of interest is impatience crystallized into a market rate. It can be expressed in numbers as the premium that a man is willing to pay for this year's money over next year's money. Fundamentally, the reason why human is impatience is that human life expectancy is limited. Also, huamn lacks the foresight to predict their future needs and wants. Those who, having a high rate of impatience, strive to acquire more present income, at the cost of future income, tend to raise interest rate. These are the borrowers, spenders, selling of assets.On the other hand, those who, having a lower rate of impatience, strive to acquire more future income at the cost of present income, tend to lower the interest rate. These are the lenders, the savers, the investors.

### The Distinction on Real and Nominal Interest Rate

## The Moral Aspect of Interest Rates

## Types of Repayment Plans

## Commonly Used Interest Rate Metrics

## The Computations Behind Time Value of Money Formula -- fv, pmt, nper, pv and rate

Most financial professionals are familiar with the concept of the time value of money and the respective formulas to derive the future value, present value, rate, etc. While Excel, Google Sheets, or financial calculators offer convenient functions, not every one of us knows what equation is being solved and how it is solved.

The core equation is the following:
$$fv + pv \cdot (1+r)^{nper} + pmt \cdot (1+r \cdot w) \cdot \frac{(1+r)^{nper}-1}{r}=0$$

where, $fv$ is the future value, $pv$ is the present value, $pmt$ is the payment, $nper$ is the number of periods, $r$ is the rate, and $w$ is the type of payment (0 for end of period, 1 for beginning of period). The sign of $fv$ is the opposite of $pv$ and $pmt$.

Moving $fv$ to the right side of the equation, the first term on the left is the future value of the present value. The second term is the future value of a series of regular equal payments ([Annuity](https://en.wikipedia.org/wiki/Annuity)). Since there are 5 variables, we can expect to have 5 corresponding formulas to solve for each variable:

- `FV(rate, number_of_periods, payment_amount, [present_value], [end_or_beginning])`: solving for future value is straightforward (move all other terms except $fv$ to the right side of the equation).
- `PV(rate, number_of_periods, payment_amount, [future_value], [end_or_beginning])`: solving for present value is straightforward (move all other terms except $pv$ to the right side of the equation).
- `PMT(rate, number_of_periods, present_value, [future_value], [end_or_beginning])`: solving for payment is straightforward (move all other terms except $pmt$ to the right side of the equation).

Solving for $nper$ and $r$ is more complicated. Let's start with $nper$: `NPER(rate, payment_amount, present_value, [future_value], [end_or_beginning])`. Let $z$ = $pmt \cdot (1+r \cdot w)/r$. Grouping terms involving $(1 + r)^{nper}$, then we have:
$$\begin{aligned}
    fv - z + \left(pv + z\right) \cdot (1 + r)^{nper} &= 0 \\
    nper &= \frac{\log\left(\frac{z - fv}{pv + z}\right)}{\log(1 + r)}
\end{aligned}$$

The `RATE` formula is the most complicated. When using the RATE function in Excel, there is an argument called guess. Most of us will just leave it as default or even do not understand why there is such a thing. It looks impossible to write the equation with $r$ on one side. To find the root of this non-linear equation, we use the Newton-Raphson method. The formula is: 

$$x_{n+1} = x_n - \frac{g(x_n)}{g'(x_n)}$$
until a sufficiently precise, that is $g_{n+1} - g_n < \epsilon$, is reached.

![Newton Method](newton_method.png)

We start with our initial guess $x_n$. Then the tangent line at $x=x_n$  intercepts the x-axis at $x_{n+1}$ which is a better approximation of the root. The slope of the tangent line is $g'(x_n) = \frac{g(x_n)}{x_n - x_{n+1}}$. Solving for $x_{n+1}$, we have $x_{n+1} = x_n - \frac{g(x_n)}{g'(x_n)}$. If the difference between $x_{n+1}$ and $x_n$ is less than a certain threshold, we stop the iteration.

## References

- [^1]: Fisher, Irving. The ‘Impatience Theory’ of Interest; a Study of the Causes Determining the Rate of Interest ... Bologna, Nicola Zanichelli, 1911. http://archive.org/details/cu31924013755909.
