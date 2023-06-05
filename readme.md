# DA/ML project brief
Manage credit cardholders who might potentially default on their outstanding balances, earlier in the customer life cycle.

# Requirements
1. Use a classification model to predict defaulters
2. Use a clustering algorithm to focus on higher-priority customers.
3. Use design thinking to come up with targeted interventions to minimize chances of outstanding default

# Overview
## Classification using XGB
For classification, I used a **XGBoost Classifier** with hyperopt parameter tuning for best F1 score, because the classes for default vs non-default are imbalanced, and optimizing for F1 score will be more suitable than accuracy.

After training and tuning the XGB model, I used it to predict probability of default for customers in the test set.
Then, for each customer, their **default importance** is calculated as **default probability * outstanding balance** (total bills - total pay amounts for the past 6 months). This gives us the default importance of each customer in the test set.

## Clustering using K-Means to define high priority segment
For clustering, a K-Means algorithm was used over hierarchical clustering because I waned to set the number of clusters to 3. Based on the cluster with the highest mean default importance, we analyzed the customers' demographics. A higher proportion of the customers in the high priority segment were: married, age 30s, university-educated; compared to the other 2 segments.

## Optional segmenting: sorting customers by default importance
Because the customer's default importance (outstanding balance * default probability) has been calculated, we can sort them in descending order => higher default importance customers will be at the top. 

This way, we can choose to target the 90th percentile (top 10 percent of the customers by default importance). This will help us to maximize the outstanding balance collected. Pls refer to the notebook for details.

(Assuming that all customers will react to the interventions in the same manner, i.e. will repay their default balance.)


## Design thinking
Based on the demographics data, together with user research/interviews, our group came up with a customer persona and targeted solutions: repeated notifications with clearer messaging, 1-click easy payment, and automated payment scheduling. Pls refer to the pdf for more details.


## Suggestions for improvements
We are assuming that all customers will react to the same degree to our interventions. However, this is unlikely in real life. If we are able to collect data on the customers that respond to the interventions, we can perhaps use another model to predict who are the more responsive customers, and consider this factor (responsiveness to payment notifications, etc) to optimize our solution.






