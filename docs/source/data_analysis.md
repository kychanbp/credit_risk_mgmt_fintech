# General Data Analysis Techniques

This article presents my personal perspective on approaching data analysis. While there are many methodologies and best practices in the field, the following framework represents my thoughts on providing a structured approach to guide your analytical process. These views are based on my experience and should be taken as one practitioner's opinion rather than definitive guidance.

## Objective

The ultimate goal of data analysis is to act on the understanding generated from data. This is often referred to as generating "actionable insights." It's important to note that action does not always mean implementing something new—sometimes the appropriate action is maintaining the status quo.

The key questions we'll explore are:

- How to develop understanding of a problem/observation
- How to derive actions based on that understanding

## Understanding of a Problem/Observation

**The first step in developing understanding is to clearly and precisely state the problem.** This crucial yet often overlooked step challenges many analysts who struggle to articulate the problem they're trying to solve concisely. When asking colleagues or stakeholders to define the problem, you may find their explanations create more confusion than clarity. This highlights the importance of achieving alignment on the problem definition before proceeding with analysis. As an analyst, it's your responsibility to ensure the problem is defined clearly and precisely. Key questions to consider include:

- What is the context/background of the problem?
- What are the success criteria?
- What are the constraints?
- What is the scope of the problem?
- Who are the key stakeholders?

**The second step is to generate hypotheses that can help address the problem.** While commonly advised, the process of hypothesis generation is rarely discussed in detail. This skill is one of the most underrated yet valuable in the analytical process, as it directly impacts the effectiveness and efficiency of subsequent analysis. Consider an idealized scenario: if we had a superintelligent agent that could simulate any possibility instantaneously, there would be no need to constrain our hypothesis space. However, as human analysts with limited time and resources, we must be strategic in generating promising hypotheses that are both testable and likely to yield meaningful insights. While experience is valuable in hypothesis generation, time spent alone does not necessarily translate to better analytical skills. Rather, it's the quality of our analytical thinking and ability to learn from past analyses that helps us generate more effective hypotheses.

Several approaches can help generate promising hypotheses:

**Big Ideas:**

- Cultivate intellectual curiosity by asking "why" about things that interest you. Many people accept things at face value without questioning underlying mechanisms or assumptions. By consistently asking "why," you can develop deeper insights and uncover hidden patterns and relationships.
- Embrace interdisciplinary thinking. Problem-solving often requires drawing inspiration from seemingly unrelated domains. For example, concepts from reinforcement learning can inform credit policy optimization, while machine learning techniques can enhance portfolio management strategies. By studying diverse fields, you'll develop a richer mental toolkit and identify novel connections.
- Focus on fundamental principles and mental models. Knowledge can be viewed as a tree—from core concepts (roots), you can derive many specific applications (branches). By mastering foundational concepts and first principles, you'll be better equipped to understand and reason about new situations through extrapolation and analogy.

**Practical Techniques:**

- Bayesian reasoning: Pre-existing knowledge or analysis can inform your hypothesis generation. Reviewing past analyses helps identify promising hypotheses worth testing, as each piece of evidence should update your prior beliefs. For example, when tasked with expanding a stagnant Brazilian credit portfolio, reviewing historical analyses helped generate testable hypotheses that proved effective in driving portfolio growth.
- Causal Models: While each problem you face may be new, you've accumulated experiences that build your "World Model." Common sense indicates a strong causal model of the world—you don't need someone to tell you that income affects credit risk. To develop your causal model, consider the advice above. Once you have a causal model in mind (which can be imperfect), you can generate hypotheses by reasoning through the relationships in your model. For more information on causal models, see this {doc} `article </prediction/intervention_response>`.
- Learn from the best: One effective way to constrain the hypothesis space is to study successful practitioners (individuals or companies). Understanding not just what they do, but why they do it is crucial. Since industry leaders likely have years of experience, there is substantial evidence and data to observe. By applying Bayesian reasoning and causal models, you can adapt best practices to your context.
- Collective Wisdom: Problem-solving need not be solitary. Leveraging colleagues' experiences and insights through collaborative discussion can enhance hypothesis generation. Their unique perspectives, combined with Bayesian reasoning and causal models, can help identify promising angles you may have missed. While credit-sharing concerns sometimes create barriers to collaboration, fostering open knowledge exchange ultimately leads to better solutions.
- Maintain intellectual humility: During hypothesis generation, avoid strong preconceptions or biases. If you're already highly confident in a particular hypothesis, testing it provides little value. Similarly, be wary of confirmation bias—choosing hypotheses simply because you want them to be true, rather than having evidence suggesting they might be true. Remain open-minded and let the data guide your understanding.

