# retail-payment-economics
Retail Payment Transaction Costs and Impact on Net Profit
RETAIL PAYMENT ECONOMICS
Interactive Model — Project Scope & Scope Freeze
Version: 1.0
Date: August 2026
Status: For Scope Freeze / Approval
 
1. Executive Summary
The objective is to build a simple interactive model that explains the economics of retail payment acceptance, with a particular focus on:
How much of a retailer's net profit is consumed by payment transaction costs?
The model will compare the US and India using the same underlying framework and allow the user to change key variables interactively.
The model should not attempt to reproduce every detail of payment-processing economics. Instead, it should provide a transparent and intuitive framework in which the user can change:
•	Payment mix
•	Payment-method variable costs
•	Payment-method fixed costs
•	Average transaction value
•	Net profit margin
•	Annual revenue, where relevant
and immediately see the impact on:
•	Weighted payment cost
•	Payment cost as % of revenue
•	Absolute annual payment cost
•	Payment cost as % of net profit
•	Variable vs. fixed cost contribution
The most important output is:
Payment Cost ÷ Net Profit
This is the metric that makes relatively small payment-cost differences economically meaningful for low-margin retailers.
 
2. The Core Question
The model should answer one question almost instantly:
"Given this retailer's payment mix, average transaction size and profit margin, how much of its profit is being consumed by payment costs?"
It should also allow the user to explore:
•	What happens if card usage increases?
•	What happens if UPI usage increases?
•	How much does a 10 bps change matter?
•	How important are fixed transaction costs?
•	How does average ticket size affect payment economics?
•	At what profit margin does payment cost become significant?
•	At what payment mix does one market become materially more or less expensive than another?
•	What happens if UPI eventually acquires a merchant fee?
•	Why can payment costs matter disproportionately to retailers with 1–3% net margins?
•	How much does a change in average transaction value alter the effective payment cost?
•	How much of the blended cost comes from variable fees versus fixed transaction costs?
 
3. Guiding Design Principles
3.1 Simple first
The user should understand the model without needing knowledge of payment-industry terminology.
3.2 Transparent
Every important assumption should be visible.
There should be no "black box" calculation.
The user should be able to understand where the final blended payment cost comes from.
3.3 Interactive
Changing an assumption should immediately change the outputs.
3.4 Comparable
The US and India should use exactly the same fundamental calculation framework.
The difference should arise from payment mix, payment economics and user-selected assumptions — not from different formulas.
3.5 No false precision
Where actual retailer-specific data is unavailable, assumptions should be clearly identified as:
•	Reported
•	Sourced
•	Illustrative / Model Assumption
rather than presented as fact.
3.6 Expandable
The basic experience should remain simple while allowing an Advanced Mode for users who want to examine the underlying assumptions.
 
4. Model Architecture
The model consists of four layers.
Layer 1 — Retailer Economics
Inputs:
•	Annual revenue
•	Average transaction value
•	Net profit margin
From these we derive:
•	Transaction volume
•	Net profit
 
Layer 2 — Payment Mix
The retailer's sales are divided across payment methods.
Initial payment-method taxonomy:
•	Credit card
•	Debit card
•	UPI
•	Cash
•	Wallet / Other
Payment mix should be expressed primarily as:
% of sales value
rather than simply % of transaction count.
The total must equal:
100%
 
Layer 3 — Merchant Payment Acceptance Cost
The model should not assume a single universal transaction-cost percentage.
Instead, each payment method has two potential cost components:
Variable cost
A percentage of transaction value.
Example:
Credit card = 150 bps
Fixed cost
A fixed amount per transaction.
Example:
$0.05 per transaction
Therefore:
Payment Cost per Transaction = Transaction Value × Variable Fee % + Fixed Fee
The resulting blended payment cost is an output of the model, not a hard-coded assumption.
This is an important scope change from the earlier single blended-cost approach.
 
Layer 4 — Outputs
The model calculates:
•	Weighted payment cost %
•	Annual payment cost
•	Payment cost per $/₹100 of revenue
•	Net profit
•	Payment cost as % of net profit
•	Variable-cost contribution
•	Fixed-cost contribution
•	Effective payment cost by payment method
•	Sensitivity to average transaction value
 
