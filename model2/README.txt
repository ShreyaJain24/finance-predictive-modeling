########################### Retrieving data from database ######################

Notebook: database_read.ipynb


########################### EDA ######################
Notebook: data_analysis.ipynb

EDA 1:

1. Mutiple geo-coordinates(long and lat) are present for each user. In order to consolidate all the coordinates information at a user-level, the most frequent coordinates are considered. 
2. Decimal points of the coordinates have been removed as these points need to be catgeorical. Letting the points be as continuous variables would be incorrect. We are losing some precision on the points but this done to keep the cardinlaity of the now categorical feature in check.
3. Most frequent provider is taken against each user
4. Additional attribute - No of gps datapoints against each user as a continuous feature

Comments: 
-As not many unique lats and longs. Use the direct value as categories. Can't use them directly as not a numerical feature


Observations after running Statistical tests on the processed input: 
1. Long and lat values are highly correlated, as not many coordinates are present.
2. No other correlations observed.
PS: Pandas profiling report on EDA1: Branch_profiling_report_1.html



EDA 2: 

1. After analysing frequency distribution of altitude feature - it's categorised into 2 buckets. Low and high altitudes.


Stats: 
1. We observe a slight correlation betwwen location_provider and altitude 
PS: Pandas profiling report on EDA2: Branch_profiling_report_2.html




EDA 3:
1. Adding age and cash_incoming_30days attributes from the user_attributes. 
PS: Pandas profiling report on EDA3: Branch_profiling_report_3.html


########################### Model building ######################
Notebook: model.ipynb

1. Categorical attrbutes are converted to one hot encoded vectors. Dataset is split into training and test sets
2. As the dataset size is low, instead of using direct discriminatory models, I first used Random forest. It's easy to control overfitting in Random Forest as opposed to a Decision tree and is explainable 
3. Model analysis: 
a) getting an accuracy of 0.71 with good enough precision and recall values. Can check the recall and precision scores on the notebook
b) Checked the distribution of predicted probabilities on the test set for the confidence in the predicted classes. 
c) ROC curve is plotted to check TPR and FPR for the right threshold.


4. Experimented with a probabilistic generative model as well ith Naive Bayes. It runs with an accuracy of 0.63. 
5. Tried SVC with kernel for non-linear decision boundaries. But it's overfitting the data.
6. Pickled and saved the model 

########################### Model API ######################

model_api.ipynb

1. Created a simple api in Flask framework. Running the api on a separate shell and sending requests from the notebook.


########################### Future tasks ######################

1. A better way to use coordinates information by checking for public information available online at the coordinate level. The information can range from population of the district, urban/rural area, GDP metrics at the district level, major source of revenue of the district, etc. 

2. Using timestamp information as the difference between the application and gps collection time

