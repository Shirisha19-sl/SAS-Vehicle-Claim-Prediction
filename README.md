# Vehicle-Claim-Prediction

## Introduction:
In the competitive landscape of the insurance industry, accurately predicting car insurance claims is crucial for enhancing profitability and customer satisfaction. This project focuses on developing a predictive model to determine the likelihood of a policyholder filing a claim within the next six months based on the car insured.
The second-hand dataset used for this project from Kaggle, with around 40 columns and more than 50k records, includes comprehensive information about the policyholders, encompassing various attributes such as policy tenure, age of the car, age of the car owner, population density of the policyholder's city, and specifics of the car including make, model, power, and engine type. These features provide valuable insights into both the vehicle's characteristics and the policyholder's environment, allowing for a robust analysis of the factors influencing claim likelihood.
By leveraging this data, the project aims to identify key risk factors and patterns that can be used to inform business decisions such as premium adjustments, underwriting policies, and customer engagement strategies.

## Dataset Link
- <a href="https://www.kaggle.com/datasets/ifteshanajnin/carinsuranceclaimprediction-classification/data?select=train.csv">Dataset</a>

## Data Exploration
The second-hand dataset used for this project from Kaggle, with around 40 columns and more than 11k records, includes comprehensive information about the policyholders, encompassing various attributes such as policy tenure, age of the car, age of the car owner, population density of the policyholder's city, and specifics of the car including make, model, power, and engine type. 
These features provide valuable insights into both the vehicle's characteristics and the policyholder's environment, allowing for a robust analysis of the factors influencing claim likelihood.
Is_claim – A binary variable indicating whether the policy holder file a claim in the next 6 months or not.
Based on the output of the stat explorer node, can see below observations:
There are no missing values in both class and interval variables.
Skewness of the variables is very minimal which means the data doesn’t have much outliers.
Can see no abnormalities in values based on the minimum and maximum for each variable.
No imputation or handling outliers is needed.

## Data Partition 
The data is partitioned into 70% training data and 30% validation data. 
We do this using a Data Partition node with training and validation evenly distributed with the target values.

## Model
#### Logistic regression
Add the logistic regression node to the data partition node and analyze the results. 
We have used stepwise algorithm as our selection model. The stepwise selection method starts with an intercept and iteratively adds the predictors to the model based on their significance levels.
The selected model is the model trained in the last step (Step 5). It consists of the following variables:
age_of_car
area_cluster
Policy_tenure
Based on the results as seen, The mean squared error (MSE), which indicates the difference between predicted and actual values, is 0.23. This suggests that, on average, the model's predictions deviate from the actual values by this amount.
The misclassification rate represents the portion incorrectly classified observations is 0.37 for both the training and validation sets approximately which suggests 37% are misclassified.
The Precision and accuracy of training data using the event classification table is 51.7% and 63.8% respectively, whereas for validation they are 49.1% and 63.4% respectively

<img width="324" height="224" alt="lr 2" src="https://github.com/user-attachments/assets/8de3218e-c619-413d-92f4-3b7c3ae20cac" />

#### Decision Tree
The algorithm has used “Policy Tenure” for the first split which is seen in tree and based on the results, we see that the training data is approximately misclassified by 36% and the validation data is approximately 35%. The average squared error is 0.22 and 0.22 respectively for the training and validation data.
Based on the event classification table, the precision and accuracy is 62.8% and 63.4% for training, on the other hand for validation it is 66.6% and 64.78%. 

<img width="215" height="195" alt="DT 1" src="https://github.com/user-attachments/assets/b63b08a1-4249-4212-8e80-ba69855de117" />

<img width="337" height="180" alt="DT 2" src="https://github.com/user-attachments/assets/cc37c6b0-c069-49dc-ae95-66b0ed731775" />

#### ANN
ANN node to the data partition node and analyze the results.  
Considering the following hyper parameters in properties. 
Maximum Iterations :30
Number of Hidden units :8
Total number of hidden nodes :30
Activation Functions: Tanh, Logistic, Sine.
The misclassification rate for validation is 0.36 and for training it is 0.34. 
Based on the classification table, precision and accuracy of the validation data is 52.3% and 64.4%.

<img width="226" height="204" alt="ANN 1" src="https://github.com/user-attachments/assets/4d7ecc47-2627-4e69-bcdc-d96b6b12561a" />


The plot displaying the misclassification rate for the neural network shows that the model has chosen the 8th training iteration as the optimal stopping point. Although the training misclassification rate continues to decrease, the validation misclassification rate begins to increase slightly, indicating potential overfitting

<img width="411" height="171" alt="ANN 2" src="https://github.com/user-attachments/assets/3ab9d598-fdb5-4388-8a3a-0b460a5da8cf" />


## Model Comparison
In this project, multiple models were developed to predict claims. To identify the best-performing model, we used the model comparison node, evaluating each model based on the misclassification rate on the validation dataset.
The results from the model comparison node show that the Decision Tree model achieved the best performance, with a validation misclassification rate of 0.35, translating to an accuracy of approximately 65%. The Artificial Neural Network (ANN) model also performed comparably, with accuracy close to that of the Decision Tree.

<img width="960" height="192" alt="Model Comparison" src="https://github.com/user-attachments/assets/91cd3ba4-49b0-4004-9da6-cc3b15dea93d" />

## Business Value
Predicting car insurance claims based on a comprehensive dataset adds considerable business value by enhancing pricing accuracy, improving underwriting and claims management, and supporting strategic decision-making. This leads to greater profitability, operational efficiency, and competitive advantage in the insurance market.
This prediction not only enhances the precision of underwriting processes but also contributes to the development of personalized insurance products, ultimately driving customer loyalty and operational efficiency.
Improved pricing accuracy enhances profitability and competitiveness in the market while ensuring customers are charged fairly based on their risk profile.
We can see that the variables like age_of_car,  policy tenure, area_cluster and displacement (engine capacity in CC) play a major role in claim prediction.
By analyzing these variables, insurers can better tailor policies, pricing, and risk management strategies to suit the needs and risk profiles of customers in specific geographic regions.

## Conclusion
The fact that different models all have similar misclassification rates suggests that there may be limitations in the data itself, as different algorithms are unable to find substantially different patterns.
Insufficient predictive features: The current features might not capture enough information to differentiate claim vs. no-claim events well.
Overlapping Data Patterns: If the features for claim and non-claim cases are similar, it will be challenging for models to separate them accurately.
Potential Data Imbalance: If there is a significant imbalance between claim and non-claim cases, the models might struggle to learn patterns for the minority class (often claims), leading to poor predictive performance.
Features such as below might provide more insights 
Behavioral Features: Information on policyholder behavior, such as driving frequency, speed, or past incidents, could provide valuable insights but might be missing.
Environmental Factors: Factors like weather conditions, traffic congestion, or road safety features in the policyholder’s area could influence claim likelihood.
Detailed Claim History: If available, historical claim details like claim amount, type, and frequency would help in understanding the risk profile of policyholders.
Vehicle Condition and Usage Patterns: Information on the car’s condition, mileage, and usage pattern (e.g., for work, leisure, or commuting) can impact the probability of a claim.