5. Payment Methods
Payment Method	US	India	Treatment
Credit Card	Yes	Yes	Variable % + fixed cost
Debit Card	Yes	Yes	Variable % + fixed cost
UPI	N/A	Yes	Variable % + fixed cost
Cash	Yes	Yes	Primarily fixed handling cost
Wallet / Other	Yes	Yes	Variable % + fixed cost
The model should deliberately avoid going into detailed provider-level economics in Version 1.
For example, we do not initially need separate lines for:
•	Visa
•	Mastercard
•	American Express
•	Individual banks
•	Individual payment processors
•	Apple Pay
•	Google Pay
•	Walmart Pay
These may be explored later if required.
 
6. User Inputs
Basic Mode
The main interface should expose only the variables that materially affect the economics.
 
6.1 Market
Toggle:
US | India
 
6.2 Payment Mix
User controls:
•	Credit Card %
•	Debit Card %
•	UPI %
•	Cash %
•	Wallet / Other %
Total must equal:
100%
The interface should preferably use sliders.
 
6.3 Average Transaction Value
Example:
$50 / ₹1,000
This is important because fixed payment costs become more significant when transaction values are smaller.
 
6.4 Net Profit Margin
Example:
3.0%
This is one of the most important variables in the model because the same payment cost can represent a very different percentage of profit depending on the retailer's margin.
 
7. Advanced Inputs
Advanced Mode exposes the assumptions underlying each payment method.
For each method:
•	Variable payment cost %
•	Fixed cost per transaction
Optional additional variables:
•	Annual revenue
•	UPI MDR
•	Payment incentive/subsidy
•	Method-specific transaction volume
The user should be able to override the default calibrated assumptions.
 
8. Average Transaction Value
Average transaction value must be included in Version 1.
This is an important addition because payment costs are not always purely percentage-based.
For example, a payment method costing:
1.5% + ₹2 per transaction
would cost:
₹100 transaction
₹1.50 + ₹2
= ₹3.50
= 3.5% effective cost
₹1,000 transaction
₹15 + ₹2
= ₹17
= 1.7% effective cost
₹10,000 transaction
₹150 + ₹2
= ₹152
= 1.52% effective cost
Therefore:
Fixed costs matter disproportionately for low-ticket transactions.
This makes average transaction value an important variable when comparing different retail categories.
 
9. Merchant Payment Acceptance Cost — Calibration Framework
The model should use method-level assumptions rather than a single blended transaction-cost assumption.
The two components are:
9.1 Variable merchant-facing payment fee
Percentage of transaction value.
9.2 Fixed merchant-facing transaction cost
Currency amount per transaction.
The blended cost should therefore be calculated as:
Blended Payment Cost % = Weighted Variable Cost % + Effective Fixed Cost %
where:
Effective Fixed Cost % = Fixed Cost per Transaction ÷ Average Transaction Value
The key principle is:
There is no universal "40 bps" assumption.
The blended payment cost should emerge from:
Payment Mix + Variable Cost + Fixed Cost + Average Transaction Value
 
10. Calibrated Default Framework
The following ranges should be used as model calibration ranges, not as claims that every retailer pays these exact rates.
Blended Variable Cost — Default Framework
Market	Low Case	Base Case	High Case
India	~20 bps	~30–35 bps	~50 bps
US	~90 bps	~120–130 bps	~160–200 bps
These blended ranges are intended to be produced by the underlying payment mix and method-level assumptions.
They should remain editable in Advanced Mode.
 
Fixed-Cost Framework
Market	Illustrative Fixed-Cost Range	Treatment
India	₹0.25–₹0.75 / transaction	Modeling assumption; weaker universal market evidence
US	$0.05–$0.10 / transaction	Calibration range; should be sourced/calibrated where possible
The fixed-cost ranges should not be presented as universal industry facts.
 
11. Treatment of the Former 40 bps Assumption
The earlier 40 bps assumption should not be retained as the model's generic base-case transaction cost.
The reason is that a single blended assumption obscures the underlying economics.
For India in particular, 40 bps may be a reasonable higher-cost outcome depending on:
•	Payment mix
•	Credit-card share
•	Average transaction value
•	Fixed transaction costs
•	Other payment methods
For the US, 40 bps is too low to represent a generic blended merchant payment cost given the significantly higher card economics.
Therefore:
40 bps becomes a sensitivity / possible outcome, not a fundamental assumption.
 
