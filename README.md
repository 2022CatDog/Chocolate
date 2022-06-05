# CatDog: All about Chocolate



## Project Overview
Chocolate popularity over the world never decreases. More and more fancy and novel chocolates are coming to the market. We want to find out what factors affect the rating of certain chocolate and provide chocolate manufacturers with this information to help them determine what type of chocolate to produce in the future; we also want to predict chocolate ratings using these features and help consumers to pick their favorite chocolates.



## Description of the Data
We download our raw data from Kaggle and scrape more recent chocolate rating data from the website ([Flavors of Cacao - Chocolate Database](http://flavorsofcacao.com/chocolate_database.html)) which is also the original source of our training dataset. The raw features include the year when a rating was made, chocolate company name, company location, bean origin, cocoa percentage, whether the chocolate contains certain ingredients, the first to fourth tastes (a lot of missing values) and the ratings provided by the chocolate reviewers.



## Feature Engineering
Our primary analysis shows that most of the features have an impact on the rating. Due to the high cardinality of certain features, we use different ways to encode them. For company location and bean origin, we group countries by their continents. Then we one-hot and target encode these location based features. For the taste profile, we group similar taste descriptive words together, e.g., fatty & oily, sandy & gritty and earthy & dirt. Then we select the 18 most frequent categories and use them to replace the old features (first to fourth tastes). If any taste of a chocolate falls in one of the 18 taste categories including fruity and creamy, we label it as 1 otherwise 0.


![Chocolate_Fruit_Rating](https://user-images.githubusercontent.com/32944487/172035335-d75cf204-5fc0-4a43-8c86-3ae0de7a4962.png)

![Chocolate_Creamy_Rating](https://user-images.githubusercontent.com/32944487/172035344-2e8385fb-e510-4cec-8f46-f66cd580d485.png)


Exploratory data analysis on the newly built features points out that a few features e.g. containing cocoa butter or not has almost no impact on the rating, and some features do have an impact on rating, e.g. chocolate with sugar has higher average rating. These results are also backed up by hypothesis tests. For high cardinality features, we run one way ANOVA with significance level 0.05 to see if at least two of the values make difference in average rating. For binary features, we ran two sample t-test with significance level 0.05 to see if the impact of certain ingredients on rating is significant. The test results align with our data visualization.

![Chocolate_Sugar_Rating](https://user-images.githubusercontent.com/32944487/172035363-8d19cbba-47af-42dc-b9ab-20eae1ab18ca.png)

## Models
We use regression models to predict the ratings in the test set. The performance metric we use is mean absolute error. It can be understood as how much the prediction rating deviates from the actual rating within a plus or minus range. We build five regression models, which are lasso regression, random forest regression, xgboost regression, lightgbm regression and catboost regression. For the linear regression model, we compare the performance of feature selection with a 10-fold cross validation in two ways - one is based on the hypothesis testing result and the other uses lasso to tune the regularization coefficient. For the tree based models (except for catboost), we run grid search with 10-fold cross validation on the training set to optimize the hyperparameters. For catboost, we use the built in pool function to encode location and time features, and tune some of the hyperparameters. We achieve 0.30 mean absolute error with a 10-fold cross validation.

![Chocolate_Location_Rating](https://user-images.githubusercontent.com/32944487/172035307-6d363e46-b563-4d93-a3c7-594ed52ad289.png)


We run our models on test data and confirm that all the predicted ratings are within a reasonable range. We achieve 0.2533 test mean absolute error (using XGBoost), whereas the mean absolute error of the baseline model is 0.2935.



## Model Limitations
We notice that the average rating varies a lot by year. Our models do not handle time data very well. We manually organize and encode the taste profile. This requires a lot of effort and it is hard to accommodate unseen tastes . A potential way of improving taste profile classification is to apply a pre-trained NLP model to the tastes and use a clustering model to group the tastes based on their similarities.



## Conclusion
We find out the important features determining chocolate ratings are: cocoa percentage, fruity taste, creamy tastes, cocoa taste and sandy taste. This information may be useful for chocolate manufacturers when creating new products. We also find that chocolates with companies and beans from Africa and Asia tend to have relatively higher ratings compared with those from the other continents, which may be helpful for consumers to choose what chocolates to purchase. Among the models we experiment, XGBoost has the best performance on the test set. One future direction is to further fine-tune and investigate the XGBoost model to see the robustness of such model with respect to feature selection. 
