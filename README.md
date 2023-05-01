# Telecom Customer Churn Data Analysis

- Analyzed large Telecommunications datasets to identify trends and patterns related to customer behavior.
- Utilized tidyverse and ggplot library to perform tidying, manipulation, and data visualization in R.
- Developed and implemented machine learning algorithms like Random Forest, Decision Trees and Logistic Regression to predict the likelihood of customers canceling their service, and using data insights to develop strategies to minimize financial losses.

## Introduction
This is an individual assignment and will be a chance for you to perform an applied data science project on a real data set. 

We will be working with the `telecom_df` data frame in this project. This data set contains information on over 1,000 customer of a U.S. telecommunications company. The description of this data and the variables contained in it are provided below.

The objective of this project is to explore the factors that lead to customers canceling their mobile and Internet service and develop machine learning algorithms that will predict the likelihood of a customer canceling their service in the future.

## Telecommunications Data

The `telecom_df` data frame contains information on the customers of a large U.S. telecommunications company which provides Internet and cellular service. 

The company is looking to see if it can determine the factors that lead to customers canceling their service and whether it can predict if a customer will cancel their service in the future. 

The company has experienced record levels of customers leaving their service in the past couple of years and this is leading to large financial losses. 

The goal is to become better at identifying customers at risk of canceling their service to minimize financial losses.

Specifically, the broad questions that the company is trying to answer include:

- What are the factors that are associated with customers canceling their service?
- Is it possible to predict whether a customer will cancel their service? If so, how accurate are the predictions?
- How many costly errors is the model expected to produce (customers classified as not canceling, but eventually do)?
- Are there any actions or policies the company can implement to reduce the risk of service cancellation?

The data set contains a mixture of customer information (senior citizen indicator, presence of dependents, months with the company, etc..), and customer behavior (type of Internet and cellular service, average monthly call minutes, etc...)

The outcome variable in this data is `canceled_service`. This variable records whether a customer eventually canceled their service and indicates a financial loss to the company.

**Note**: The outcome variable has been coded as a factor with 'yes' as the first level. This is the format that `tidymodels` expects for calculating model performance metrics. There is no need to recode this variable in your machine learning process.

# Exploratory Data Analysis (50 Points)

In this section, you must think of **at least 5 relevant questions** that explore the relationship between `canceled_service` and the other variables in the `telecom_df` data set. The goal of your analysis should be discovering which variables drive the differences between customers who do and do not cancel their service.

You must answer each question and provide supporting data summaries with either a summary data frame (using `dplyr`/`tidyr`) or a plot (using `ggplot`) or both.

In total, you must have a minimum of 3 plots (created with `ggplot`) and 3 summary data frames (created with `dplyr`) for the exploratory data analysis section. Among the plots you produce, you must have at least 3 different types (ex. box plot, bar chart, histogram, scatter plot, etc...)

Each question must be answered with **supporting evidence** from your tables and plots.

See the example question below.

### Sample Question
The sample below is from a previous semester where students analyzed a dataset, **employee_df**, with information on employees of a company and whether they decided to leave the company for another job.

The question, `R` code, and answer are examples of the correct style and language that you should use for your work.

### Question

*Is there a relationship between employees leaving the company and their current salary?*

**Answer**: Yes, the data indicates that employees who leave the company tend to have lower salaries when compared to employees who do not. Among the 237 employees that left the company, the average salary was \$76,625. This is over \$20,000 less than the average salary of employees who did not leave the company.

Among the employees *who did not leave the company*, only 10% have a salary that is less than or equal to \$60,000. When looking at employees who did leave the company, this increases to 34%.

## Question 1

**Question**:
Is monthly charges effecting the telecom company sales? if yes, explain in brief.

**Answer**:

We can conclude from the visual representations below that there is a negligible impact of monthly fees on customers quitting the business. So, we cannot declare that monthly fees should be regarded as a significant element affecting the company's profits.