12. India Calibration Illustration
An illustrative large-retailer payment mix can be used to demonstrate how the blended cost is derived.
This mix is an analyst/model assumption, not reported market-wide data.
Payment Method	Sales Mix	Variable Cost Assumption	Contribution
UPI	60%	0 bps	0.0 bps
Credit Card	20%	150 bps	30.0 bps
Debit Card	5%	40 bps	2.0 bps
Cash	12%	0 bps	0.0 bps
Other	3%	50 bps	1.5 bps
Total	100%		33.5 bps
This demonstrates the key principle:
The blended payment cost is an output, not an assumption.
The illustrative mix produces approximately 33.5 bps, which sits within the proposed 30–35 bps India base-case range.
 
13. UPI Treatment
The model should distinguish between:
Merchant-facing cost
What the retailer actually pays.
and:
Ecosystem economic cost
The broader cost incurred by banks, payment infrastructure providers, government, etc.
For Version 1:
The model measures merchant-facing payment cost.
Therefore, if UPI has zero merchant MDR under the applicable policy, the model may use:
0 bps
as the merchant-facing cost.
However, the assumptions panel should explicitly state:
Zero UPI MDR does not mean zero economic cost to the payment ecosystem.
This distinction is important.
 
14. UPI MDR Sensitivity
The model should explicitly allow the user to change UPI merchant pricing.
Suggested scenario:
0 bps → 10 bps → 20 bps → 30 bps
This allows the model to examine what happens if UPI moves from a zero-MDR environment toward a modest merchant charge.
Illustrative impact
At a:
60% UPI payment mix
moving UPI from:
0 bps → 30 bps
adds:
60% × 30 bps = 18 bps
to blended payment cost.
At a:
3% net profit margin
the additional 18 bps represents:
18 ÷ 300 = 6% of net profit
This is an analytical sensitivity, not a forecast of future UPI pricing.
 
15. Payment Mix — Value vs Volume
The preferred model definition is:
Payment mix = percentage of sales value
rather than percentage of transactions.
This matters because:
10% of transactions ≠ necessarily 10% of sales
For example:
•	Cash may represent many low-value transactions.
•	Credit cards may represent fewer but higher-value transactions.
•	Jewellery may have a very different payment mix from grocery.
•	E-commerce may have a different mix again.
Version 1 should therefore use sales-value mix.
An advanced version could later allow separate:
•	Transaction count mix
•	Transaction value mix
but this is not required initially.
 
16. Core Formulas
16.1 Transaction Volume
Transaction Volume = Annual Revenue ÷ Average Transaction Value
 
16.2 Payment Cost per Transaction
For each payment method:
Payment Cost per Transaction = Transaction Value × Variable Fee % + Fixed Fee
 
16.3 Effective Payment Cost %
For a payment method:
Effective Payment Cost % = Variable Fee % + (Fixed Fee ÷ Average Transaction Value)
 
16.4 Weighted Payment Cost %
Weighted Payment Cost % = Σ [Payment Mix × Effective Payment Cost %]
for all payment methods.
 
16.5 Annual Payment Cost
Annual Payment Cost = Annual Revenue × Weighted Payment Cost %
 
16.6 Net Profit
Net Profit = Annual Revenue × Net Profit Margin
 
16.7 Payment Cost as % of Net Profit
This is the principal output:
Payment Cost / Net Profit = Weighted Payment Cost % ÷ Net Profit Margin
 
17. Primary Outputs
The model should prominently display the following.
17.1 Weighted Payment Cost
Example:
1.06% of revenue
Meaning:
The retailer spends approximately $1.06 on payment acceptance for every $100 of sales.
 
17.2 Annual Payment Cost
Example:
$1.06 billion
This gives absolute scale.
 
17.3 Net Profit Margin
Example:
3.0%
 
17.4 Payment Cost / Net Profit
The most important KPI.
Example:
35.3%
Meaning:
Payment costs consume approximately 35% of the retailer's reported profit pool.
 
17.5 Variable vs Fixed Cost Contribution
Show:
Variable payment costs = X% of total payment cost
Fixed transaction costs = Y% of total payment cost
This helps users understand the effect of average ticket size.
 
18. Proposed HTML / Visual Experience
The final tool should be a single-page HTML experience.
It should feel like a compact decision tool rather than a spreadsheet.
 
Section 1 — Header
Retail Payment Economics
Subtitle:
How much of retail profit is consumed by payment acceptance?
Primary toggle:
🇺🇸 US | 🇮🇳 India
 
