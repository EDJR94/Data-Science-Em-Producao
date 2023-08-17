# Rossmann Store Sales Prediction
![rossmann](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/982bd982-b6d6-4174-8f87-93063fd96acf)

## 01. Business Problem

Rossmann operates over 3,000 drugstore chains in 7 European countries. Store sales are influenced by various factors, including promotions, competition, school and state holidays, seasonality, and location. Currently, Rossmann store managers are tasked with predicting their daily sales up to six weeks in advance. With thousands of individual managers making predictions based on their unique circumstances, the accuracy of results can vary significantly.

As a Data Scientist, my task was to help predict these daily sales with a six-week lead time through Data Analysis and Machine Learning models and report the results to the CFO via a Telegram Bot.

## 02. Assumptions

- The dataset contains sales made between 01/01/2013 and 07/31/2015.
- The original variables/attributes (and their meanings) in the dataset are as follows:

| Attributes | Meaning |
| --- | --- |
| store | unique id for each store |
| day_of_week | day of the week (1 to 7) |
| date | date |
| sales | financial volume of sales on the day |
| customers | number of customers on the day |
| open | indicator if the store was open (0 = closed, 1 = open) |
| promo | indicates if the store had a promotion on the day |
| state_holiday | indicates if it was a state/national holiday (a = public holiday, b = Easter, c = Christmas, 0 = none) |
| school_holiday | indicates if the store was affected by the closure of public schools on the day |
| store_type | indicates the store type (4 types: a, b, c, d) |
| assortment | describes the level of product assortment (a = basic, b = extra, c = extended) |
| competition_distance | distance in meters to the nearest competitor store |
| competition_open_since_month | month when the nearest competitor store opened |
| competition_open_since_year | year when the nearest competitor store opened |
| promo2 | ongoing and consecutive promotion for some stores (0 = store did not participate, 1 = store participated) |
| promo2_since_week | indicates the week of the year when the store started participating in promo2 |
| promo2_since_year | indicates the year when the store started participating in promo2 (complementary to promo2_since_week) |
| promo_interval | describes the consecutive intervals when promo2 started, indicating the months when the promotion started again (Ex.: "Feb,May,Aug,Nov" means each interval started in February, May, August, and November in a given year for a given store) |

## 03. Solution Strategy

The strategy used was the CRISP method, divided into 10 parts:

