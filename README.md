# Project-Capstone-Modul-3
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