19. Control Panel
Controls should appear on the left or top.
Payment Mix
Interactive sliders:
•	Credit Card
•	Debit Card
•	UPI
•	Cash
•	Other
With:
Total = 100%
 
Retail Economics
Slider/input:
Net Profit Margin
Example:
1% ───────●────── 10%
 
Transaction Economics
Input:
Average Transaction Value
Example:
₹1,000
 
20. Payment Mix Visualisation
Use a:
100% stacked bar
Example:
Credit | Debit | UPI | Cash | Other
This should change dynamically as the user moves the sliders.
The user should be able to visually see the transition from:
Card-heavy → UPI-heavy
or:
Cash-heavy → Digital-heavy
 
21. Headline KPI Cards
The centre of the screen should contain large KPI cards.
Weighted Payment Cost
1.06%
Payment Cost / Net Profit
35.3%
This should be the dominant KPI.
Annual Payment Cost
$1.06bn
Net Profit
$3.0bn
 
22. Payment Cost Decomposition
Add a visual decomposition of:
Total Payment Cost
into:
Variable Cost
•	
Fixed Cost
For example:
42 bps total
could display:
•	Variable = 35 bps
•	Fixed = 7 bps
This should allow the user to immediately understand where the blended cost originates.
 
23. US vs India Comparison
A side-by-side comparison should be available.
Example:
Metric	US	India
Payment cost / revenue	1.06%	0.40%
Net margin	3.0%	3.0%
Payment cost / profit	35.3%	13.3%
A bar chart should visually highlight the difference.
The user should be able to modify both markets independently.
 
24. Sensitivity Visualisation
Version 1 should include a simple sensitivity view.
Potential formats:
Heatmap
Net Margin × Payment Cost
or:
Line chart
Payment Cost / Profit vs Net Margin
Example:
Net Margin	Payment Cost / Profit
1%	100%
2%	50%
3%	33%
4%	25%
5%	20%
This makes the central economic relationship immediately intuitive.
 
25. Ticket-Size Sensitivity
A second sensitivity view should show:
Payment Cost / Profit vs Average Transaction Value
This demonstrates why fixed costs matter.
Example:
₹100 → ₹500 → ₹1,000 → ₹5,000 → ₹10,000
As average ticket rises, fixed-cost impact declines.
This is particularly useful for comparing:
Grocery
•	High transaction frequency
•	Low average ticket
versus:
Jewellery
•	Low transaction frequency
•	High average ticket
Even if both have identical percentage payment fees, their effective payment economics can differ because of fixed transaction costs.
 
26. Dynamic Insight Box
The tool should translate the mathematics into plain English.
For example:
"At a 3.0% net margin, the modeled payment cost of 1.06% of revenue consumes 35.3% of net profit."
If the user changes the variables:
"Increasing UPI share from 40% to 60% reduces modeled payment cost from 0.62% to 0.45% of revenue, assuming all other inputs remain unchanged."
Another possible insight:
"At a ₹500 average transaction value, fixed transaction costs contribute 10 bps to the modeled payment cost. At ₹5,000, the same fixed cost contributes only 1 bp."
This makes the tool useful to non-financial users.
 
27. Basic vs Advanced Mode
Basic Mode
Expose:
•	Market
•	Payment mix
•	Average transaction value
•	Net profit margin
The payment-cost assumptions remain embedded.
 
Advanced Mode
Expose:
•	Variable payment cost
•	Fixed cost per transaction
•	UPI MDR
•	Payment incentives
•	Annual revenue
•	Transaction volume
•	Method-specific transaction volume
•	Low / Base / High cost scenarios
This allows sophisticated users to inspect the mechanics without overwhelming the normal user.
 
28. Scenario Analysis
Version 1 should support simple live scenarios.
Scenario 1 — Card-heavy
Increase card share.
Scenario 2 — UPI-heavy
Increase UPI share.
Scenario 3 — Low-margin retailer
Reduce net margin.
Scenario 4 — Higher UPI MDR
Move UPI from:
0 bps → 10 → 20 → 30 bps
Scenario 5 — Smaller ticket
Reduce average transaction value.
Scenario 6 — Higher ticket
Increase average transaction value.
Scenario 7 — Higher-cost payment environment
Move the market from:
Low → Base → High
calibrated payment-cost assumptions.
 
