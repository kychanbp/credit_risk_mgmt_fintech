# Defining Risk Tiers

Risk tiers are a ruler to classify borrowers into different risk levels. For a ruler, we need to consider the scale, range, and granularity. For example, if we want to measure the height of a person, we can use centimeters as the scale, and the range can be from 0 to 300 cm, and the granularity can be 1 cm.

What, then, should be the appropriate **scale** for measuring risk? As discussed in [Commonly Used Risk Metrics](../key_objective/risk_metrics.md), numerous metrics exist to quantify risk. However, when evaluating borrowers, it is crucial to adopt a unified metric rather than switching between different metrics—for example, using First Payment Default (FPD) for new users and 3-month cumulative Days Past Due (DPD) for existing users. The ultimate metric should consistently be the **annualized cost of risk**. All other risk metrics employed in credit decision-making are intermediate measures that ultimately map to this unified metric. We rely on these intermediate metrics primarily because they are easier to access and simpler to calculate.

Regarding the **range** of the scale, it is important to ensure that it remains **expandable**. For example, initially defining risk tiers simply as 'Low', 'Medium', and 'High' might seem adequate. However, if future analysis identifies a distinct 'Very High' risk segment or necessitates subdividing the 'Medium' category into finer segments, a rigid categorical structure becomes challenging to adapt without redefining the entire system. In contrast, a numerical scale allows for easier addition of new tiers or adjustments to existing boundaries as needed.

The **granularity** of the scale relates directly to sensitivity toward profit and loss. Businesses with high margins may be less sensitive to incremental changes, such as an additional 1% cost of risk, whereas low-margin businesses may be more sensitive. Generally, it is advisable to start with greater granularity, as risk tiers can always be combined later if the treatment for multiple tiers is identical.



