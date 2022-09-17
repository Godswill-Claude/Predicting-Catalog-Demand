# Predicting-Catalog-Demand

Overview 

This project aims to enable the management of a company to determine if it should send a catalog list to a number of new customers and if it would be a good business decision to do so. A historical dataset (p1-customers.xlsx) was used to build a linear regression model, which was then applied to the new dataset (p1-mailinglist.xlsx) and used to predict the potential profit of sending out the catalog for the 250 new customers
The software applications used for the entire analytical process and model building are Excel and Alteryx. 
The following steps were taken to get the desired results.
Step 1: Business and Data Understanding
Ultimately, the company needs to decide whether or not it should send a catalog to the 250 new customers.

To make this decision, the company needs to determine how much money it can expect to earn from sending out a catalog to the new customers. It needs to predict the potential profit of sending out the catalog. The expected profit contribution must exceed $10,000, otherwise the catalog will not be sent out.

To make this prediction, we need a historical dataset (p1-customers.xlsx) to build a linear regression model, which will then be applied to the new dataset (p1-mailinglist.xlsx) and used to predict the potential profit of sending out the catalog for the 250 new customers.

From the p1-customers.xlsx data set, we can initially assume the followings:
Target variable: Average_Sale_Amount
Predictor variables: Name, Customer_Segment, Customer_ID, Address, State, City, Zip, Store_Number, Avg_Num_Products_Purchased, #_Years_as_Customer.

NB: Because the field Responded_to_Last_Catalog is only contained in the p1-customers.xlsx but not in the p1-mailinglist.xlsx, it was not used in the linear regression model since it could not be applied to the mailing list data set.


Step 2: Analysis, Modeling, and Validation
Customer_ID, Zip, Store_Number, Avg_Num_Products_Purchased, #_Years_as_Customer are all numeric variables. Hence, scatterplot was used to check their usefulness in predicting the target variable. The followings were discovered:

•	The scatterplot of the predictor variable Avg_Num_Products_Purchased versus the target variable Average_Sale_Amount shows a sloped line. More so, the linear regression trial shows a p-value of 2.2e-16 (which is far less than 0.05) and with three stars to the right Hence, a strong linear relationship exists between the predictor variable Avg_Num_Products_Purchased and the target variable and will be used in the model.

•	The scatterplot for the rest of the numeric variables (Customer_ID, Zip, Store_Number, #_Years_as_Customer) versus the target variable Average_Sale_Amount show no slope. Hence, no linear relationship exists between these variables and the target variable. More so, investigations carried out by plugging these variables into the linear regression tool gave p-values greater than 0.05 with no stars to the right.  As such, they are not good predictor variables for the target variable and will not be included in the model.
 

As for the categorical variables Name, Customer_Segment, Address, State and City, the linear regression tool in Alteryx was used as a trial-and-error measure to determine which is/are statistically significant, one after the other, and the following results were obtained:
	For Name, the p-value is 0.7512 (which is greater than 0.05) and with no stars. Hence it is not statistically significant.
	For Customer_Segment, the p-value is 2.2e-16 (which is far less than 0.05) and with three stars to the right. Hence it is very much statistically significant.
	For Address, the p-value is 0.318 with no stars, which is greater than 0.05. Hence it is not statistically significant.
	For City, the p-value is 0.8374 with no stars, which is greater than 0.05. Hence it is not statistically significant.
	The variable State could not run in Alteryx, and looking at the fact that there is no variation in its values both in the historical data set and the dataset to be predicted, we can safely conclude that it is not statistically significant.


Conclusively, the only two statistically significant predictor variables that were used to build the model are: Avg_Num_Products_Purchased and Customer_Segment.

Fixing in and running the linear regression tool in Alteryx using these two predictor variables, the following regression formula (or model) was obtained:
Average_Sale_Amount = 303.46 + 66.98(Avg_Num_Products_Purchased)
– 149.36(Customer_SegmentLoyalty Club Only)  
+ 281.84(Customer_SegmentLoyalty Club and Credit Card)  
– 245.42(Customer_SegmentStore Mailing List)  
+ 0 (Customer_SegmentCredit Card Only).

Looking at the statistical results from the model, it can be seen that the p-values of all the predictor variables used to build the model are all 2.2e-16 (which is far less than 0.05) and all with significance codes ***. Hence, the predictor variables are all statistically significant, and we can leave them all in. The Multiple R-squared is 0.8369 and the Adjusted R-Squared is 0.8366 (which are all close to 1). All of these indicates a very strong model with which a Data Analyst should be confident of making reliable predictions.


Step 3: Presentation/Visualization
	Using a score tool, I was able to get the predicted sales amount per customer.
	Next, using a scatter plot tool, I observed the correlation between the score (or predicted sales amount) versus the Avg_Num_Products_Purchased (the best numeric variable in the model), and I noticed a very strong positive correlation.
	Then using a formula tool, I computed the expected revenue per customer as Expected_Revenue = [Score_Yes] × [Score].
	Next, I used a summarize tool to sum up all the expected revenues for all 250 customers. This gave $47,224.8713.
	Finally, using another formula tool, I calculated the final profit that can be accrued from sending a catalog to the 250 customers as follows:

Profit = (Sum_Expected_Revenue × 50% average gross margin) – (6.50 costs of printing and distributing per catalog × 250 customers)
 
= $ 21987.4356865455
	
Since the company will only send out the catalog if the expected profit exceeds $10 000, and the trusted model here is predicting a profit more than twice this amount, I would strongly recommend that the company sends out the catalog to the 250 new customers. 
 
