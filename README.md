<h2>Overview</h2>

This excel spreadsheet has 2 sheets

1.ABCD Classification:
Given the profit per unit, units sold for each SKU/item, classify the item as A, B, C, or D for "Sales Ranking" and "Total Profit Ranking". 

The SKU/item that are classified as D for both categories are recommended to be discontinued. 

2.Re-Order Point:

<H2>Sheet 1. ABCD Classification</H2>

<h3>Objective:</h3>
The objective is to identify the performance of each SKU/item based on how many units are sold and total profit. Based on these performance metrics, it is recommended whether or not to discontinue the item. 

<h3>Methodology:</h3>
I used different Excel functions to create additional columns. 

Right table 1: Total Profit Ranking 
<h4>"Min amount"(to meet the cut-off) column </h4>

Left table: 
<h4>"Total Profit" column</h4>
Total Profit = Profit Per unit * Units Sold 

<h4>"Sales Ranking" column</h4>

Equation for the first entry: 

<code> =IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D"))) </code>

Nested If function is used. If the units sold >= minimum amount to reach top 20th percentile, then classify it as "A". 

Else if the units sold >= minimum amount to reach top 40th percentile, then classify it as "B". 

Else if the units sold >= minimum amount to reach top 60th percentile, then classify it as "C". 

Else classify it as "D". 