![crisp](https://github.com/EDJR94/pa004_health_insurance/assets/128603807/67b3ae4f-ea88-42e9-9cb4-43eee51cec4a)

1. Business question presented by the CFO.
2. Understanding the Rossmann Business.
3. Data Collection.
4. Data Cleaning.
5. Data Exploration.
6. Data Modeling.
7. Using Machine Learning Models.
8. Evaluation of Machine Learning Algorithm.
9. Model Deployment in Production.
10. Telegram Bot.

## 04. Key Business Insights

The following business hypotheses were raised based on how Rossmann operates:

1. Stores with a larger assortment should sell more.
2. Stores with closer competitors should sell less.
3. Stores with longer-standing competitors should sell more.
4. Stores with longer-running promotions should sell more.
5. Stores with more consecutive promotions should sell more.
6. Stores open during Christmas holidays should sell more.
7. Stores should sell more over the years.
8. Stores should sell more in the second half of the year.
9. Stores should sell more after the 10th day of each month.
10. Stores should sell less on weekends.
11. Stores should sell less during school holidays.

Among the 11 hypotheses, the most important ones considered by me were:

1. Stores with longer-standing competitors should sell more.

![h1 hypothesis](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/100e4719-8fc2-4ed4-8c03-db42674916c6)

From the graph, we can see that the closer the competitor store opens to the current date (2015), the more Rossmann stores sell. This can also be seen from the positive correlation.

2. Stores should sell more in the second semester.

![download (2)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/c6d47e45-684d-48a7-a153-354f68748eb7)

From the graph, we can see that sales drop significantly after month 6, with a strong negative correlation.

3. Stores should sell more after the 10th day of each month.

![download (3)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/e68b99ae-b9f4-42d5-ad6b-f775a148f38c)

From the graph, we observe that store sales fluctuate throughout the days of the month. There is no strong correlation between the day of the month and sales.

4. Sales should be lower during school holidays.

![download (4)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/efeb5c56-7f38-4584-b57c-a70980965fda)

Indeed, sales are lower during school holidays, but there is a detail in months 7 and 8 where sales are equal and higher. This is likely due to summer vacations.

## 05. Machine Learning

The following Machine Learning models were used to analyze sales prediction:

- *Average Model*
- *Linear Regression*
- *Linear Regression Regularized*
- *Random Forest Regressor*
- *XGBoost Regressor*

After analyzing the errors (MAE, MAPE, and RMSE) below, I chose to proceed with the *XGBoost Regressor*. Although the *Random Forest* presented slightly better error values, it has a significantly larger size than the *XGBoost Regressor*.

| Model Name | MAE | MAPE | RMSE |
| --- | --- | --- | --- |
| Random Forest Regressor | 680.854054 | 0.100115 | 1012.687130 |
| XGBoost Regressor | 868.958205 | 0.130309 | 1238.550843 |
| Average Model | 1354.800353 | 0.206400 | 1835.135542 |
| Linear Regression | 1867.089774 | 0.292694 | 2671.049215 |
| Linear Regression - Lasso | 1891.704881 | 0.289106 | 2744.451741 |

After applying Cross-Validation, we can observe from the table below that the errors are close to the errors applied to the training dataset above, confirming that the model has good generalization capability.

| Model Name | MAE CV | MAPE CV | RMSE CV |
| --- | --- | --- | --- |
| Random Forest Regressor | 836.83 +/- 217.3 | 0.12 +/- 0.02 | 1255.04 +/- 316.89 |
| XGBoost Regressor | 1060.51 +/- 178.41 | 0.15 +/- 0.02 | 1512.59 +/- 241.37 |
| Linear Regressoion | 2081.73 +/- 295.63 | 0.3 +/- 0.02 | 2952.52 +/- 468.37 |
| Linear Regression - Lasso | 2116.38 +/- 341.5 | 0.29 +/- 0.01 | 3057.75 +/- 504.26 |

Finally, the final model, after adjusting the hyperparameters, was as follows:

| Model Name | MAE | MAPE | RMSE |
| --- | --- | --- | --- |
| XGBoost Regressor | 695.985642 | 0.102112 | 1007.379751 |

## 06. Business Model Translation

From the predictions made by the model, we can translate the error values found into estimated business values. In the table below are the model's predictions considering the worst and best financial scenarios.

| Scenarios | Values |
| --- | --- |
| prediction | R$ 284,718,336.00 |
| worst_scenario | R$ 283,938,442.77 |
| best_scenario | R$ 285,498,228.15 |

## 07. Telegram Bot

After deploying the model to production, I created a Telegram bot that retrieves real-time sales predictions for the desired store:

![rossmann bot](https://user-images.githubusercontent.com/128603807/236702453-dae91759-bd2e-44be-8079-3de5cf56be14.jpg)

## 08. Final Product and Conclusion

The final product was the Telegram bot that can be accessed by the CFO from any device connected to the internet and using Telegram, facilitating the budget definition for the renovation of each store. Additionally, the hypotheses generated valuable insights that can be used to increase sales.

## 09. Next Steps

Continue with additional CRISP cycles, focusing on:

- Testing other Machine Learning models.
- Filling missing data in other ways.
- Testing other approaches to deal with outliers.
- Exploring alternative strategies to define model hyperparameters.
- Adding more query options to the Telegram Bot.

## References

Dataset: [https://www.kaggle.com/competitions/rossmann-store-sales](https://www.kaggle.com/competitions/rossmann-store-sales)

