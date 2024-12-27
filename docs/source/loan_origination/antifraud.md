# Antifraud

**Date**: December 2024

**Last Updated**: December 2024

This document is written from the perspective of someone with a background in underwriting and loan origination. As such, it may not be exhaustive for seasoned antifraud professionals. Furthermore, the specific types of fraud encountered are highly dependent on the product structure and its use cases. For example, embedded finance products, such as Buy Now Pay Later (BNPL) options on e-commerce platforms, are generally less susceptible to merchant fraud compared to open market products like credit cards.

This document outlines a mental model for approaching antifraud, covering key aspects such as objectives, common fraud types, and preventative measures.

## Components of Antifraud

Effective antifraud measures require a comprehensive understanding of all participants involved in a transaction. These typically include the **buyer**, **seller**, and the **lender** providing credit. More complex transactions may also involve intermediaries such as **acquirers** or **payment processors**, while offline transactions might include **sales agents**. Each participant has a distinct role and, consequently, presents a unique potential for fraud or may lack the necessary incentives or capabilities to prevent it. Therefore, from a lender's perspective, it is essential to identify and mitigate the specific fraud risks associated with each participant. The initial step, then, is to identify all participants in the transaction.

Once all participants are identified, the next crucial step is to pinpoint the specific fraud risks associated with each. While some common fraud types exist, effectively combating fraud requires a proactive, adversarial mindset. We must anticipate the evolving tactics of fraudsters, who are constantly seeking new loopholes, driven by inherent incentives.

### Buyer

Key objectives in preventing buyer fraud include:

- Mitigating **identity theft** and **account takeover**.
- Preventing **coordinated group attacks**.

The following are common fraud types associated with buyers:

-   **Identity Theft:** A fraudster uses another individual's personal information to apply for credit.
-   **Synthetic Identity Fraud:** A fabricated identity is created by combining real and fake information, sometimes using deepfakes to mimic a person's appearance or voice.
-   **Account Takeover:** A legitimate buyer's account is compromised and subsequently used to fraudulently obtain credit.
-   **Group Fraud:** Fraudsters often operate in organized groups, and a buyer may be part of a larger fraud ring.
-   **Return Fraud:** Buyers may exploit return policies for fraudulent purposes, such as returning a different item or damaged goods.

To mitigate these risks, lenders should implement strong **Know Your Customer (KYC)** and transaction verification processes to rigorously confirm buyer identities. These measures will be discussed in more detail in the mitigation section below.

As previously mentioned, the specific types of fraud encountered are highly dependent on the product structure and its use cases. For credit card products, additional fraud types include:

-   **Stolen or Lost Cards:** A fraudster uses a stolen or lost card to make unauthorized purchases.
-   **Card Not Present (CNP) Fraud:** A fraudster uses a card without being physically present at the point of sale, typically through online or phone transactions.
-   **Skimming:** A fraudster uses a device to illegally copy card data from the magnetic stripe.

### Seller

Key objectives in preventing seller fraud are:

- To prevent **collusion with buyers**.
- To prevent **fraudulent chargebacks and refunds**.

Sellers also present unique fraud risks. Common fraud types include:

-   **Fraudulent Cash-Out:** This occurs when a seller colludes with a buyer (or fraudster) to extract the credit limit as cash. For example, the buyer makes a purchase, but the goods are never delivered. The buyer receives the funds from the lender and often shares a portion with the seller.
-   **Transaction Laundering:** This involves a merchant processing transactions on behalf of another business that is either prohibited (e.g., online gambling, adult content) or considered high-risk, effectively disguising the true nature of the transaction.
-   **Refund Fraud:** A merchant processes a fake refund to their own account, effectively siphoning funds from the lender.

The degree of control a lender exerts over a seller varies significantly based on the product structure and its intended use. For example, in embedded finance arrangements, lenders typically have greater oversight of sellers compared to open market products like credit cards.

## Mitigation

### Identity Verification

Identity verification comprises two crucial elements: verification against a trusted third-party source and the detection of fraudulent identity information.

-   **Third-Party Verification:** This process typically involves comparing the buyer's provided identity information and facial image against a trusted third-party source, such as a government database, to confirm their authenticity.
-   **Fake Identity Detection:** This employs various technologies, including models to identify counterfeit identity documents, deepfakes, and 1-to-N matching against a database of existing identities, as well as liveness detection to ensure the individual is physically present.

### Account Takeover

Account takeover attempts can be detected by monitoring various suspicious activities, such as unusual login attempts per device, IP address, or user, changes in credentials, and a high number of activation attempts.

Mitigation measures following the identification of potential account takeover risks may include rejecting the account, implementing a cooling-off period, or requiring additional verification steps, such as liveness detection with facial verification. **Multi-factor authentication (MFA)**, regular password changes, and robust password policies are also effective deterrents.

Additionally, **device fingerprinting** can help identify suspicious devices used for account creation or login by analyzing browser and device characteristics to create unique identifiers. **Behavioral biometrics**, which analyzes user behavior patterns (e.g., typing speed, mouse movements), can also help detect anomalies indicative of account takeovers or bots.

### Merchant Onboarding

Merchant onboarding, also referred to as **Know Your Business (KYB)**, is the process of verifying a merchant's legitimacy before establishing a business relationship. This verification may encompass confirming the merchant's identity, business registration, and screening against sanctions and **Politically Exposed Persons (PEP)** lists, among other relevant checks. Furthermore, during onboarding, acquirers might gather supplementary business data, such as the GPS coordinates of the merchant's physical location and details about their business activities.

It's worth noting that acquirers may lack the direct incentive to conduct comprehensive KYB checks, as they are not the primary bearers of financial risk stemming from merchant fraud.

### Transaction Monitoring

Transaction monitoring typically involves observing suspicious activities, including:

-   **Unusual Transaction Volume:** A sudden surge in transaction volume processed by a merchant, often within a short timeframe.
-   **High-Risk Merchant Designation:** A merchant flagged as high-risk due to prior fraudulent behavior or other indicators.
-   **Excessive Transaction Amounts:** Transactions exceeding established thresholds based on the merchant's historical activity.
-   **High-Risk Geographic Location:** A merchant operating from a location known for elevated fraud rates, such as fraud hotspots.
-   **High-Risk Industry Affiliation:** A merchant engaged in a high-risk sector, such as online gambling or adult entertainment.

### Data Analysis and Machine Learning

-   **Graph Analysis:** Graph analysis can be used to map entities and their relationships, employing graph algorithms to detect patterns and anomalies indicative of fraudulent activity.

### Balancing Fraud Prevention and User Experience

-   **Segmented User Journey:** Implement a streamlined checkout process for known, low-risk customers, while incorporating additional verification steps for high-risk profiles.
-   **Dynamic Friction:** Employ dynamic friction by increasing verification requirements only when necessary, adjusting the level of friction in response to the evolving risk profile.

### Sources of Inspiration

As previously discussed, combating fraud is an ongoing challenge, as fraudsters continually adapt their tactics. Inspiration for antifraud measures can be drawn from various sources, including reported cases, active monitoring of social media platforms like X (formerly Twitter), Reddit, and Facebook, close collaboration with industry professionals and law enforcement, and even red teaming exercises, where experts simulate attacks to identify system vulnerabilities.

## Disclaimer

This document is a work in progress and should be considered less definitive than other documents in this series. It will be updated as more information becomes available.