**The final step in developing understanding is to test the hypotheses.** This is typically the most straightforward step, though data analysts often focus solely on this part without sufficient consideration of the previous steps. Two primary techniques are commonly used:

- Conditioning: This fundamental technique involves analyzing relationships by examining data subsets based on specific criteria. For example, to test whether income affects credit risk, you might segment customers into income brackets and compare default rates. While simple to implement, it's important to control for confounding variables and consider selection bias.
- A/B Testing: Also known as randomized controlled trials, this experimental technique involves randomly assigning subjects to treatment and control groups to measure causal effects. For instance, to evaluate a new marketing campaign's impact on credit risk, you would randomly split your customer base into groups receiving different versions of the campaign. Random assignment helps isolate the causal effect by controlling for both observed and unobserved confounding factors. However, proper implementation requires careful consideration of sample size, statistical power, and ethical implications.

**An effective data analyst will dedicate most of their time to the first two steps, with only a small portion spent on the final step.**

## Deriving Actions

Once you've developed a clear understanding through rigorous analysis and hypothesis testing, you should grasp the causal relationships between key variables and your defined success criteria. With this foundation, you can begin deriving actionable recommendations.

The key is to systematically evaluate potential actions based on their expected impact on target outcomes, considering both direct effects and potential unintended consequences. Focus on interventions that leverage the strongest causal relationships identified in your analysis while remaining mindful of practical constraints and implementation feasibility considered in step one. Remember that actions can be implemented in multiple steps, so treat it as a strategic process instead of a one-off action.

Use this checklist to guide your action generation process:

- Does the action have material impact on the success criteria?
- Can you implement the action, considering practical constraints and stakeholders?
- Are there potential unintended consequences?

While deriving actions may seem straightforward once you understand the problem, many analysts hesitate to make recommendations due to the stress of potential negative consequences. For example, in credit risk management, your proposed actions could impact a multi-billion dollar portfolio. This highlights an important truth: **Decision-making requires both analysis and courage.**

## Communicating Results

While communication skills are crucial for winning stakeholder buy-in, they must rest on a foundation of rigorous analysis and sound decision-making. The ability to deeply understand problems and derive effective actions is prerequisite to meaningful communication. Analysts sometimes overemphasize either communication skills at the expense of analytical fundamentals, or vice versa. The key is developing both capabilities in parallel—strong analytical skills to generate valuable insights, and clear communication skills to effectively share those insights with stakeholders.

Consider these tips for effectively communicating analytical findings:

- Begin with a clear, concise problem statement that frames the context and importance of your analysis
- Establish your methodological approach and key assumptions upfront to set proper expectations and build credibility
- Define critical metrics and success criteria explicitly to ensure alignment on how results will be evaluated
- Structure communication hierarchically—lead with key insights and recommendations before diving into supporting details
- Craft a compelling narrative that builds understanding progressively, creating moments of insight that reinforce key points
- Use data visualization strategically to illuminate patterns and relationships
- Anticipate and address potential questions or concerns proactively
- Close with a focused summary of main takeaways and specific next steps
- Tailor technical detail to your audience while maintaining analytical rigor
- Practice active listening during presentation to gauge understanding and adjust as needed

The goal is not just sharing information, but driving understanding and action. By following these principles, you can more effectively translate complex analyses into clear, actionable insights for stakeholders.
