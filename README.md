<h2>Overview:</h2>

In  E x c e l, I created a workbook to streamline supply chain management: 

Sheet 1. ABCD Classification:

Given the profit per unit and units sold for each SKU/item, the item is classified as "A", "B", "C", or "D" based on "Sales Ranking" and "Total Profit Ranking" metrices. 

The SKU/item that are classified as "D" in both categories are recommended to be discontinued. 


Sheet 2. Re-Order Point & VLOOKUP:

Given the beginning & current stock counts and the re-order point for each SKU/item, the current stock count is calculated which further determines whether determine it needs to be re-ordered.  

The XLOOKUP function is used here to efficiently match each SKU with its corresponding current inventory count.

<H2>Sheet 1. ABCD Classification:</H2>

Here is a snippet of how the sheet looks:
<img src="https://github.com/w7978708wen/Supply-Chain-Repository/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%201.png?raw=true"></img>

<h3>Objective:</h3>
The objective is to evaluate the performance of each SKU/item based on how many units are sold and total profit. Based on these performance metrics, it is recommended whether or not to discontinue the item. 

The spreadsheet is designed to update automatically (in terms of classification and conditional formatting) when the percentile inputs or other data values change.

<h3>Key insight:</h3>

The following products are recommended to be discontinued, since they receive a D classification for both Sales Ranking and Total Profit Ranking: 
SKU99005,SKU98633,SKU99010,SKU45667

<h3>Methodology:</h3>
I used several E x c e l functions to create additional calculated columns. 

<h4>Right table 1: Total Profit Ranking:</h4>

<h4>"Min amount"(to meet the cut-off) column:</h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%202.png?raw=truee"></img>

Equation for the first entry: 
<code>=PERCENTILE.EXC($D2:$D20, 1-K4)</code>

I used the <code>PERCENTILE.EXC</code> function to determine the threshold amounts for the top 20th, 40th, and 60th percentiles of total profit. Specifically, I used 1 minus the 20th percentile to get total profit amounts in the top 20th percentile. 



<h4>Right table 2: Sales Ranking:</h4>

<h4>"Min amount"(to meet the cut-off) column </h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%203.png?raw=true"></img>

Equation for the first entry: 
<code>=PERCENTILE.EXC($C2:$C20, 1-K11)</code>

I used the <code>PERCENTILE.EXC</code> function to determine the threshold amounts for the top 20th, 40th, and 60th percentiles of units sold amounts. Specifically, I used 1 minus the 20th percentile to get units sold amounts in the top 20th percentile. 




<h4>Left table:</h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Repository/blob/main/Screenshots/ABCD%20Classification%20sheet%20pt%204.png?raw=true"></img>

<h4>"Total Profit" column:</h4>

Total Profit = Profit Per Unit * Units Sold 

<h4>"Sales Ranking" column:</h4>

Equation for the first entry: 

<code> =IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D"))) </code>

<code>Nested IF</code> is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Else if the units sold >= minimum amount to reach top 40th percentile, then classify it as "B". 

Else if the units sold >= minimum amount to reach top 60th percentile, then classify it as "C". 



<h4>"Total Profit Ranking" column:</h4>

Equation for the first entry: 

<code>=IF(D2>=$L$4,"A",IF(D2>=$L$5,"B",IF(D2>=$L$6,"C","D")))</code>

<code>Nested IF</code> function is used. If the units sold >= minimum amount to reach top 20th percentile (calculated earlier, from right table), then classify it as "A". 

Similar to the "Sales Ranking" column, I applied the same classification logic for "B", "C". If it's neither "A", "B", nor "C", then assign it the classification of "D". 


<h4>"Discontinue" column:</h4>

Equation for the first entry: 

<code>=IF(AND(E2="D",F2="D"),"Yes","No")</code>

If the cell value under the "Sales Ranking" column is "D" and if the cell value under the "Total Profit Ranking" column is "D", then assign it a value of "Yes". Else, "No". 

I also applied conditional formatting: 

If a cell under the "Discontinue" column contains the text "Yes", then make the cell have red highlight and red text. 
If a cell under the "Discontinue" column contains the text "No", then make the cell have green highlight and green text. 


<hr style="height:5px;background-color:#1e1c1f;">
<H2>Sheet 2.Pivot Table – SKU Profits</H2>

I created a Pivot Table using the columns in the "ABCD Classification" sheet's left table.

I categorized the products by "Total Profit Ranking". I also sorted the "Average Profit Per Unit" column in ascending order to get a quick view of which products have the lowest "Average Profit Per Unit" and should be recommended for discontinuation.

Here is a snippet of how the sheet looks like:

<img src="https://github.com/w7978708wen/Supply-Chain-Repository/blob/main/Screenshots/Pivot%20Table%20%E2%80%93%20SKU%20Profits%20pt%201.png?raw=true"></img>


<hr style="height:5px;background-color:#1e1c1f;">
<H2>Sheet 3.Re-Order Point & VLOOKUP</H2>

<h3>Objective:</h3>
The objective is to determine whether each SKU/item needs to be re-ordered based on the current stock count. 

Here is a snippet of how the sheet looks like:

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/Re-Order%20Point%20&%20VLOOKUP%20sheet%20pt%201.png?raw=true"></img>


The XLOOKUP function efficiently matches each SKU with its corresponding current inventory count, making XLOOKUP a great tool in supply chain management. 

The spreadsheet is designed to update automatically (in terms of whether a SKU/item needs to be re-ordered) when values like number of units sold and re-order point change.

<h3>Key insight:</h3>

There are currently 6 items that need to be re-ordered, because the current stock on hand is less than the re-order point: SKU22769, SKU45456, and others...

<h3>Methodology:</h3>
Given the beginning stock, units sold, re-order point of each SKU/item, I used several functions to create additional calculated columns. 

<h4>Left table:</h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/Re-Order%20Point%20&%20VLOOKUP%20sheet%20pt%202.png?raw=true"></img>

<h4>Current Stock On Hand column:</h4>
Current Stock On Hand = Beginning Stock  Sales/Consumed 

<h4>RE-ORDER column:</h4>

<code>=IF(E2>=D2,"No", "Yes")</code>

I used an <code>IF</code> function, such that if the current stock on hand is greater than or equal to the re-order point, then assign the cell value is "No". Otherwise, assign the cell value as "Yes". 

<h4>Right table:</h4>

<img src="https://github.com/w7978708wen/Supply-Chain-Case-Study-/blob/main/Screenshots/Re-Order%20Point%20&%20VLOOKUP%20sheet%20pt%203.png?raw=true"></img>

<h4>Current Stock On Hand column:</h4>

Syntax: 
<code>=xlookup(lookup_value, lookup_array, return_array,[if_not_found],[match_mode],[search_mode])</code>

I typed: 
<code>=XLOOKUP(I4,A:A,E:E,"SKU Not Found",0)</code>


The lookup_value is what you would type in the SKU input cell (cell I4).

Within the <code>XLOOKUP</code> function, let the [match_mode] value equal to 0, which means to return exact match.



