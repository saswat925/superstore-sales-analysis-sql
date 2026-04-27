# superstore-sales-analysis-sql


The Superstore Story: From Raw Data to Business Decisions
Chapter 1: The Dataset
I got my hands on a Global Superstore dataset — 51,252 transactions, 4,873 customers, across 7 markets worldwide. The mission? Find where the money is being made, where it's being lost, and what the business should do next.

Tools: SQL | Snowflake | Power BI

Chapter 2: Cleaning the Mess
Before any analysis, the data needed fixing:

Dates were stored as text — converted to proper DATE format
278 product names had broken encoding characters — fixed them
Found 38 duplicate rows — removed
Standardized market names and trimmed whitespace from all text columns
Lesson: Never trust raw data. Always clean first.

Chapter 3: The Big Picture
Total Sales	$12.63M
Total Profit	$1.46M
Profit Margin	11.60%
Total Orders	25,035
Avg Discount	8.14%
12.63M in sales sounds great — but only 1.46M stayed as profit. That's just 11.6 cents on every dollar. Something is eating into the margins. Let's dig deeper.

Chapter 4: The Growth Story
Year	Sales	Profit	Growth
2011	$2.26M	$248K	—
2012	$2.67M	$307K	+18%
2013	$3.40M	$406K	+27%
2014	$4.30M	$504K	+26%
Sales nearly doubled in 4 years. Profit grew from 248K to 504K. The business is scaling — but is it scaling profitably?

Chapter 5: Who's Buying?
Segment	Sales	Margin
Consumer	$6.50M (51.5%)	11.49%
Corporate	$3.82M (30.3%)	11.53%
Home Office	$2.31M (18.3%)	11.99%
Consumer segment is the engine — driving half the revenue. But Home Office quietly has the best margin at 11.99%.

Chapter 6: The Category Battle
Category	Sales	Profit	Margin
Technology	$4.74M	$662K	13.97%
Furniture	$4.11M	$285K	6.94%
Office Supplies	$3.78M	$517K	13.68%
Technology wins. Best sales AND best margin.

Furniture is the problem child — 4.1M in sales but only 285K profit. For every 100 sold in furniture, only 6.94 is profit.

Chapter 7: The Tables Disaster
Digging into sub-categories, I found the real culprit:

Sub-Category	Sales	Profit	Margin
Copiers	$1.51M	+$259K	+17.13%
Paper	$244K	+$59K	+24.23%
Tables	$757K	-$64K	-8.47%
Tables is the ONLY sub-category running at a loss. Every table sold is losing money. This single sub-category dragged down the entire Furniture category.

Recommendation: Renegotiate supplier pricing or discontinue low-margin table products.

Chapter 8: The Discount Trap
This was the biggest discovery:

Discount	Orders	Profit	Avg Profit/Order
0-5%	29,444	+$1.83M	+$62
5-10%	4,212	+$280K	+$66
10-20%	6,271	+$173K	+$28
20-30%	965	-$21K	-$22
30%+	10,360	-$793K	-$77
Discounts above 20% destroyed $814K in profit.

10,360 orders had 30%+ discounts — and they collectively lost $793K. That's more than half of total profit wiped out by aggressive discounting.

This is the #1 profit killer in the entire business.

Chapter 9: The Global Map
Market	Sales	Margin
APAC	$3.58M	12.13%
EU	$2.94M	12.69%
US	$2.30M	12.46%
LATAM	$2.16M	10.24%
EMEA	$806K	5.44%
Canada	$67K	26.62%
APAC is the biggest market. But the real story is at the extremes:

Canada — tiny market ($67K) but 26.62% margin. Scale it up!
EMEA — $806K sales but only 5.44% margin. Needs urgent review.
Southeast Asia — $883K sales, 1.99% margin. Almost zero profit.
Chapter 10: Heroes & Villains
Top Products (Heroes):

Canon Imageclass 2200 Copier → +$25,200 profit
Cisco Smart Phone → +$17,239
Motorola Smart Phone → +$17,027
Worst Products (Villains):

Cubify 3D Printer Double Head → -$8,880 loss
Lexmark Laser Printer → -$4,590
Motorola Smart Phone, Cordless → -$4,447
Interesting: Motorola appears on BOTH lists — the Full Size model makes 17K profit, but the Cordless model loses 4.4K. Same brand, opposite results.

Customer Alert: Sean Miller spent 35,170 (4th highest) but generated **-410 loss**. Heavy discounting suspected.

Chapter 11: Final Verdict
Finding	Action
Discounts >20% losing $814K	Cap maximum discount at 20%
Tables sub-category losing $64K	Renegotiate or discontinue
Southeast Asia at 1.99% margin	Review pricing strategy
EMEA at 5.44% margin	Audit operational costs
Canada at 26.62% margin	Invest and scale up
3D Printers losing money	Remove from catalog
Technology at 13.97% margin	Double down on Tech products
60% orders use Standard shipping	Optimize shipping costs
The Bottom Line
The Superstore is growing fast — 90% revenue growth in 4 years. But heavy discounting is the silent killer, destroying 814K in potential profit. Fix the discount policy, cut the Tables losses, and double down on Technology and high-margin markets like Canada — and this business could easily hit **2M+ in annual profit**.

Analysis by Saswat Betta | SQL on Snowflake