29. Particularly Interesting "What If?" Questions
The model should eventually allow questions such as:
"At what card mix does payment cost reach 50% of profit?"
"What happens if UPI starts charging 20 bps?"
"How much does a 10 bps reduction in card cost save?"
"How much does moving 10% of sales from cards to UPI save?"
"At what net margin does payment cost become economically insignificant?"
"How much does average ticket size affect payment economics?"
"How much of payment cost is variable versus fixed?"
These are more valuable than simply reporting payment fees.
 
30. Public-Company Calibration Layer
An optional section can allow the framework to be applied to actual listed retailers.
For each company:
•	Revenue
•	Net profit
•	Net profit margin
•	Assumed payment mix
•	Assumed average transaction value
•	Payment cost
•	Payment cost / profit
can be displayed.
However:
Company financial data and payment assumptions must remain separate.
If payment mix is not disclosed by the company, it should be labelled:
Analyst assumption
and not presented as reported data.
The public-company layer is intended as a demonstration/calibration layer, not the foundation of the generic model.
 
31. Retailer-Type Extensions
A later version could provide presets for:
Grocery
High transaction frequency
Low average ticket
General Merchandise
Medium ticket
Mixed payment methods
Jewellery
Low transaction frequency
Very high ticket
Electronics
Medium/high ticket
E-commerce
Digital-heavy payment mix
These presets are not required for Version 1 but are compatible with the framework.
 
32. Data & Evidence Policy
The model should use the following hierarchy.
Financial data
Prefer:
1.	Company annual reports
2.	Regulatory filings
3.	Investor presentations
4.	Credible financial databases
 
Payment costs
Prefer:
1.	Payment networks
2.	Regulators
3.	Government sources
4.	Industry bodies
5.	Credible research
 
Payment mix
Prefer:
1.	Company disclosure
2.	Industry data
3.	Analyst assumption where unavailable
 
Fixed transaction costs
Unless a credible source exists, clearly identify them as:
Illustrative / Modeling Assumption
 
Important calibration principle
Payment gateway list prices for small merchants should not automatically be treated as the economics paid by very large retailers.
Where possible, the model should distinguish:
•	Published schedule
•	Merchant-facing observed/estimated rate
•	Large-retailer negotiated economics
•	Analyst/model assumption
 
33. Assumption Labelling
Every assumption should carry one of three labels.
Reported
Directly disclosed by company/regulator.
Sourced
Derived from a credible external source.
Illustrative / Modeling Assumption
User/model assumption where reliable public data is unavailable.
This is important because the tool is intended to be an economic framework, not a false-precision calculator.
 
34. Version 1 — Explicitly Out of Scope
The following should NOT be included initially.
Payment-network detail
•	Visa vs Mastercard
•	Amex
•	Network assessment fees
•	Issuer interchange economics
•	Detailed issuer/network economics
Customer economics
•	Cashback
•	Rewards
•	Loyalty economics
Risk economics
•	Fraud
•	Chargebacks
•	Fraud prevention costs
Working capital
•	Settlement timing
•	Float
•	Cash conversion
Commercial impact
•	Incremental sales from Apple Pay
•	Conversion-rate improvement
•	Customer retention
•	Customer acquisition
Technology
•	Payment gateway infrastructure costs
•	POS software costs
•	ERP integration
Macro / policy
•	Forecasting future UPI policy
•	Predicting future card interchange regulation
These may become Version 2 modules.
 
35. QA / Model Integrity Checks
The tool must automatically check:
Payment mix
Total:
100%
 
Transaction value
Must be:
> 0
 
Net margin
Must be:
> 0
for payment cost/profit calculation.
If zero or negative:
Payment Cost / Profit = N/M
rather than producing a misleading number.
 
Fixed-cost reconciliation
Fixed costs should reconcile to:
Transaction Volume × Fixed Cost
 
Weighted-cost reconciliation
Total payment cost should equal:
Σ payment-method costs
 
Variable / fixed reconciliation
Total payment cost should reconcile to:
Variable payment cost + Fixed payment cost
 
Currency
US calculations remain in:
USD
India calculations remain in:
INR
 
Dynamic integrity
Changing one variable should only affect logically connected outputs.
 
