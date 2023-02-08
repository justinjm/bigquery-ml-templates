---
source_url: "https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub"
---
# BigQuery ML Marketing Templates

(Documentation for [https://github.com/GoogleCloudPlatform/bigquery-ml-templates](https://www.google.com/url?q=https://github.com/GoogleCloudPlatform/bigquery-ml-templates&sa=D&source=editors&ust=1675884463741174&usg=AOvVaw25RkE5q2AMgNnVpNLettKH), Apache v2 license)

##

[Overview](#overview)

[Data Schema](#data-schema)

[Modeling Introduction](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.53t9g2apqu3s)

[BigQuery ML Features](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.q9wk00m9ryl9)

[Customer Segmentation](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.xagjfebkoa2h)

[Modeling Steps](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.6erdstecp6r1)

[Results](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.ebmx5ebijjl9)

[Customer Lifetime Value](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.fbocmmbe035p)

[Modeling Steps](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.ka8wyn6chun7)

[Results](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.g2qjb6b986zg)

[Conversion/Purchase Prediction](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.f63c1olsyrgn)

[Modeling Steps](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.tp0t8luirgg8)

[Results](https://docs.google.com/document/u/1/d/e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb/pub#h.k9maya2vfzbm)

##

## Overview

This document contains BigQuery ML templates for common marketing use cases. The templates use synthetic data, which was generated as per below use case and schema.

* Customer is a B2B office supplier: OS Inc
* OS Inc's customers are businesses whose information is stored in CRM in Account object
* End users of these businesses login to OS's ecommerce website to order supplies; End user information (demographics, etc) is stored in the User object in CRM
* Website activity of each user is tracked in GA360

Though these templates are based on a fictitious B2B company, the modeling techniques and methods apply equally to a B2C scenario as well.

Here are the three use cases:

1. **Customer Segmentation** is the practice of dividing a customer base into groups of individuals that are similar in specific ways relevant to marketing, such as age, gender, interests and spending habits. Segmentation allows marketers to better customize their marketing efforts to various audience groups.
2. **Customer Lifetime Value (LTV)** is an important metric used by businesses to measure the total revenue that they can reasonably expect from a customer. It is used by these organisations to identify and prioritize significant customer segments that would be most valuable to the company.
3. **Conversion/Purchase Prediction** predicts if a user “converts” or “purchases”, which in this case is defined as someone signing-up for a membership program that the company offers. Membership has a cost but provides additional benefits e.g. free shipping. It is in the company's interest if many users sign up for this membership as it helps streamline their operations and also helps with recurring revenue.

## Data Schema

The below diagram shows how data from a CRM system and GA360 is brought together in BigQuery. In practice, this data usually sits in different silos in companies and integrating all that data together is a critical first step to enable any ML or analytics.

![](https://docs.google.com/drawings/d/svCHqYE_45j22w7HG1ahgVg/image?parent=e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb&rev=39&drawingRevisionAccessToken=AwSStuygKMvlKw&h=526&w=624&ac=1)

Here are the list of all fields:

**Accounts** | **Users**  | **GA360**

---------- | ---------- | ----------
Account ID | User ID    | User ID
Account Number | Gender     | Last Visit
Account Source | Loyalty Program | Visit ID
Annual Revenue | Lifetime Value | Visit Start Time
State Code | City       | Time On Screen
Country Code | Age        | Time On Site
Channel Program Name |            | Unique Screen Views
Industry   |            | Medium
Name       |            | Browser
Number of employees |            | Screen Resolution
Ownership  |            |
Rating     |            |
Site       |            |
Type       |            |
Year Started |            |
Total Opportunity Amount |            |
Date of First Sale |            |
Date of Last Sale |            |
Average Sales Cycle |            |
Number of Renewals |            |
Num Opportunities Won |            |
Num Opportunities Lost |            |

The data files matching above schema are available as csv files in the git repository. It is suggested that the user let BQ auto-detect the schema when ingesting these csv files. Please select the options shown in the picture while uploading a table to dataset in bigquery. Note that BigQuery automatically uses the first row in the dataset as column names.

![](https://lh5.googleusercontent.com/O7ACgXXZ70gqgmJvwxdb7hueLO314Hj3sQVU3Pg6jIW9HezL-7YQ8EFj8ZtJvPdAkDxjaR6p9Rw4nbL4DP1RHExM0YBJv79uZ3B8iyh51c5eNMysxaJIdGFWSk-9tdlvEwgpK7Kis3BBSddZaw2Xcw)

## **M****odel****ing Introduction**

Selecting features is an important aspect of any modeling exercise. Models rarely perform well when all available columns are fed to it. For example, ID columns (e.g. user ID) are random, and can even hurt the model. Careful feature selection and feature engineering (act of transforming data columns to get the most out of them) can improve the accuracy of a model.

Here are some things to keep in mind when selecting features.

1. Use your domain knowledge and knowledge of your data to identify the columns that you think have an impact on the model.
2. After data exploration, include those columns that exhibit non-random patterns. For example, those columns that follow a normal distribution often make for good features.
3. Perform feature engineering to improve accuracy, e.g. bucket revenue into individual bins, extract weekday/weekend from dates, etc.

Creating charts (histograms, line charts, etc.) are the most common ways of exploring data. Here are a couple of examples.

![](https://lh4.googleusercontent.com/rSJz5SsfMwqXS5kgLUuQn1sbPLfgMmfUYKGICEvApdWbjBq0HRw5a6BwmihSzkj0lD5TEni5-uSauY2wPBh8I7v7NPKsX_BbIOAD2ZFJu1y2pQIWMdCA-BQjW51vaWpHEo4pTyp6UTc43reV16NKYA)

Here are the steps involved in modeling:

1. Select features
2. Build the model
3. Evaluate the model
4. Repeat steps 1-3 until desired accuracy is achieved

In a real world scenario, it is very likely that some amount of data engineering or cleansing will be required. Here are some common techniques:

1. Removing outliers
2. Imputation of null values - this is automatically handled by BigQuery ML
3. Transformations such as log transformation, z-scaling, etc
4. Binning (bucketizing) values into certain groups

## **BigQuery ML** **Features**

BigQuery ML handles some common feature creation and machine learning tasks. Below is what you do not need to worry about. Please read the [documentation](https://www.google.com/url?q=https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create&sa=D&source=editors&ust=1675884463768164&usg=AOvVaw2pCGpEgjSuy1PgEeKKPQiW) for more details on these.

* Auto-tuned learning rate for regression models
* Auto-split of data into training and test for classification and regression models, to prevent over-fitting. There is no split for clustering, as it is an unsupervised model without labeled data. Default split is random 80/20, there are options to change the split strategy and fraction.
* Standardization of numeric features
* One-hot encoding of strings to create numeric features
* Null imputation: Nulls during training and prediction are treated as a category for categorical features, and imputed to the mean value for numeric features.
* Class imbalance handling: If there are rare classes in the data, the weights for regression models are automatically scaled.

## **Customer Segmentation**

Customer segmentation is the practice of dividing a customer base into groups of individuals that are similar in specific ways relevant to marketing, such as age, gender, interests and spending habits. Segmentation allows marketers to better customize their marketing efforts to various audience groups.

K-means clustering is an unsupervised learning modeling technique, typically used for such segmentation. In this example, we segment customers based on CRM and GA360 data.

This diagram shows a high level view of the iterative modeling process.

![](https://docs.google.com/drawings/d/shItteY6cUPEZQybH9vRxpA/image?parent=e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb&rev=6&drawingRevisionAccessToken=Oct7svaogFFNfQ&h=247&w=624&ac=1)

Here are the list of features used, along with the applied feature transformations.

**Field**  | **Description** | **Feature Engineering**

|---------- | ---------- | ----------|
Annual Revenue | Annual Revenue of the account of the user | Binning into small, medium and large. This was done to simplify interpretation of this column’s impact on clusters.
| Time On Screen | Total time spent by user on screen | Aggregated from GA360 data
| Unique Screen Views | Total number of screens viewed by the user | Aggregated from GA360 data
| Loyalty Program | Loyalty program for the user |
| Lifetime Value | Lifetime value of the user in the account |
| Age        | Age of the user |

### Modeling Steps

The first step is to aggregate to GA360 data [customer_segmentation_sql/data_aggregation.sql].

SELECTUser_ID,<br>SUM(timeOnScreen) AS timeOnScreen,<br>SUM(UniqueScreenViews) AS UniqueScreenViews<br>FROM`yourprojectid.yourdataset.GA360`GROUP BYUser_ID

The SQL query to select the data from various tables and create view for model training[customer_segmentation_sql/feature_selection.sql].

SELECT`yourprojectid.yourdataset.Users`.User_ID,<br>`yourprojectid.yourdataset.Accounts`.Account_Number,<br>`yourprojectid.yourdataset.Accounts`.Annual_Revenue,<br><br>`yourprojectid.yourdataset.Aggregated_GA360`.timeOnScreen,<br>`yourprojectid.yourdataset.Aggregated_GA360`.UniqueScreenViews,<br>`yourprojectid.yourdataset.Users`.Loyalty_Program,<br>`yourprojectid.yourdataset.Users`.Lifetime_Value,<br>`yourprojectid.yourdataset.Users`.Age<br>FROM`yourprojectid.yourdataset.Aggregated_GA360`,<br>`yourprojectid.yourdataset.Users`,<br>`yourprojectid.yourdataset.Accounts`WHERE`yourprojectid.yourdataset.Aggregated_GA360`.User_ID = `yourprojectid.yourdataset.Users`.User_ID<br>AND <br><br>`yourprojectid.yourdataset.Accounts`.Account_Number = `yourprojectid.yourdataset.Users`.Account_ID<br>ORDER BY`yourprojectid.yourdataset.Users`.User_ID ASC

Here is the SQL command to train the model [customer_segmentation_sql/model_train.sql].

CREATE MODEL `yourprojectid.yourdataset.my_model` OPTIONS(model_type='kmeans',<br><br>num_clusters=9,<br><br>distance_type='euclidean')<br><br>AS SELECT <br><br>Annual_Revenue,<br><br>timeOnScreen,<br><br>UniqueScreenViews,<br><br>Loyalty_Program,<br><br>Lifetime_Value,<br><br>Age<br><br>FROM <br><br>`yourprojectid.yourdataset.data`;

Distance type is Euclidean by default, if not specified. The training of the K means clustering model happens iteratively with loss being calculated at each step. The loss calculation is done by finding the total distance of the data points from the centroid of their assigned class. The model training stops when the change in the loss is less than a threshold.

****

**Evaluate the model**

Accuracy of the model is determined using an evaluation run on the data. The command to perform this evaluation is [customer_segmentation_sql/model_evaluation.sql]:

SELECT <br><br>*<br><br>FROM <br><br>ML.EVALUATE(MODEL `yourprojectid.yourdataset.my_model`, TABLE `yourprojectid.yourdataset.data`);

****

The above mentioned command performs the evaluation on the data set and outputs the following metrics:

1. Mean squared distance (loss) - squared point-to-centroid distances, averaged over clusters
2. [Davies-Bouldin Index](https://www.google.com/url?q=https://en.wikipedia.org/wiki/Davies%25E2%2580%2593Bouldin_index&sa=D&source=editors&ust=1675884463785023&usg=AOvVaw03PCB-t_MtWz1Xd7-cZRUg) - an average of inter-cluster scatter to intra-cluster separation. Lower the value, better the clusters as it also incorporates intra-cluster distance.

**Choose number of clusters**

Choosing the number of clusters (k) in a clustering algorithm is a well discussed [topic](https://www.google.com/url?q=https://stats.stackexchange.com/questions/23472/how-to-decide-on-the-correct-number-of-clusters&sa=D&source=editors&ust=1675884463785826&usg=AOvVaw37caWPp9_EuQRbm5PkmG0r), and consensus is that there is no right way of choosing the clusters. This could either be driven by a business decision (e.g., you don’t want to run more than 5 different campaigns) or via iterative modeling and testing for accuracy. One common way of choosing k is called the elbow method. Clustering over multiple values of K is performed, and the loss is plotted against k. The "elbow point," where the rate of decrease sharply shifts, can be used to determine a good starting point for k.

Following are the steps to perform the elbow plot analysis in BigQuery:

1. Train models for different number of classes(k) [customer_segmentation_sql/model_train.sql]:

CREATE MODEL `yourprojectid.yourdataset.my_model` OPTIONS(model_type='kmeans',<br><br>num_clusters=3,<br><br>distance_type='euclidean')<br><br>AS SELECT <br><br>*<br><br>FROM <br><br>data;

2. Store training loss for various values of k in views [customer_segmentation_sql/model_evaluation.sql]:

SELECT <br><br>'<k>' AS Size,<br><br>*<br><br>FROM <br><br>ML.EVALUATE(MODEL `yourprojectid.yourdataset.my_model`);

3. Perform the Union of the views into a single view [customer_segmentation_sql/models_comparison.sql]:

SELECT <br><br>*<br><br>FROM <br><br>`yourprojectid.yourdataset.model_1_Evaluation` <br><br>UNION ALL<br><br>SELECT <br><br>*<br><br>FROM <br><br>`yourprojectid.yourdataset.model_2_Evaluation` <br><br>....<br><br>UNION ALL<br><br>SELECT <br><br>*<br><br>FROM <br><br>`yourprojectid.yourdataset.model_<k>_Evaluation`

4. Plot the loss (mean squared distance) vs number of clusters graph in Data Studio to find the best suitable value of k. The "elbow" in the loss chart suggests the number of clusters can be 9.

![](https://lh6.googleusercontent.com/gaI1JDY1GwtdnT4t4KsRndr0q8Fnf_qy9zgRUZgaEMabtv6pfMqVs1uoiel5zeFKVzSFCKGeJVtRLD5Q-fd0S-RUjMfjXCxXjcJri7iIWeoikzbEVn_Qt6vwOSEokRyrJ4Z2VX6QbuDLHac-u38Xdg)

Sequence of SQL execution:

1. customer_segmentation_sql/data_aggregation.sql
2. customer_segmentation_sql/feature_selection.sql
3. customer_segmentation_sql/model_train.sql
4. customer_segmentation_sql/model_evaluation.sql
5. customer_segmentation_sql/model_prediction.sql

### Results

The clusters created from the model are visualized as Data Studio dashboards here:

[https://datastudio.google.com/u/1/reporting/1kypbH_rR07fdE7ZGIatYjPy7VKwkd1wV/page/vI0i](https://www.google.com/url?q=https://datastudio.google.com/u/1/reporting/1kypbH_rR07fdE7ZGIatYjPy7VKwkd1wV/page/vI0i&sa=D&source=editors&ust=1675884463795358&usg=AOvVaw0gyO5tf-BoyEEy4OSEJB8_)

The SQL query to generate data for the dashboard is as follows:

[customer_segmentation_sql/model_prediction.sql]:

SELECT <br><br>Data.*,<br><br>Accounts.Total_Opportunity_Amount,<br><br>Accounts.Country_Code,<br><br>Accounts.Industry,<br><br>Clusters.CENTROID_ID<br><br>FROM <br><br>`yourprojectid.yourdataset.Accounts` as Accounts, `yourprojectid.yourdataset.data` as Data,<br><br>ML.PREDICT(MODEL `yourprojectid.yourdataset.my_model`,<br><br>TABLE `yourprojectid.yourdataset.data`) as Clusters<br><br>WHERE <br><br>Accounts. Account_Number = Data.Account_Number<br><br>AND <br><br>Clusters.User_ID = Data.User_ID<br><br>ORDER BY <br><br>Data.User_ID;

Here are a couple of dashboard screenshots. The first one shows distribution of users across the various clusters. Filters can be set to narrow down on a subset of data.

![](https://lh6.googleusercontent.com/ZJDeItyTiSO9C9e6Q8ARY1QPSJpHjlEYJ32WgnFdqbSzsMSfH-YY17D5W4VUVzFtrmwI0sMGpRE5fPm54zkN6qtWJVod2-XX6plrieWiRKafniIqUrVWW1YOGtqtlMufsc3-TBjFBFKxqJEP8miO0w)

This screenshot shows how various features behave by cluster.

![](https://lh3.googleusercontent.com/sa3UeIyhf_UgsJVNYMKW4HG0opdF_6KugYZ_2q37XNBnnaVZ2i-5KZ0U1K7-PNMU1dNwCeFQT7oDX3RdsXAmAaby6R9CO6O9o4AtPLbvIFHj0ClECtwwApqSqxGObMLLGHhi70luTAQyvr3fVTi4Rg)

## **Customer Lifetime Value**

Customer Lifetime Value (LTV or CLV) is an important metric used by businesses to measure the total revenue that they can reasonably expect from a customer. There are many ways of calculating LTV as described [here](https://www.google.com/url?q=https://en.wikipedia.org/wiki/Customer_lifetime_value&sa=D&source=editors&ust=1675884463800371&usg=AOvVaw0yj6Igb5X-ESPf17gdByib). The LTV value is usually stored in the CRM system. In this modeling use case, we will predict LTV for a brand new user. Predicting LTV for a new user helps a company determine which users are of most “value”, understand those users’ common characteristics, and focus more on them.

Logistic regression is a classification algorithm used to categorize observations to a discrete set of classes. In this given problem we classify customers based on CRM and GA360 data. The customers have been segregated into 3 classes of Lifetime Values (Small, Medium and Large) to help prioritize the different customer segments.

This diagram shows a high level view of the model iterative process.

![](https://docs.google.com/drawings/d/sCg_OxBoKWcsCrJ9kGws_dg/image?parent=e/2PACX-1vSmenfaFjKMq89s2hyESD1v8eRdkZiQspNTAkKQFoSnmEhG1KkpIRIpOEHB1anaA5rTBY5sq-izLghb&rev=56&drawingRevisionAccessToken=sy4PFdDBRAoGwQ&h=247&w=624&ac=1)

In this example, we will do 2 modeling iterations. Here are the features used for the first iteration.

**Field**  | **Description** | **Feature Engineering**

---------- | ---------- | ----------
Time On Screen | Total time spent by user on screen | Aggregated from GA360 data per user.
Unique Screen Views | Total number of screens viewed by the user | Aggregated from GA360 data per user
Screen Resolution | Screen resolution most used by the User | **Mode** calculated from GA360 data per user. Since users used various devices over time, screen resolutions were different for the same user. We computed the mode of the screen resolutions used by a user for the feature since neither the mean of screen resolutions would yield a valid screen resolution and nor would the median.
Loyalty Program | Loyalty program for the user | The values range from 1 to 5, where 5 is considered highest loyalty. We are using loyalty program as an ordinal variable (order matters) and hence treating it as a numeric column. If there were no specific ordering, we would have cast it to a string to treat as a categorical variable.
Lifetime Value | Lifetime value of the user in the account | Binning into small, medium and large. This is used as the label for prediction.
Country Code | Country Code of the User |
Age        | Age of the user | Binning into unknown, young, adult, elderly. This was done for two reasons. Firstly, we observed that many users had not given their age.<br><br>Secondly, it is common practice for people to not furnish correct age so bucketing would reduce the mean error.

The first iteration returned an overall accuracy of 55.8% (see results section below for more details). To improve accuracy below two features were added/changed. The accuracy of the model improved to 70.8%. The decision to make these changes were based both on data exploration as well as a bit of trial and error.

**Field**  | **Description** | **Feature Engineering**

---------- | ---------- | ----------
Age        | Age of the user | Used age as a continuous variable and BQML automatically uses mean to impute values when NULL; this is done to avoid loss of information from binning that may lead to biased results.
Loyalty program normalized by age | It was observed that older people’s loyalty program was heavily skewed. This feature was introduced to reduce the impact of age on loyalty. | Normalize loyalty program values by dividing it by age. We are using loyalty program as an ordinal variable (order matters) and hence treating it as a numeric column. The values range from 1 to 5, where 5 is considered highest loyalty.

### Modeling Steps

The first step is to aggregate to GA360 data [lifetime_value_classification_sql/data_aggregation.sql].

SELECTUser_ID,<br>SUM(timeOnScreen) AS timeOnScreen,<br>SUM(UniqueScreenViews) AS UniqueScreenViews<br>FROM`yourprojectid.yourdataset.GA360`GROUP BYUser_ID

Next we need to calculate the classification boundaries to be used to create the classes [lifetime_value_classification_sql/classification_boundaries_calculation.sql].

SELECT(MIN(LifeTime_Value)+AVG(LifeTime_Value))/8 Boundary1,<br>(MAX(LifeTime_Value)+AVG(LifeTime_Value))/4 Boundary2<br>FROM`yourprojectid.yourdataset.Users`

We need to also find the mode of Screen resolution used by each user which can be found using the combination of the queries [lifetime_value_classification_sql/screen_resolution_count.sql and lifetime_value_classification_sql/screen_resolution_mode.sql].

SELECTUser_ID,<br>screenResolution,<br>COUNT(screenResolution) AS CountFROM`yourprojectid.yourdataset.GA360`GROUP BYUser_ID,<br>screenResolution<br>ORDER BYUser_ID

SELECTA.User_ID,<br>MIN(A.screenResolution) AS screenResolution,<br>MAX(A.Count) AS CountFROM`yourprojectid.yourdataset.ScreenResolutionCount` A,<br>(<br>SELECTUser_ID,<br>MAX(Count) AS Max_Count<br>FROM`yourprojectid.yourdataset.ScreenResolutionCount`GROUP BYUser_ID) B<br>WHEREA.User_ID = B.User_ID<br>AND A.Count = B.Max_Count<br>GROUP BYUser_ID<br>ORDER BYUser_ID

We then bucketize the age into 4 buckets [lifetime_value_classification_sql/Iteration1/ages_bucketization.sql].

SELECT* EXCEPT(Age),<br>CASEWHEN Age IS NULL THEN "Unknown"WHEN Age < 25 THEN "Young"WHEN Age >= 25 AND Age < 50 THEN "Adult"ELSE "Elderly"END Age_Bucket<br>FROM`yourprojectid.yourdataset.Users`

The following SQL query helps to label the users [lifetime_value_classification_sql/Iteration1/users_labelling.sql].

SELECT* EXCEPT(LifeTime_Value),<br>CASEWHEN LifeTime_Value < Boundary1 THEN "Small"WHEN LifeTime_Value >= Boundary1 AND LifeTime_value < Boundary2 THEN "Medium"ELSE "Large"END ClassFROM`yourprojectid.yourdataset.Users_Age_Bucketed`,<br>`yourprojectid.yourdataset.Classification_Boundaries`

The SQL query to select the data from various tables and create view for model training[lifetime_value_classification_sql/Iteration1/feature_selection.sql].

SELECT`yourprojectid.yourdataset.Users_Bucketed_Classified`.User_ID,<br>`yourprojectid.yourdataset.Aggregated_GA360`.timeOnScreen,<br>`yourprojectid.yourdataset.Aggregated_GA360`.UniqueScreenViews,<br>`yourprojectid.yourdataset.Users_Bucketed_Classified`.Loyalty_Program,<br>`yourprojectid.yourdataset.Users_Bucketed_Classified`.Age_Bucket,<br>`yourprojectid.yourdataset.Users_Bucketed_Classified`.Country_Code,<br>`yourprojectid.yourdataset.ScreenResolutionMode`.screenResolution,<br>`yourprojectid.yourdataset.Users_Bucketed_Classified`.Class<br>FROM`yourprojectid.yourdataset.Aggregated_GA360`,<br>`yourprojectid.yourdataset.Users_Bucketed_Classified`,<br>`yourprojectid.yourdataset.Accounts`,<br>`yourprojectid.yourdataset.ScreenResolutionMode`WHERE`yourprojectid.yourdataset.Aggregated_GA360`.User_ID = `yourprojectid.yourdataset.Users_Bucketed_Classified`.User_ID<br>AND `yourprojectid.yourdataset.Accounts`.Account_Number = `yourprojectid.yourdataset.Users_Bucketed_Classified`.Account_ID<br>AND `yourprojectid.yourdataset.Aggregated_GA360`.User_ID = `yourprojectid.yourdataset.ScreenResolutionMode`.User_ID

Here is the SQL command to train the Logistic Regression model for the first iteration.

[lifetime_value_classification_sql/Iteration1/model_creation.sql]

CREATE MODEL `yourprojectid.yourdataset.model_iteration_1` OPTIONS(model_type='logistic_reg',<br><br>auto_class_weights=true,<br><br>input_label_cols=['Class'])<br><br>AS SELECT <br><br>screenResolution,<br><br>timeOnScreen,<br><br>UniqueScreenViews,<br><br>Loyalty_Program,<br><br>Age_Bucket,<br><br>Country_Code,<br><br>Class<br>FROM <br><br>`yourprojectid.yourdataset.data`;

The option auto_class_weights is set to true by default and is used to reduce the bias of the classifier towards the most popular class. These initial default weights are calculated using the formula: TOTAL_INPUT_ROWS / (INPUT_ROWS_FOR_CLASS_N * NUMBER_OF_UNIQUE_CLASSES).

BQML automatically imputes NULL values in a numeric column with mean values. However in this case we needed the imputation to be done explicitly to calculate the “Normalized Loyalty Program” values by dividing Loyalty Program with Age. Here’s how we calculated the average ages to be replaced in place of NULL values: [lifetime_value_classification_sql/Iteration2/average_age_calculation.sql].

SELECTROUND(AVG(age)) AS average_age<br>FROM`yourprojectid.yourdataset.Users`

Then we clean the ages in the dataset [lifetime_value_classification_sql/Iteration2/age_cleaned.sql].

SELECT* EXCEPT(Age),<br>CASEWHEN Age IS NULL THEN average_age<br>ELSE Age<br>END Age<br>FROM`yourprojectid.yourdataset.Users`,<br>`yourprojectid.yourdataset.Average_Age`

The SQL query to select the data from various tables and create view for model training[lifetime_value_classification_sql/Iteration2/feature_selection.sql].

SELECT`yourprojectid.yourdataset.Users_Calculated`.User_ID,<br>`yourprojectid.yourdataset.Aggregated_GA360`.timeOnScreen,<br>`yourprojectid.yourdataset.Aggregated_GA360`.UniqueScreenViews,<br>`yourprojectid.yourdataset.Users_Calculated`.Loyalty_Program,<br>`yourprojectid.yourdataset.Users_Calculated`.Age,<br>`yourprojectid.yourdataset.Users_Calculated`.Country_Code,<br>`yourprojectid.yourdataset.ScreenResolutionMode`.screenResolution,<br>`yourprojectid.yourdataset.Users_Calculated`.Normalized_Loyalty_Program,<br>`yourprojectid.yourdataset.Users_Calculated`.Class<br>FROM`yourprojectid.yourdataset.Aggregated_GA360`,<br>`yourprojectid.yourdataset.Users_Calculated`,<br>`yourprojectid.yourdataset.Accounts`,<br>`yourprojectid.yourdataset.ScreenResolutionMode`WHERE`yourprojectid.yourdataset.Aggregated_GA360`.User_ID = `yourprojectid.yourdataset.Users_Calculated`.User_ID<br>AND `yourprojectid.yourdataset.Accounts`.Account_Number = `yourprojectid.yourdataset.Users_Calculated`.Account_ID<br>AND `yourprojectid.yourdataset.Aggregated_GA360`.User_ID = `yourprojectid.yourdataset.ScreenResolutionMode`.User_ID

Here is the SQL command to train the Logistic Regression model for the second iteration.

[lifetime_value_classification_sql/Iteration2/model_creation.sql]

CREATE MODEL `yourprojectid.yourdataset.model_iteration_2` <br>OPTIONS(<br><br>model_type='logistic_reg',<br><br>auto_class_weights=true,<br><br>input_label_cols=['Class'])<br>AS SELECT <br><br>screenResolution,<br><br>timeOnScreen,<br><br>UniqueScreenViews,<br><br>Loyalty_Program,<br><br>Age,<br><br>Country_Code,<br><br>Normalized_Loyalty_Program,<br><br>Class<br><br>FROM <br><br>`yourprojectid.yourdataset.Dataset_Calculated`;

The training of the Logistic Regression multi-class model happens using a multinomial classifier. The loss calculation happens using a cross entropy loss function which is a log loss function. This type of function produces higher loss when the predicted label deviates from the actual label. The loss calculation tries to minimize this value to output a better performing model.

****

**Evaluate the model**

Accuracy of the model is determined using an evaluation run on the data. The command to perform this evaluation is :

[lifetime_value_classification_sql/Iteration1/model_evaluation.sql]

SELECT *<br>FROM ML.EVALUATE(MODEL yourdataset.model_iteration_number)

The above mentioned command performs the evaluation on the data set and outputs the following metrics:

1. Precision: It refers to the percentage of results which have been classified relevantly
2. Recall: It refers to the percentage of total relevant results which have been classified correctly.
3. Accuracy: It refers to the percentage of correctly classified labels.
4. F1_score: It is defined as the harmonic average of precision and recall. F1 score is said to be at its best when it is closer to 1 and worst when it is closer to 0.
5. Log_loss: It is the metric which the model tries to minimize to get better performance
6. roc_auc: This metric gives us an indication of the performance of the model. Values closer to 1 indicate a better performance.

The confusion matrices shown below illustrate that the inter-class confusion decreases drastically from Iteration 1 to Iteration 2. Confusion matrix is available on the BigQuery UI (evaluation tab for the model), or can be generated using ml.CONFUSION_MATRIX.

![](https://lh6.googleusercontent.com/bk4u4Q7cSMp1XvIvmUBqnzes9hRrwxE6zrQE8SZ7QuDinvmRcazkMtqsBqTAcJHxxyn4jEXOtYEs60e7TSMaEgMqUvwbi1WyP3i3LUEkUPAi9nXVfr55uMoj2Oz6Vv-NgiEKw5kmCTRC9-Z4h0vLeA) | ![](https://lh3.googleusercontent.com/ik8_W9dKpUZi4PASslL0ujNL9Nd6Qgfghfuepau3uhoZLgrUb6A2BsnrEjDPlQSWG_eosFW3Vtvm7saKCFwZgBFMfGfGHE8qyYXCvndBQ4v9EGhOLlMScOR4yEtXopLKx--UnHrNs9-YP0hdL-N3AA)

---------- | ----------
Confusion Matrix for Iteration 1 | Confusion Matrix for Iteration 2

The confusion matrix provides the class predictions in a table layout and allows visualization of the performance of the classification algorithm . Each row of the matrix represents the instances in a predicted class while each column represents the instances in an actual class. It provides quick visibility into overall accuracy as well as false positives and false negatives.

Sequence of SQL execution:

1. lifetime_value_classification_sql/data_aggregation.sql
2. lifetime_value_classification_sql/classification_boundaries_calculation.sql
3. lifetime_value_classification_sql/screen_resolution_count.sql
4. lifetime_value_classification_sql/screen_resolution_mode.sql
5. lifetime_value_classification_sql/Iteration1/ages_bucketization.sql
6. lifetime_value_classification_sql/Iteration1/users_labelling.sql
7. lifetime_value_classification_sql/Iteration1/feature_selection.sql
8. lifetime_value_classification_sql/Iteration1/model_creation.sql
9. lifetime_value_classification_sql/Iteration1/model_evaluation.sql
10. lifetime_value_classification_sql/Iteration1/model_prediction.sql
11. lifetime_value_classification_sql/Iteration1/model_confusion_matrix_creation.sql
12. lifetime_value_classification_sql/Iteration2/average_age_calculation.sql
13. lifetime_value_classification_sql/Iteration2/age_cleanup.sql
14. lifetime_value_classification_sql/Iteration2/users_labelling.sql
15. lifetime_value_classification_sql/Iteration2/features_selection.sql
16. lifetime_value_classification_sql/Iteration2/model_creation.sql
17. lifetime_value_classification_sql/Iteration2/model_evaluation.sql
18. lifetime_value_classification_sql/Iteration2/model_prediction.sql
19. lifetime_value_classification_sql/Iteration2/model_confusion_matrix_creation.sql

### Results

The first iteration yielded an accuracy of 55.8% and the second, an accuracy of 70.8%

The LTV classes created from the model are visualized via Data Studio dashboards here:

[https://datastudio.google.com/u/0/reporting/1qrRuCUVt_zy44X5wZN1yOZ2Mfll06ubA/page/GV3k](https://www.google.com/url?q=https://datastudio.google.com/u/0/reporting/1qrRuCUVt_zy44X5wZN1yOZ2Mfll06ubA/page/GV3k&sa=D&source=editors&ust=1675884463846673&usg=AOvVaw3vEvV2-lTxXI6Ge2-6U5lk)

The SQL query to generate data for the dashboard is as follows:

Iteration 1:

[lifetime_value_classification_sql/Iteration1/model_prediction.sql]

SELECTtimeOnScreen,<br>UniqueScreenViews,<br>Loyalty_Program,<br>Age_bucket,<br>Country_code,<br>screenResolution,<br>Class,<br>predicted_Class<br>FROMML.PREDICT(MODEL `yourprojectid.yourdataset.model_iteration_1`,<br>(<br>SELECT*<br>FROM`yourprojectid.yourdataset.Dataset_Iteration_1`))

Iteration 2:

[lifetime_value_classification_sql/Iteration2/model_creation.sql]

SELECTtimeOnScreen,<br>UniqueScreenViews,<br>Loyalty_Program,<br>Age,<br>Country_code,<br>screenResolution,<br>Normlized_Loyalty_Program,<br>Class,<br>predicted_Class<br>FROMML.PREDICT(MODEL `yourprojectid.yourdataset.model_iteration_2`,<br>(<br>SELECT*<br>FROM`yourprojectid.yourdataset.Dataset_Iteration_2`))

Here are a couple of dashboard screenshots. The first picture shows the distribution of predicted labels across the various classes. Filters can be set to narrow down on a subset of data.

![](https://lh3.googleusercontent.com/FeG5iqsOV9bRN4NTTT4G5Auh5uJHLTnk7QdxhXi1qXb_fXNDAxpAoFphOSwkuukldR3m6VJm0zh34KPbezC-kUvQ1SYEDJzKB49OMDgfUjc1ioGT0IqGH7LeM_IPyqGduXR3rw0AJOujsd-RX0Uzsg)

The below chart shows the distribution of various features per target class.

 ![](https://lh5.googleusercontent.com/WzIExijbiErlHf1SFf_7kmuNl7CiBS9h44WsSR05H4ehLLyCSBZJblKeOURcwy9r9MO90nic_ca-CeXjI2BJxCK3sTqPQuqgnh3hfpwjhB__OgqaEpXpiEDGKWsXb_JW6xyEkV9aaq5bPYVC3tt9Nw)

****

## Conversion/Purchase Prediction

In this example, we predict if a user will purchase the membership program that the company offers. A similar model can be used for any purchase prediction with equivalent underlying data. Membership has a cost to the user, but provides additional benefits e.g. free shipping. It is in the company's interest if many users sign up for this membership as it helps streamline their operations and also helps with recurring revenue.

A binary logistic regression classification model is used to predict whether a conversion occurs or not. In this given problem we label customers based on CRM, GA360 data and Account activation data. Tracking the customer’s usage, we can observe whether a user is going to sign up for membership within first three months (i.e., convert).

Here are the features used for the conversion prediction.

**Field**  | **Description** | **Feature Engineering**

---------- | ---------- | ----------
Total Time On Screen Month 1  | Total time spent by user on screen in the first month of usage | Aggregated from GA360 data’s time on Screen feature per user for the first month of usage. The features Total Time On Screen for the 3 months before a customer sign’s up was calculated incrementally to check if the gradual increase in usage affects the model creation.
Total Time On Screen Month 2  | Total time spent by user on screen in the second month of usage | Aggregated from GA360 data’s time on Screen feature per user for the two months of usage since first use.
Total Time On Screen Month 3 | Total time spent by user on screen in the third month of usage | Aggregated from GA360 data’s time on Screen feature per user for the three months of usage since first use.
Unique Screen Views | Total number of screens viewed by the user | Aggregated from GA360 data per user
Lifetime Value | Lifetime value of the user in the account | This feature was selected to give the model insights to priority customers who have a higher probability of converting.
Age        | Age of the user |

### Modeling Steps

The first step is to aggregate the GA360 data [conversion_prediction_binary_classification_sql/data_aggregation.sql].

SELECTUser_ID,<br>SUM(timeOnScreen) AS timeOnScreen,<br>SUM(UniqueScreenViews) AS UniqueScreenViews<br>FROM`yourprojectid.yourdataset.GA360`GROUP BYUser_ID

We find the date of the first activity of all users from GA360 data [conversion_prediction_binary_classification_sql/users_first_activity_selection.sql].

SELECTUser_ID,<br>MIN(Activity_Date) Activity_Date<br>FROM`yourprojectid.yourdataset.GA360`GROUP BYUser_ID

We use the first date and the GA360 data to find total time on screen for all users for the first, second and third months [conversion_prediction_binary_classification_sql/total_timeOnScreen_month1_calculation.sql and conversion_prediction_binary_classification_sql/total_timeOnScreen_month2_calculation.sql and conversion_prediction_binary_classification_sql/total_timeOnScreen_month3_calculation.sql].

SELECTGA360.User_ID,<br>SUM(timeOnScreen) Total_timeOnScreen<br>FROM`yourprojectid.yourdataset.GA360` GA360,<br>`yourprojectid.yourdataset.First_Activity` First_Activity<br>WHEREGA360.User_ID = First_Activity.User_ID<br>AND DATE_DIFF(GA360.Activity_Date, First_Activity.Activity_Date, month) <= 1GROUP BYGA360.User_ID

SELECTGA360.User_ID,<br>SUM(timeOnScreen) Total_timeOnScreen<br>FROM`yourprojectid.yourdataset.GA360` GA360,<br>`yourprojectid.yourdataset.First_Activity` First_Activity<br>WHEREGA360.User_ID = First_Activity.User_ID<br>AND DATE_DIFF(GA360.Activity_Date, First_Activity.Activity_Date, month) = 2GROUP BYGA360.User_ID

SELECTGA360.User_ID,<br>SUM(timeOnScreen) Total_timeOnScreen<br>FROM`yourprojectid.yourdataset.GA360` GA360,<br>`yourprojectid.yourdataset.First_Activity` First_Activity<br>WHEREGA360.User_ID = First_Activity.User_ID<br>AND DATE_DIFF(GA360.Activity_Date, First_Activity.Activity_Date, month) = 3GROUP BYGA360.User_ID

We segment the users into labels based on their signup dates where true being the case when signup date is within three months of the first activity date [conversion_prediction_binary_classification_sql/labels_generation.sql].

SELECTSignup.User_ID,<br>CASEWHEN Signup_Date <= DATE_ADD(Activity_Date, INTERVAL 3 MONTH) THEN 1ELSE 0END Label<br>FROM`yourprojectid.yourdataset.Users_Signup_Dates` Signup,<br>`yourprojectid.yourdataset.First_Activity` First_Activity<br>WHERESignup.User_ID = First_Activity.User_ID

Since most of the examples are false we randomly select 15000 false examples and merge with the true ones [conversion_prediction_binary_classification_sql/true_example_selection.sql and conversion_prediction_binary_classification_sql/false_example_selection.sql and conversion_prediction_binary_classification_sql/false_example_random_selection.sql and conversion_prediction_binary_classification_sql/users_selection.sql].

SELECT*<br>FROM`yourprojectid.yourdataset.Labels`WHERELabel = 1

SELECT*<br>FROM`yourprojectid.yourdataset.Labels`WHERELabel =0

SELECT*<br>FROM`yourprojectid.yourdataset.Label_False`WHERELabel = 0ORDER BY RAND()<br>LIMIT 15000

SELECT*<br>FROM`yourprojectid.yourdataset.Label_True`UNION ALL<br>SELECT*<br>FROM`yourprojectid.yourdataset.Label_False_Random`

Since all users may not have usages in their second and third months of their first activity date [conversion_prediction_binary_classification_sql/total_timeOnScreen_month1_extention.sql and conversion_prediction_binary_classification_sql/total_timeOnScreen_month2_extention.sql and conversion_prediction_binary_classification_sql/total_timeOnScreen_month3_extention.sql]

SELECT*<br>FROM (<br>SELECTUsers_Selected.User_ID,<br>Total_timeOnScreen_month1.Total_timeOnScreen<br>FROM `yourprojectid.yourdataset.Total_timeOnScreen_month1` Total_timeOnScreen_month1<br>FULL OUTER JOIN`yourprojectid.yourdataset.Users_Selected` Users_Selected<br>ONTotal_timeOnScreen_month1.User_ID = Users_Selected.User_ID)<br>WHEREUser_ID IS NOT NULL

SELECT*<br>FROM (<br>SELECTUsers_Selected.User_ID,<br>Total_timeOnScreen_month1.Total_timeOnScreen<br>FROM `yourprojectid.yourdataset.Total_timeOnScreen_month2` Total_timeOnScreen_month2<br>FULL OUTER JOIN`yourprojectid.yourdataset.Users_Selected` Users_Selected<br>ONTotal_timeOnScreen_month2.User_ID = Users_Selected.User_ID)<br>WHEREUser_ID IS NOT NULL

SELECT*<br>FROM (<br>SELECTUsers_Selected.User_ID,<br>Total_timeOnScreen_month1.Total_timeOnScreen<br>FROM `yourprojectid.yourdataset.Total_timeOnScreen_month3` Total_timeOnScreen_month3<br>FULL OUTER JOIN`yourprojectid.yourdataset.Users_Selected` Users_Selected<br>ONTotal_timeOnScreen_month3.User_ID = Users_Selected.User_ID)<br>WHEREUser_ID IS NOT NULL

The SQL query to select the data from various tables and create view for model training [conversion_prediction_binary_classification_sql/feature_selection.sql].

SELECTm1.User_ID,<br>m1.Total_timeOnScreen Total_timeOnScreen_month1,<br>m2.Total_timeOnScreen Total_timeOnScreen_month2,<br>m3.Total_timeOnScreen Total_timeOnScreen_month3,<br>UniqueScreenViews,<br>Lifetime_Value,<br>Age,<br>Label<br>FROM`yourprojectid.yourdataset.Total_timeOnScreen_month1_Extended` m1, `yourprojectid.yourdataset.Total_timeOnScreen_month2_Extended` m2, `yourprojectid.yourdataset.Total_timeOnScreen_month3_Extended` m3,<br>`yourprojectid.yourdataset.Users_Selected` Users_Selected,<br>`yourprojectid.yourdataset.Aggregated_GA360` GA360,<br>`yourprojectid.yourdataset.Users` UsersWHEREm1.User_ID = m2.User_ID<br>AND m2.User_ID = m3.User_ID<br>AND m3.User_ID = Users_Selected.User_ID<br>AND Users_Selected.USer_ID = GA360.User_ID<br>AND GA360.User_ID = Users.User_ID

Here is the SQL command to train the Logistic Regression model.

[conversion_prediction_binary_classification/model_creation.sql]

CREATE MODEL `yourprojectid.yourdataset.model` OPTIONS(model_type='logistic_reg',<br><br>auto_class_weights=TRUE,<br><br>input_label_cols=['Label'])<br><br>AS SELECT <br><br>Total_timeOnScreen_month_1,<br><br>Total_timeOnScreen_month_2,<br><br>Total_timeOnScreen_month_3,<br><br>UniqueScreenViews,<br><br>Lifetime_Value,<br><br>Age,<br><br>Label<br>FROM <br><br>`yourprojectid.yourdataset.data`;

The model returned an overall accuracy of 75% (see results section below for more details).

**Evaluate the model**

Accuracy of the model is determined using an evaluation query, which evaluates the model on the test data split (from training data used for model creation) by default. The command to perform this evaluation is :

[conversion_prediction_binary_classification/model_evaluation.sql]

SELECT *<br>FROM ML.EVALUATE(MODEL yourdataset.model)

The above mentioned command performs the evaluation on the data set and outputs the following metrics:

1. Precision: It refers to the percentage of results which have been classified relevantly
2. Recall: It refers to the percentage of total relevant results which have been classified correctly.
3. Accuracy: It refers to the percentage of correctly classified labels.
4. F1_score: It is defined as the harmonic average of precision and recall. F1 score is said to be at its best when it is closer to 1 and worst when it is closer to 0.
5. Log_loss: It is the metric which the model tries to minimize to get better performance
6. roc_auc: This metric gives us an indication of the performance of the model. Values closer to 1 indicate a better performance.

Here are a few charts that BQML (evaluation tab) provides on the BigQuery Web UI to visualize the performance of the model. From the chart, we can also determine the best threshold value (threshold at which the classes are separated) which happens to be 0.67 in this case. Different use cases have different precision and recall requirements, and the threshold can be chosen to optimize for the right objective. In this case, we pick the elbow to get a balanced output.

![](https://lh3.googleusercontent.com/aILYQvM4h-LdBEccfRIN89SHhsVMRQDX-J1Y9Kbx3uEC0MyAqUMThIakOvKT13GcAMm0_PylfubfrT_OVyg0U3p13Rpa90cebvGGghjofq-QuU9-BPZN5AYpKsCV_moBwtnVaba--oLTRRNcwkPQ1w) | ![](https://lh5.googleusercontent.com/w0c5Lj54J_im16RGF21t6yxNFloCzz3CLtOd81kTJtleKQqhoS8smANuAiVYyymARmddOmHxKyVMG8LaRqb82y6VOv4hWdJO61USTHpl1dB0JLA9SI40goht-Nhdnhk0Jp_vxvi9OMJhsGZIUqLtJg)

---------- | ----------
![](https://lh4.googleusercontent.com/SGYEB8FN-1PS7jmVJaur535RCJu2BqSy-2yRPLk9_WJSc7Y-teEcbGeXEwmtM44G6T8BJVPNXTrbPuM4Hc1QEi73Ri6Yf3EqQ44_khKFChRJRWn1llUaeDKCOG3OLhfVnMHp2LqnhjPI1f-vPmL4YA) | ![](https://lh6.googleusercontent.com/rnHBvrmjlgDkLS_x9WfpEr-dTxMQss4eV2BEa6-O9X4v_7YsWxE9LNgr4gFwV_r_FD5WmNnGHxAbcRDgSnhVB-BrcHSfCoMV1BruV6xWre73vJnJktBG6s3RYliC3XuHXbMYOH-z6sGtVNbmkGACQA)

Sequence of SQL execution:

1. conversion_prediction_binary_classification_sql/data_aggregation.sql
2. conversion_prediction_binary_classification_sql/users_first_activity_selection.sql
3. conversion_prediction_binary_classification_sql/total_timeOnScreen_month1_calculation.sql
4. conversion_prediction_binary_classification_sql/total_timeOnScreen_month2_calculation.sql
5. conversion_prediction_binary_classification_sql/total_timeOnScreen_month3_calculation.sql
6. conversion_prediction_binary_classification_sql/label_generation.sql
7. conversion_prediction_binary_classification_sql/true_example_selection.sql
8. conversion_prediction_binary_classification_sql/false_example_selection.sql
9. conversion_prediction_binary_classification_sql/false_example_random_selection.sql
10. conversion_prediction_binary_classification_sql/users_selection.sql
11. conversion_prediction_binary_classification_sql/total_timeOnScreen_month1_extention.sql
12. conversion_prediction_binary_classification_sql/total_timeOnScreen_month2_extention.sql
13. conversion_prediction_binary_classification_sql/total_timeOnScreen_month3_extention.sql
14. conversion_prediction_binary_classification_sql/feature_selection.sql
15. conversion_prediction_binary_classification_sql/model_creation.sql
16. conversion_prediction_binary_classification_sql/model_evaluation.sql
17. conversion_prediction_binary_classification_sql/model_prediction.sql
18. conversion_prediction_binary_classification_sql/model_confusion_matrix_creation.sql

### Results

The model yielded an accuracy of 75%.

The classes created from the model can be visualized via Data Studio dashboards here:

[https://datastudio.google.com/u/0/reporting/1fodoHSgU3YFTwFR3vF6VT3EFTh5xvEly/page/1TFm](https://www.google.com/url?q=https://datastudio.google.com/u/0/reporting/1fodoHSgU3YFTwFR3vF6VT3EFTh5xvEly/page/1TFm&sa=D&source=editors&ust=1675884463877244&usg=AOvVaw3_UbRGWVm9pSFrCizFh_S0)

The SQL below generates the data for the dashboard.

[conversion_prediction_binary_classification_sql/model_prediction.sql]

SELECT User_ID, <br> Total_timeOnScreen_month1,<br> Total_timeOnScreen_month2,<br> Total_timeOnScreen_month3,<br> UniqueScreenViews,<br> Lifetime_Value,<br> Age,<br> Label,<br> predicted_Label<br>FROM ML.PREDICT(MODEL `yourprojectid.yourdataset.model`,<br> (<br> SELECT *<br> FROM `yourprojectid.yourdataset.Dataset`))

**Making Predictions In Real Time**

The Logistic Regression model provides weights and intercept values that allows the model to be embedded in a client program (e.g. website) so that predictions can be made in real time. Here’s a sample code in Python; the same logic can be used in other languages as well.

from google.cloud import bigquery<br>from math import exp<br><br><br>client = bigquery.Client()<br><br>query_job = client.query("""SELECT * FROM ML.WEIGHTS(MODEL `yourprojectid.yourdataset.model`)""")<br>results = query_job.result()<br>weights = {}<br>for row in results:<br> weights[row[0]] = float(row[1])<br>print(weights)<br><br>label = weights['**INTERCEPT**']<br>s = ""for key in weights.keys():<br> if key == '**INTERCEPT**':<br> s += " + " + str(weights[key])<br> continue val = input("Enter value for " + key + ' : ')<br> label += (val * weights[key])<br> s += " + ( " + str(weights[key]) + " * " + str(val) + " ) "prob = exp(label) / ( 1 + exp(label))<br><br>if prob >= 0.5:<br> print("1")<br>else:<br> print("0")

Here are a couple of dashboard screenshots.The first picture shows distribution of predicted labels across the various classes. Filters can be set to narrow down on a subset of data.

![](https://lh6.googleusercontent.com/pIFChcu7O5pCkAUuqj018unZ9FRI3uE4DwHnSUQLQ3GuBcvXVq4AYV7P9fXrmH94Qq9_M0L-qN86W3juYIZhmjk08KjHKtCMy-BT0YulAZKZGUCeJCyuILi3cBtoXmDYrB4Im46uhV9xQcji5KHkVg)

The below chart shows the distribution of various features per target class.

![](https://lh3.googleusercontent.com/3hVlSqAEi9QDne-PqNq8tVUGmObpCJQ6Evp9TGvW8GAgm3OFxkGhe9LWZF1O1RtZGB93LyypMSw2ZrGXKD_Q0si1m_iY4eZjxqUPK2jbg6qMvVbUiXDlXH2fpC9H1VzPwLHjL2qeFxKwEa5Ue8rrcQ)
