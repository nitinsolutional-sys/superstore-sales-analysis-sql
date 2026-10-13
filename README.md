Superstore Profitability Analysis: Client Report
Oct 13, 2026 · @Nitin Ahluwalia
Superstore grew sales by about 30% in 2025 and 21% in 2026, but its profit margin stayed near 13%. Discounts above 20% lost about $136K, close to half of the $292K total profit, so discount control is the fastest way to raise profit.
Executive summary
•	Overall: 10,194 order lines from 5,111 orders and 804 customers (January 2023 to December 2026) produced $2.33M in sales and $292K in profit, a 12.6% margin.
•	Discounts are the biggest leak. Lines with no discount earn a 29.6% margin. Lines discounted above 20% lose money in every band, about $136K combined.
•	Furniture sells but does not earn. It brings in $755K of sales at a 2.6% margin. Tables (-$17.8K) and Bookcases (-$3.6K) lose money outright.
•	Technology and Office Supplies carry the business. Together they earn about $272K of the $292K profit, at margins of about 17%.
•	Location matters. The West earns a 15.0% margin and the Central region only 7.9%. Texas, Ohio, Pennsylvania and Illinois lost more than $70K together.
•	Recommended first step: cap discounts at 20% and review the pricing of Tables and Bookcases.
Business problem and scope
Superstore sells furniture, office supplies and technology to consumers, corporate and home-office customers across the US and Canada. Sales look healthy. Management wants to know where profit is made, where it is lost, and what to change.
This report answers five questions:
1.	How is the business performing overall, and how has it changed by year?
2.	Which categories and products make or lose money?
3.	Which regions and states underperform?
4.	How do discounts affect profit?
5.	Are any customers or shipping practices a concern?
Data and approach
Data. One table of 10,194 order lines with 21 columns: order and ship dates, customer, location, category and sub-category, sales, quantity, discount and profit. There were no missing values and no duplicate rows.
Tools. SQL Server Express and SQL Server Management Studio.
Method.
1.	Profiled the table: row counts, distinct orders, customers and products, and the date range.
2.	Checked quality: looked for nulls and duplicates, and checked a sample of dates against the source file.
3.	Cleaned the data in a view so the raw table stayed untouched. The Discount column had been stored as a floating-point number, which put some rows into the wrong discount bands (for example, 20% discounts counted as above 20%). I converted it to a fixed-precision decimal and re-checked the results.
4.	Analysed with GROUP BY, CASE WHEN, CTEs and window functions (LAG, DENSE_RANK), then turned the results into recommendations.
Full queries are in the SQL files linked at the end of this report.
Finding 1. The business is profitable, but not efficient
Measure	Result
Total sales	$2,326,534
Total profit	$292,297
Profit margin	12.6%
Orders	5,111
Customers	804
Only about 13 cents of every sales dollar becomes profit. The rest of this report looks at where the other 87 cents is going.
[Screenshot 1: KPI query and result]
Finding 2. Sales are growing, but margin is not
Year	Sales	Profit	Margin	Sales growth
2023	$494,040	$51,684	10.5%	n/a
2024	$472,993	$62,021	13.1%	-4.3%
2025	$613,934	$82,665	13.5%	+29.8%
2026	$745,568	$95,926	12.9%	+21.4%
Sales dipped in 2024, then rebounded strongly. The margin has stayed in a narrow 13% band since 2024, so the extra sales have added profit only in proportion. Growth alone will not fix profitability.
[Screenshot 2: yearly trend query and result]
Finding 3. Discounts above 20% destroy profit
Discount band	Order lines	Profit	Margin
No discount	4,925	$326,719	29.6%
Up to 10%	96	$9,100	16.6%
11 to 20%	3,758	$92,499	11.5%
21 to 30%	230	-$10,513	-10.1%
31 to 50%	311	-$48,477	-24.8%
Over 50%	874	-$77,030	-118.7%
The pattern is clear. Discounts up to 20% still leave a profit. Every band above 20% loses money, and the deepest discounts lose more than they bring in. The 1,415 lines discounted above 20% lost about $136K, close to half of total profit. In total, 1,901 order lines (18.6%) were sold at a loss.
[Screenshot 3: discount band query and result. This is the most important image in the report.]
Finding 4. Furniture earns little, and some products lose money
Category	Profit	Margin
Technology	$146,543	17.4%
Office Supplies	about $126,000	about 17%
Furniture	$19,730	2.6%
Three sub-categories lose money: Tables (-$17,753, a -8.5% margin), Bookcases (-$3,632) and Supplies (-$1,171). Furniture accounts for $755K of sales, the largest share in the business, but almost none of the profit.
[Screenshot 4: sub-category query and result, sorted so the losses are at the top]
Finding 5. Some states and one region underperform
The West earns the best margin (15.0%) and the Central region the worst (7.9%). The five weakest states by profit are:
State	Profit
Texas	-$25,729
Ohio	-$16,971
Pennsylvania	-$15,560
Illinois	-$12,608
North Carolina	-$7,491
These states were not checked for the cause. The likely reasons to test are heavy discounting and a product mix weighted towards Furniture.
[Screenshot 5: region result and worst-states result]
Finding 6. Customers and shipping
The largest customer by sales, Sean Miller ($25,043), is unprofitable (-$1,981). Revenue alone is a poor way to judge customers.
Shipping is not a problem. Average delivery time is about 4 days overall, and each ship mode meets its promise: Same Day 0 days, First Class 2.2, Second Class 3.2, Standard Class 5.0.
[Screenshot 6 (optional): top customers and shipping results]
Recommendations
1.	Cap discounts at 20%. Require manager approval for anything higher. This targets the $136K loss directly.
2.	Reprice or stop discounting Tables and Bookcases. Raise prices, renegotiate supplier costs, or drop the worst-performing products.
3.	Investigate the loss-making states. Check discounts, shipping costs and product mix in Texas, Ohio, Pennsylvania and Illinois.
4.	Promote the high-margin lines. Copiers, Accessories, Paper, Labels and Envelopes all earn margins above 24%.
5.	Judge customers on profit, not only sales. Review the largest accounts for discount-driven losses.
6.	Plan stock and campaigns around the September to December peak. Sales are highest then and lowest in February.
Limitations
This analysis shows what happened, not why. The dataset has no cost, return or supplier data, so the causes above are strong hypotheses rather than proven facts. The first next step would be to add that data and test them.
Next steps
1.	Build an Excel or Power BI dashboard with the key charts: profit by sub-category, margin by discount band, and yearly sales.
2.	Estimate the profit gain from capping discounts at 20%.
3.	Repeat the analysis monthly so changes can be tracked.
I am available for SQL and Excel analysis projects like this one. Queries, screenshots and this report are on GitHub: [add your link here].
[SUPERSTORE PROJECT.docx](https://github.com/user-attachments/files/33378427/SUPERSTORE.PROJECT.docx)
