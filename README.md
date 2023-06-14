# Bank Deposit Customers

A certain bank has done marketing campaign to get customers deposit their money. Customers profiles and marketing data are gathered to determine which customers will likely to deposit after exposed to campaign. A data scientist was hired to develop machine learning model to predict which customers will deposit, as identified customers will be prioritized to follow up.

We want to classify if a prospective customers will deposit or not. There are 10 features, which are:
Customer profile
-	age
-	job
-	balance
-	housing
-	loan

Marketing data
-	contact: Contact communication type.
-	month: Last contact month of the year.
-	campaign: Number of contacts performed during this campaign and for this client.
-	pdays: Number of days after the client was contacted from the previous campaign.
-	poutcome: Outcome of the previous marketing campaign.
-	deposit: Whether the customer deposits or not.


# Confusion Matrix

- True Positive: Predicted to deposit and actually deposit

- False Positive: predicted to deposit and actually not deposit

- True Negative: predicted to not deposit and actually not deposit

- False Negative: predicted to not deposit and actually deposit


from this breakdown, we can identify **False Negative is more costly** because it would mean unfulfilled revenue. <br>
While false positive is less costly because operational cost is not much different and also part of sales job.

But when prioritizing recall in developing model, the number of false positive equals to true positive. The model identifies customers as deposit to minimize false negative and resulted in 1:1 ratio. This is not a helpful model because it has the same possibility of randomly contacting customers from database (47% customers deposit from entire database).<br>

instead, we are going to use **precision**, because reducing false positive would lead to higher model trustworthiness (model predict deposit customer more accuratte). We want the model to predict positive class with high accuracy so those predicted to deposit will be prioritized to be contacted. The result would be a faster conversion and customers goal earlier. 

## Data Preparation
This phase include checking missing value, class imbalance checking, replacing nonsense values, binning age, multicollinearity check. Next is preprocessing phase which include scaling for numerical data, encoding for categorical data.

This model also used forward feature selection to check if all features relevant. The result was all features are required to predict best outcome.

## Modelling

Cross validation was done to get best base model. I tried 37 model which include variations of polynomial degree and Naive Bayes, voting, SVC, Gradient Boosting, Logistic Regression, Stacking, Adaboost, Decision Tree, XGboost, random forest and K-NN.

The best result was Naive Bayesian

## Tuning

Naive Bayesian variable to be tuned are var smoothing, scaler for numerical data.

## Result

True positive predicton rate is 329 / (329 + 87) = 79 % --> Which means we can reach converted customer goal faster using this model instead of randomly picking from list (only 47% of entire customers will deposit from entire database)

once we have contacted all of predicted deposited customers, we can move on towards predicted  negative customers. False negative rate is 417 / (417 + 728) = 36% --> Meaning there is 36% chance to get deposit customers picking randomly, 11% lower from before using model

In conclusion, we can reach customer goal earlier instead of hurrying to catch up at the end of quarter using this model.

## Cost Calculation

- Based on research,  cold calls should lasts 5 minutes and costs Rp 636/30s. So per call should cost Rp 10,600. But we only counts failed calls for sake of simplicity.
- Before this model, probability for customers to NOT deposit is 53%. So expected cost per call is : 53% x 10,600 = Rp 5,618
- After this model, probability for customers to NOT deposit is 21%. So expected cost per call for predicted positive group is :  21% x 10,600 = Rp 2,226


- Lets assume quarterly goal for deposit is 650
- before this model the expected cost would be 5,618 x 650 = Rp 3,651,700


- After this model, we contact predicted positive class so the cost would be : 2,226 x  416 (from entire predicted positive class) = Rp 926,016
- Then we proceed to get remaining customers (234 people) from negative predicted customers: 234 x (64% x 10,600) = Rp 1,587,456
- total cost after the model: 926,016 + 1,587,456 = Rp 2,513,472

- Our model saves 3,651,700 - 2,513,472 = Rp 1,138,228 or decrease spending by 31%



## K-Means

We use clustering method to identify audience tendencies based on age and balance. This can help develop focused strategy for each group.

Based on the clustering result, we can conclude that there are 2 different groups in our database.


Group A is for people that has balance less than certain amount. We can categorize these group as less financially-savvy.


Possible strategy for this group are:

- emphasize of guaranteed return and safety. Because they are less likely to know much regarding finance.

- easy process to deposit. Because they feel safer if they understand the know-how.

- transparancy of deposited balance. Because they can be assurred their money is there.

- Group B is for people that has balance more than certain amount. We can categorize these group as more financially-savvy.

Possible strategy for this group are:

- emphasize on interest rate higher than inflation. Since they are financially literate.
- safe from loss. To avoid loss instead of investing in stock or other financial choice.
- Personal approach since trust is key difference for people with more money
