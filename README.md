# credit-card-defaulter
# problem statement: 
  To build a classification methodology to determine whether a person defaults the credit card payment for the next month.

# data
The data contains 32561 instances with the following attributes:
Features:

⦁	LIMIT_BAL: continuous.Credit Limit of the person.
⦁	SEX: Categorical: 1 = male; 2 = female
⦁	EDUCATION: Categorical: 1 = graduate school; 2 = university; 3 = high school; 4 = others
⦁	MARRIAGE: 1 = married; 2 = single; 3 = others
⦁	AGE-num: continuous. 
⦁	PAY_0 to PAY_6: History of past payment. We tracked the past monthly payment records (from April to September, 2005)
⦁	BILL_AMT1 to BILL_AMT6: Amount of bill statements.
⦁	PAY_AMT1 to PAY_AMT6: Amount of previous payments. 

# Target Label:
Whether a person shall default in the credit card payment or not.
⦁	default payment next month:  Yes = 1, No = 0.

# Model Training 
1) Data Export from Db - The data in a stored database is exported as a CSV file to be used for model training.
2) Data Preprocessing   
⦁	Check for null values in the columns. If present, impute the null values using the categorical imputer.
⦁	Scale the numeric values using the standard scaler.
⦁	Check for  correlation.
3) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of 
  clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, 
  we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
  The Kmeans model is trained over preprocessed data, and the model is saved for further use in prediction.
4) Model Selection – After the clusters have been created, we find the best model for each cluster. We are 
  using two algorithms, “Naïve Bayes” and "XGBoost". For each cluster, both the algorithms are passed with 
  the best parameters derived from GridSearch. We calculate the AUC scores for both models and select the model 
  with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction.

# Prediction 
1) Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
2) Data Preprocessing  :  
⦁	Check for null values in the columns. If present, impute the null values using the categorical imputer.
⦁	Scale the numeric values using the standard scaler.
⦁	Check for  correlation.
3) Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.
4) Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.
5) Once the prediction is made for all the clusters, the predictions along with the Wafer names are saved in a CSV file at a given location, 
    and the location is returned to the client.
