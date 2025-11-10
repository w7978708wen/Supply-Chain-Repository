<h2>Overview</h2>

This excel spreadsheet has 2 sheets

1.ABCD Classification:
Given the profit per unit, units sold for each SKU/item, classify the item as A, B, C, or D for "Sales Ranking" and "Total Profit Ranking". 

The SKU/item that are classified as D for both categories are recommended to be discontinued. 

2.Re-Order Point:

<H2>Sheet 1. ABCD Classification</H2>

<h3>Objective:</h3>
The objective is to identify the performance of each SKU/item based on how many units are sold and total profit. Based on these performance metrics, it is recommended whether or not to discontinue the item. 

The spreadsheet is designed to update automatically whenever the percentile changes, in terms of classification and conditional formatting. 

<h3>Key insight:</h3>

It is recommended that the following products, which receive Classification D for both Sales Ranking and Total Profit Ranking, to be discontinued: 
SKU99005,SKU98633,SKU99010,SKU45667

<h3>Methodology:</h3>
I used different Excel functions to create additional columns. 

<h4>Right table 1: Total Profit Ranking </h4>
<h4>"Min amount"(to meet the cut-off) column </h4>

Equation for the first entry: 
<code>=PERCENTILE.EXC($D2:$D20, 1-K4)</code>

I used the percentile.exc function on a given column. I then selected 1 minus the 20th percentile to get total profit amounts in the top 20th percentile. 

I applied this to the top 20th, 40th, and 60th percentiles. 

<h4>"Min amount"(to meet the cut-off) column </h4>



<h4>Right table 2: Sales Ranking </h4>
<h4>"Min amount"(to meet the cut-off) column </h4>

Equation for the first entry: 
<code>=PERCENTILE.EXC($C2:$C20, 1-K11)</code>

I used the percentile.exc function on a given column. I then selected 1 minus the 20th percentile to get units sold amounts in the top 20th percentile. 

I applied this to the top 20th, 40th, and 60th percentiles. 




Left table: 
<h4>"Total Profit" column</h4>
Total Profit = Profit Per unit * Units Sold 

<h4>"Sales Ranking" column</h4>

Equation for the first entry: 

<code> =IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D"))) </code>

Nested If function is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Else if the units sold >= minimum amount to reach top 40th percentile, then classify it as "B". 

Else if the units sold >= minimum amount to reach top 60th percentile, then classify it as "C". 



<h4>"Total Profit Ranking" column</h4>

Equation for the first entry: 

<code>=IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D")))</code>

Nested If function is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Similar to the "Sales Ranking" column, I applied the elseif conditions for "B", "C". If it's neither "A", "B", nor "C", then assign it the classification of "D". 


<h4>"Discontinue" column</h4>

Equation for the first entry: 

<code>=IF(AND(E2="D",F2="D"),"Yes","No")</code>

If the cell value under the "Sales Ranking" column is "D" and if the cell value under the "Total Profit Ranking" column is "D", then assign it a value of "Yes". Else, "No". 

I also applied conditional formatting: If a cell under the "Discontinue" column contains the text "Yes", then make the cell have red highlight and red text. 
If a cell under the "Discontinue" column contains the text "No", then make the cell have green highlight and green text. 


