<h2>Overview</h2>

This excel spreadsheet contains:

1.ABCD Classification:
Given the profit per unit and units sold for each SKU/item, the item is classified as "A", "B", "C", or "D" based on "Sales Ranking" and "Total Profit Ranking" metrices. 

The SKU/item that are classified as "D" in both categories are recommended to be discontinued. 

Here is a snippet of how the sheet looks like:
<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%201.png?raw=true"></img>

<H2>Sheet 1. ABCD Classification</H2>

<h3>Objective:</h3>
The objective is to evaluate the performance of each SKU/item based on how many units are sold and total profit. Based on these performance metrics, it is recommended whether or not to discontinue the item. 

The spreadsheet is designed to update automatically (in terms of classification and conditional formatting) when the percentile input or other data values change.

<h3>Key insight:</h3>

The following products are recommended to be discontinued, since they receive a D classification for both Sales Ranking and Total Profit Ranking: 
SKU99005,SKU98633,SKU99010,SKU45667

<h3>Methodology:</h3>
I used several Excel functions to create additional calculated columns. 

<h4>Right table 1: Total Profit Ranking </h4>

<h4>"Min amount"(to meet the cut-off) column </h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%202.png?raw=truee"></img>

Equation for the first entry: 
<code>=PERCENTILE.EXC($D2:$D20, 1-K4)</code>

I used the <code>percentile.exc</code> function on a given column to determine the threshold amounts for the top 20th, 40th, and 60th percentiles of total profit. In particular, I used 1 minus the 20th percentile to get total profit amounts in the top 20th percentile. 




<h4>Right table 2: Sales Ranking </h4>

<h4>"Min amount"(to meet the cut-off) column </h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%203.png?raw=true"></img>

Equation for the first entry: 
<code>=PERCENTILE.EXC($C2:$C20, 1-K11)</code>

I used the <code>percentile.exc</code> function on a given column to determine the threshold amounts for the top 20th, 40th, and 60th percentiles of units sold amounts. In particular, I used 1 minus the 20th percentile to get units sold amounts in the top 20th percentile. 




<h4>Left table</h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%204.png?raw=true"></img>

<h4>"Total Profit" column</h4>

Total Profit = Profit Per unit * Units Sold 

<h4>"Sales Ranking" column</h4>

Equation for the first entry: 

<code> =IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D"))) </code>

<code>Nested IF</code> is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Else if the units sold >= minimum amount to reach top 40th percentile, then classify it as "B". 

Else if the units sold >= minimum amount to reach top 60th percentile, then classify it as "C". 



<h4>"Total Profit Ranking" column</h4>

Equation for the first entry: 

<code>=IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D")))</code>

<code>Nested IF</code> function is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Similar to the "Sales Ranking" column, I applied the same classification logic for "B", "C". If it's neither "A", "B", nor "C", then assign it the classification of "D". 


<h4>"Discontinue" column</h4>

Equation for the first entry: 

<code>=IF(AND(E2="D",F2="D"),"Yes","No")</code>

If the cell value under the "Sales Ranking" column is "D" and if the cell value under the "Total Profit Ranking" column is "D", then assign it a value of "Yes". Else, "No". 

I also applied conditional formatting: 

If a cell under the "Discontinue" column contains the text "Yes", then make the cell have red highlight and red text. 
If a cell under the "Discontinue" column contains the text "No", then make the cell have green highlight and green text. 


