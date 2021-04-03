# Unengaged Users
It's a data science project with an aim to identify less involved customers using both unsupervised and supervised learning algorithm.

# Description

The aim of the project is to build a machine learning model to identify the unengaged users in Fin Tech industry to help them implement business actions to convert them to engaged users.

# Datasets

There were three datasets made available to us.
- Monthly Market details
- Monthly transaction
- Transaction details

# Walkthrough 

The solution has been built over Python using Pandas and Machine Learning models.

<b>Performed:-</b>
- Profiling
- Tableau Visualization
- Understanding
- Data Transformation
- Clustering
- Preprocessing
- Data Split
- Model Building and the best Model Selection


<b>Profiling:-</b>

On generating the profile report over the datasets, we gathered the below observations.

Monthly Market details: 
- It’s comprised of customer demographic columns like user id, country, user creation date, plan type, etc.
- Out of 43 columns, there’re 24 categorical and 19 numerical with total no of observation being 143316.
- It has 99154 missing cells distributed among columns “attributes notification marketing email” and “attributes notification marketing push”.
Monthly transaction:
- It’s comprised of columns like user id, transaction currency, transaction type, etc.
- Out of 43 columns, there’re 24 categorical and 19 numerical with total no of observation being 143316.
- It has 99154 missing cells distributed among columns “attributes notification marketing email” and “attributes notification marketing push”.
Transaction details:
- It’s comprised of columns like user id, amount_usd, transaction type, etc.
- Out of 65 columns, there’re 1 categorical and 64 numerical with total no of observation being 143316.
- It has 22794 missing cells in a column amount_usd.


<b>Tableau Visualization:-</b>

The dataset is visualized over tableau to answer the below questions. The respective solutions is made available for preview at "https://public.tableau.com/profile/shreeya6445#!/".

1. What can be inferred from the distribution of the total amount_usd transactions across different transactions_state? 
2. Which transactions_type has been most beneficial to ParTech monetarily
3. Which type of transactions has the highest amount_usd of non-COMPLETED transactions? 
4. How does the count of new joiners and the total number of transactions by the new joiners vary across time (day-level)? 
5. What does the overall distribution of distinct users across different countries look like on the world map? 
6. What does the average birth_year of users across different countries look like on the world map?
7. Which plan_type is most popular among the users? 
8. How does the average distribution of each plan_type vary across yearmonth?
9. What is the total number of SENT and FAILED notifications across yearmonth? 
10.What does the box-plot distribution of amount_usd and tx_count across yearmonth tell us about the outliers? 
11.What inferences can be drawn based on average distributions of each transaction direction and transactions_type across ‘yearmonth’s?


<b>Understanding:-</b>
- The dataset is missing the target variable to classify the feature as unengaged or engaged user.
- The dataset needs to be transformed prior clustering for customer segmentation.

<b>Data Transformation:-</b>
- Utilized transaction details dataset along with Monthly market dataset.
- On Monthly market dataset imputed the missing value with the most frequent.
- As transaction  dataset and it has no missing value, check the proportion distribution of the column transaction state.
- Out of 27lakh entries 24lakh entries were of the completed transaction.
- As the customer who completes the transaction will be beneficial. Hence will be focusing on the transactions where the transaction state is completed.
- Considering 2018, as the observation time-period filtering the year 2018 from the completed transactions data.
- Transformed the column user_created_date,created_date  into datetime and then granularized it multiple columns like day, month, year, yearmonth.
- We aimed to build a new dataset from the existing in such a way that there’s a unique entry per user id for three month average.
- It has been attained using group by operation on column user_id.
- Using Aggregation, four new columns were generated.
- Number of transactions (Use count of amount_usd)
o	Total USD value of transactions (Use sum of amount_usd)
o	Total distinct types of transactions (Use transactions_type)
o	Total distinct days of transactions (Use created_date)
- The result of the four group by and aggregations were converted into dataframe and joined into one dataset using user_id as a common index.
- The tenure was calculated and applied on each of the four columns.
- As we remained with only numerical column to process upon, applied StandardScaler as a preprocessing technique.


<b>Clustering:-</b>
- Using Elbow graph identified 2 cluster needs to be formed.
- KMeans cluster algorithm has been applied on the scaled data frame and the result has been predicted for the same.
- The predicted result is appended to the scaled data frame as a column.
- On visualizing the predicted result against various column of agg we came to conclusion, class 1 belongs unengaged user whereas class 0 to engaged users.
- When the cluster prediction was visualized over yearmonth, we identified the strength of unengaged user is more than the engaged users. Hence imbalanced proportion.

<b>Preprocessing:-</b>
- As we are already working on the scaled data, I checked for correlation next.
- Distinct_Days_Count was highly correlated, hence dropped the column

<b>Data Split:-</b>
- Training data - 80% till 201809
- Validation data 1 (out-of-sample) - 20% till 201809 
- Validation data 2 (out-of-time) - 201812 
- Scoring data – 201901

<b>Model Building and the best Model Selection:-</b>
-  Train, tune and validate an XGBoost and Logistic Regression classification model.
-  Both model performed exceptionally well with recall and f1 score on both classes being 90% above.
-  But I choosed XGB or LogisticRegression  as LR was inaccurate by 2% in comparison with XGB's recall.
-  XGB gave an average F1 score of around 95%.
-  When predicted over scoring data, F1 score for class1 was 97% whereas of class0 was 92%.