36. Key Conceptual Relationship
The entire model can ultimately be understood through one simple relationship:
Payment Cost / Net Profit = Payment Cost % of Revenue ÷ Net Profit Margin
This is the conceptual heart of the model.
For example:
Payment cost = 1%
Net Margin	Payment Cost / Profit
1%	100%
2%	50%
3%	33%
4%	25%
5%	20%
10%	10%
This is why payment costs that look tiny on a revenue basis can become enormous relative to profit.
 
37. Why Fixed Costs Matter
The model should explicitly demonstrate:
The lower the average transaction value, the larger the effective impact of fixed payment costs.
This creates a useful distinction between retailers.
For example:
Grocery
•	High transaction count
•	Low average ticket
versus:
Jewellery
•	Low transaction count
•	High average ticket
Even if both have identical percentage payment fees, their effective payment economics can differ because of fixed transaction costs.
 
38. Key Insight the Model Should Enable
The ultimate purpose is not to determine:
"Visa costs 157 bps."
The more interesting question is:
"How does the structure of a retailer's transactions determine how much of its profit is consumed by payment acceptance?"
That is the strategic insight the tool should communicate.
The model should make clear that:
Payment economics are a function of payment mix, pricing, transaction size and retailer profitability.
Not simply:
"What is the card fee?"
 
39. Recommended Build Sequence
Phase 1 — Freeze
Approve:
•	Definitions
•	Formulae
•	Payment-method taxonomy
•	Inputs
•	Outputs
•	Calibrated assumptions
•	Assumption treatment
•	Visual design
 
Phase 2 — Calculation Engine
Build the mathematical model independently of the UI.
Test:
•	Payment mix
•	Fixed cost
•	Variable cost
•	Average ticket
•	Margin
•	Annual revenue
•	US vs India
 
Phase 3 — Assumptions
Populate initial assumptions and source them where possible.
Clearly classify:
•	Reported
•	Sourced
•	Illustrative
The model should retain source references for all sourced assumptions.
 
Phase 4 — HTML Interface
Build the single-page interactive interface.
 
Phase 5 — Visualisation
Add:
•	KPI cards
•	Payment mix chart
•	Variable vs fixed cost decomposition
•	US vs India comparison
•	Sensitivity chart
•	Ticket-size sensitivity
•	Dynamic insight box
•	Assumptions panel
 
Phase 6 — QA
Run:
•	Formula checks
•	Boundary checks
•	Reconciliation checks
•	US/India comparison checks
•	Sensitivity checks
 
Phase 7 — Calibration
Apply the model to selected listed retailers.
This becomes a demonstration layer, not the foundation of the model.
 
40. Scope Freeze Criteria
The scope should be considered frozen once we agree on these items:
1.	Core formula set
2.	Payment-method taxonomy
3.	Payment mix methodology
4.	Merchant Payment Acceptance Cost definition
5.	Variable + fixed cost decomposition
6.	Inclusion of average transaction value
7.	Calibrated US/India default ranges
8.	Basic vs Advanced input structure
9.	Primary KPI: Payment Cost / Net Profit
10.	Single-page HTML visualisation concept
11.	Assumption labelling framework
12.	Data/evidence hierarchy
After this point, changes should be treated as Version 2 enhancements, rather than changes to the fundamental model.
 
41. Final Product Philosophy
The finished tool should sit somewhere between:
a financial model
and
an explanatory visual calculator.
It should not feel like Excel.
It should not feel like a payment-industry technical document.
It should feel like:
"Give me a few assumptions and I'll show you the economic significance of payment costs in 30 seconds."
The user should be able to move one slider — for example:
UPI share from 40% to 60%
and immediately understand:
Payment cost ↓ → profit burden ↓
while simultaneously seeing how the result changes with:
•	Transaction size
•	Payment pricing
•	Payment mix
•	Profit margin
•	Fixed-cost contribution
 
42. One-Line Definition of the Product
An interactive retail economics model that converts payment mix, variable and fixed transaction costs, ticket size and profit margins into a simple measure of how much of a retailer's profit is consumed by payment acceptance.
 
SCOPE FREEZE — VERSION 1.0
In scope
Payment mix + variable cost + fixed cost + average ticket + net margin + US/India comparison + sensitivity + visualisation
Primary output
Payment Cost as % of Net Profit
Primary design principle
Simple enough to understand. Comprehensive enough to interrogate.
Fundamental model principle
Do not assume a single blended transaction cost. Derive it.
Next step after approval
Build the calculation engine first, before touching the HTML/UI.