![image](https://user-images.githubusercontent.com/130720035/235512322-e489f2d7-b9e7-4dbd-80c2-193b45067bfa.png)

## Question 2

**Question**:
Is there any relation between contract and the canceled service? If yes, explain in brief.

**Answer**:

Yeah, it is evident from the visualisation below that those who signed a month-to-month contract are more likely to cancel the service than those who signed a two-year contract, who are more likely to keep the term without canceling. As we all know, in order to attract customers, businesses try to maintain high fees for those who signed a month-to-month contract while keeping fees low for those who signed a yearly contract. As a result, customers who signed a month-to-month contract are terminating the contract because of the high fees.

![image](https://user-images.githubusercontent.com/130720035/235512390-c74dadc3-de35-4857-8deb-5f44721a66fe.png)

## Question 3

**Question**:

Is there any relation between network and canceled Service? If yes, explain in breif.

**Answer**:

Yes, from the below visualisation we can clearly understand that, the customers who took fibre optics network are most likely to cancel the service and the customers who took digital network are most likely to continue with the service.

![image](https://user-images.githubusercontent.com/130720035/235512460-6919a105-87f7-4d10-bd0c-0317eac7eef1.png)

## Question 4

**Question**:
Is there any relation between cellular service and canceled Services? Explain with visualisation.

**Answer**:
Certainly, it is evident from the visualisation below that consumers who have purchased numerous lines are more likely to cancel the service than those who have just purchased a single line. The expense of having numerous lines may be more than the cost of having a single line, which is why customers who have many lines are abandoning their subscription. This is visualized in the image below.

![image](https://user-images.githubusercontent.com/130720035/235512572-1dce6b6f-2263-44b7-bcd5-b33284f2a2d5.png)

## Question 5

**Question**:
Explain the relation between months with the company and canceled services?

**Answer**:

The below graph makes it very evident that customers are more likely to discontinue service at the beginning of the month than they are to continue it as the number of months spent with the business grows. The cause of this may be because customers first had challenges with the company, which the business may have taken some time to resolve technically, leading to customers continuing to use the service as the number of months with the business increased.

![image](https://user-images.githubusercontent.com/130720035/235512629-0d507eea-6f0b-4e85-a0cd-f566be8c3da8.png)

# Machine Learning Modeling 
In this section of the project, you will fit **three classification algorithms** to predict the response variable,`canceled_service`. You should use all of the other variables in the `telecom_df` data as predictor variables for each model.

You must follow the machine learning steps below. 

The data splitting and feature engineering steps should only be done once so that your models are using the same data and feature engineering steps for training.

1. Split the `telecom_df` data into a training and test set (remember to set your seed)
2. Specify a feature engineering pipeline with the `recipes` package
    - You can include steps such as skewness transformation, dummy variable encoding or any other steps you find appropriate
3. Specify a `parsnip` model object
    - You may choose from the following classification algorithms:
      - Logistic Regression
      - LDA
      - QDA
      - KNN
      - Decision Tree
      - Random Forest
4. Package your recipe and model into a workflow
5. Fit your workflow to the training data
    - If your model has hyperparameters:
      - Split the training data into 5 folds for 5-fold cross validation using `vfold_cv` (remember to set your seed)
      - Perform hyperparamter tuning with a random grid search using the `grid_random()` function
      - Refer to the following tutorial for an example - [Random Grid Search](https://gmubusinessanalytics.netlify.app/lesson-08-r-tutorial.html#Hyperparameter_Tuning14)
      - Hyperparameter tuning can take a significant amount of computing time. Be careful not to set the `size` argument of `grid_random()` too large. I recommend `size` = 10 or smaller.
      - Select the best model with `select_best()` and finalize your workflow
6. Evaluate model performance on the test set by plotting an ROC curve using `autoplot()` and calculating the area under the ROC curve on your test data

## Introduction

The Telecom company is facing financial loss due to losing of customers in high rate. The company is trying to understand the clients who may leave in the future and factors that are effecting the customers which leads to company's loss. The company uses this information to reduce their losses by knowing the customer needs, so that they can make some changes in their policy which may lead to company profits in future.

The goal of this analysis is to identify the factors that are effecting the company's growth, so that the company may make changes some of their policy's and the goal of modelling is to predict the customers who are at risk to leave the company. This analysis goal is to answer questions like:

- What are the main reasons for customers leaving the service?
- Explain the relation between months with the company and canceled services?
- Is there any relation between contract and the canceled service? If yes, explain in brief.

## Key Findings

There are some of the important points to be noted from the above analysis, they are as follows:

1) Customers who signed a month-to-month contract are more likely to cancel the service due to high fees compared to those who signed a two-year contract.
2) Customers who took fibre optics network are more likely to cancel the service compared to those who took digital network.

3) Customers who have purchased many lines are more likely to cancel the service compared to those who have just purchased a single line, possibly due to the higher cost of having multiple lines.

4) Customers are more likely to discontinue service at the beginning of the month than they are to continue it as the number of months spent with the business grows, possibly due to initial challenges with the company that were eventually resolved.


## Modeling Results

From the above machine learning modellings, the best model was logistic regression model. The roc_auc we obtained was 88%.
ROC_AUC measures the difference between the customers who are willing to cancel the service and the customers who are willing to continue with the company. A value of 1 represents perfect prediction and value of 0.5 represents that the model
used random guessing. From the ROC_AUC we got an value of 88% which means it predicted 88% correctly, which results the model performed well.
...


## Recommendations

1) **Offer more for the customers to take long term contract**: The telecom company should offer discounted rates to the customers for long term customers to make the short term customers sign for long term contract, because from the above analysis we got to know that the customers who signed for 2-years contract are less likely to leave the company.
2) **Enhance the level of service provided to customers of fiber optics**: The telecom company should focus more on improving the quality of service for the customers who took fiber optics, because these customers are more likely to cancel the services with the company.
3) **For customers that have multiple lines, provide more flexible pricing options.**: The company should focus more on the customers having multiple lines, like to provide some discounted rate for every time they add their new line, because the customers with multiple lines are most likely to leave the company.
4) **Enhance customer service and assistance**: The telecom business should concentrate on enhancing customer care and support as customers are more likely to cancel service at the beginning of the month. This will allow them to respond to any difficulties customers may have promptly. This can be done by hiring more customer service representatives so they can resolve problems.

Finally, we can conclude that by implementing the above recommendations, the telecom company may reduce their customers loss and might increase their profits in future.
...
