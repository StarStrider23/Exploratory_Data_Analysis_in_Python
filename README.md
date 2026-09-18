# Exploratory Data Analysis in Python

Project by Alexsey Chernichenko

## Project Background and Overview

This project explores Systembolaget's sales data from 2009 to 2024 using Python. The analysis examines long-term sales trends, product categories, prices, product origins and changes in consumer purchasing patterns over time. The project was developed as an exploratory data analysis exercise, with a particular focus on transforming raw tabular data into interpretable statistics and visualisations. The dataset consists of annual Systembolaget sales files containing product-level information such as category, price, volume, country of origin and sales volume. The original data is publicly available from Systembolaget's sales statistics and the datasets used in this analysis are also included in the repository.

The dataset used can be found in https://www.omsystembolaget.se/foretagsfakta/systembolaget-i-siffror/forsaljningsstatistik/ or in the same repository, in the "Systembolaget" folder.

## Dataset

The data contains information including:

- Product and article identifiers
- Product and producer names
- Product categories and subcategories
- Price
- Product volume
- Bottle/container type
- Country and region of origin
- Organic and ethical classifications
- Sales volume in litres
- Across the 16 annual files, the datasets contain approximately 15,000–47,000 observations per file, depending on the year and table.

## Project Goals

The analysis investigates several questions:

- How did Systembolaget's sales develop between 2009 and 2024?
- How did sales change during different periods?
- Which product categories account for the largest sales volumes?
- How have average product prices changed over time?
- How has the price of light lager changed since 2009?
- Which countries are the main origins of wine and beer sold in Sweden?
- Which spirit categories have the highest sales volumes?
- Can historical trends provide reasonable short-term forecasts of sales and prices?


## Results & Discussion

### Sales & Revenues 

Figure X shows Systembolaget's reported revenue between 2009 and 2024. Overall, revenue follows a clear upward trend throughout the period, with the exception of a decline in 2022. The most pronounced year-on-year increase occurred between 2019 and 2020, when revenue increased by approximately 13.6%.

<img width="456" alt="Снимок экрана 2025-05-21 в 14 52 55" src="https://github.com/user-attachments/assets/ccc71f2b-a0ca-46fd-9288-29d3e5d51548" />

![Revenue](https://github.com/user-attachments/assets/a1c48bcb-b035-439e-8a2d-a5c1612e012b)

We see that, with the exception of year 2022, the company's revenue has only grown. Observe the 13.6% procent jump from year 2019 to 2020, which looks anomalous. This is probably due to the COVID-19 pandemic that started in february 2020 in Sweden. It lasted around 2 years and most of the restrictions were lifted around the same month year 2022. While the restrictions in Sweden were milder than in any other country, there were certain restrictions that people had to follow. The relevant ones are number of people that were allowed to be in stores simultaneously (this concerns Systembolaget), bars closing at 20:00 and maximum number of people sitting at a table, which was 4. This, people's caution and desire to enjoy themselves by still being able to drink alcoholic beverages are what probably resulted in such a jump. There's also a chance that Systembolagets online sales grew as well. However, Systembolaget doesn't provide any such statistics. The situation normalised after year 2022, which can be observed on the graph. 

In order to predict the revenue for the next 5 years, I used the Darts module (a user friendly module in Python for forecasting) and the ARIMA model, AutoARIMA to be more specific since Darts' ARIMA model requires at least 30 data points and there are only 16 available at the moment. The ARIMA model is one of the basic models, but it is proven to be a good one. It is suitable since the revenue the data is non stationary (i.e. exhibits a trend, an upward trend to be specific) and has no seasonality. The last reason is why I didn't use SARIMA, for instance. Anyhow, the prediction for the revenue for years 2025-2030 is below. 

![Revenue prediction](https://github.com/user-attachments/assets/5a92a19d-6c27-4812-bf86-c19547c155bd)

It is probably hard to read off the values, but one can extract them by using the mean() function. The future revenues are 50,342,852,500 SEK, 51,690,479,000 SEK, 52,976,455,100 SEK, 54,333,607,100 SEK and 56,024,699,600 SEK. Of course, making predictions aren't easy. There are just too many variabls and things that may go wrong. After all, nobody expected the outbreak of the COVID-19 virus.

The increase coincides with the COVID-19 pandemic and the restrictions introduced in Sweden during 2020–2022. These included restrictions on the number of customers permitted in stores, restrictions on opening hours for bars and restaurants, and limitations on the number of people allowed to gather. Changes in consumer behaviour during this period may therefore have contributed to the unusually large increase in Systembolaget's revenue. However, the available data does not allow the effect of these factors to be isolated, and the observed increase should not be interpreted as evidence of a direct causal relationship. Systembolaget's publicly available sales statistics also do not provide sufficient information to determine the contribution of online sales to the change.
Revenue subsequently declined in 2022 before returning to an upward trajectory. This suggests that at least part of the unusually large increase observed in 2020 was temporary, although the longer-term upward trend remained.
Revenue Forecast
To obtain an indicative forecast of future revenue, an ARIMA model was fitted using the Darts forecasting framework. Auto-ARIMA was used to select the model specification. The annual dataset contains only 16 observations, which places substantial limitations on the reliability of long-term time-series forecasting. The model should therefore be regarded as an exploratory forecasting tool rather than a precise prediction of future revenue.
The historical series exhibits a clear trend but no obvious recurring seasonal pattern at the annual frequency. For this reason, a non-seasonal ARIMA model was used rather than a seasonal ARIMA specification.
The resulting forecasts for the following five years are approximately:
Year	Forecast revenue (SEK)
2025	50,342,852,500
2026	51,690,479,000
2027	52,976,455,100
2028	54,333,607,100
2029	56,024,699,600
The forecasts indicate continued revenue growth over the forecast horizon. However, they should be interpreted with considerable caution. With only 16 annual observations available for model fitting, there is limited information from which to estimate long-term dynamics or distinguish persistent trends from temporary changes. In addition, the model cannot anticipate structural changes in consumer behaviour, pricing, regulation, economic conditions or other unexpected events.
Consequently, the forecasts are best interpreted as an extrapolation of the historical revenue pattern under the assumptions of the fitted model, rather than as a definitive prediction of Systembolaget's future revenue.


### 3. 

The main alcoholc categories are Wine, Beer, cider & other drinks, Whisky and Alcohol free drinks. Below is a graph that shows how well each of the categories has been selling throughout the years.

![spirits](https://github.com/user-attachments/assets/204273f5-a15d-42f4-8d97-598dcd0181e7)

It's no suprise that Beer, cider & other drinks and Wine are the most dominating on the market. Then comes the Spirits (or liquer) category which is followed by the Alcohol free, which looks like the 0-line on this scale (but of course it is not). The Beer, cider & other drinks and Wine products outsell the Whisky products by as much as 7-10 times. One can also see (allegedly) the COVID-19 effect. It is clearly visible on the Beer, cider & other drinks line, a tad less on the wine line and practically invisble on the Whisky line, but this is due to the scale of the picture. Plotting only the Spirits and the Alcohol free drinks shows that the last category actually experienced decrease in sales during the 1st year of the pandemic, which is interesting. 

![Spirits+AlcFree](https://github.com/user-attachments/assets/44510a1c-18dc-4ee9-8be8-dedfa9ebc9f1)

### 4.

It is intersting to inspect average price of a bottle of alcohol. For this, I added a restriction - a bottle shouldn't be greater than 1000 ml. This is volume of most bottles/cans/packs that alcohol is sold in. Otherwise, Systembolaget also sells kegs and other products with more volume. 

![Avg_alc](https://github.com/user-attachments/assets/246cd786-131a-4c88-81a9-e53e68d337b9)

Anyway, it should come as no surprise that the Spirits category is the most expensive with the average price for a bottle being around 455 SEK in 2024. It follows then by the Wine (229 SEK), Alcohol free (31 SEK) and Beer, cider & other drinks (29 SEK). What is interesting here is the fact that a bottle of beer/cider/other is cheaper than its alcohol free counterpart. This wasn't the case 10 years ago (22.45 SEK vs 23.3 SEK), but the Alcohol free category saw a big price increase (from 22.45 SEK to 25.25 SEK) year 2016, which is 11% growth, while the Beer, cider & other drinks only grew 0.8% during the same period. We can also notice that the price curves became more steep the past few years. 

### 5.

Now, let's inspect light lager beer. After all, this is probably the most sold product. How much does a person in Sweden pay on average for a bottle a lager beer? For this, I tracked only the light lager beers that have been sold constantly during the years 2009-2024. There are only 62 such products. Thus, we can also investigate how price on the same beers has changed.

![Avg_lag](https://github.com/user-attachments/assets/270ae411-9d1a-4f99-b8c3-84bdf977555f)

It costed around 16 SEK in 2009 and now the average price is around 22 SEK which is a 27% increase. Once again, we can see that during the last few years, the curve became more steep. The increase was 6.3% during the years 2022 and 2023 and just 2.5% the last year. 

Now, what will be the average price in the future?


![Avg_lag_pred](https://github.com/user-attachments/assets/fb3cf92d-c8f6-4813-86c6-9eba9950b3b6)

The same model (ARIMA) predicts the following average prices for the next 5 years: 22.18 SEK, 22.48 SEK, 23.11 SEK, 23.39 SEK and 23.76 SEK. Percentually, the  growths are roughly between 1.1% and 2.7% which isn't anything outrageous and within the past frames. 

### 6.

Now, let's investigate the 2nd biggest alcohol group - wines. Below is a graph that shows top 7 countries whose wine customers prefered to buy the most. 

![wine](https://github.com/user-attachments/assets/6f46b9ef-e6b4-4a5e-8ea3-b5f97f9716da)

The market is dominated by the Italian wines which then is followed by the French and Spanish wines, which almost go neck and neck. But what is interesting to see on this graph is the decline of the sales of the South African and Australian wines. During the years 2009-2011, the two were #1 and #3, but ever since they steadily declined whereas the other sales either stayed unchanged or grew. Now, of course this doesn't necessarily imply that Systembolaget should waive these particular wines. After all, they are still the fourth and fifth biggest groups, but perhaps one could start thinking about decreasing the selection of the South African and Australian wines. To make decisions on what to constrain, one could look at how each wine from South Africa and Australia performs. 

However, this is only one alternative of what this decline might indicate. The other possibility is that Systembolaget itself started purchasing less of the South African and Australian wines and there's just much less to buy for customers. Although, this would mean that Systembolaget now buys ca 2 times less of these wines than 16 years ago. In order to find out if this is true one would need to investigate wine purchase data which is unfortunately unavailable since this isn't something Systembolaget shares.

Finally, here are top 20 countries in the same category.

![wine1](https://github.com/user-attachments/assets/0f654445-c753-4ce9-bed3-ac8cf4219f20)

### 7. 

What are the most popular liquer groups? Systembolaget categorises things differently prior and after to the year 2016 for some reason. That's why I investigated the data from the year 2016 and beyond.

![spirits](https://github.com/user-attachments/assets/7609e38d-0d28-4139-9edf-ea9aec594a4b)

The categories Drinks & Cocktails (which is mostly comprised of other liquers than whisky such as gin, vodka, rum, etc) and Whisky lead the sales and one can also see noticeable jumps around the years of the pandemic. After 2022, there's a small decrease in sales of these 2 categories. 

### 8. 

Finally, let's investigate the beer subcategory. It is strongly dominated by the Swedish beers (what a surprise, huh?) to the extent that one can't really see the other countries except for the "International marks" which represent beers brewed in multiple countries. 

![beer1](https://github.com/user-attachments/assets/ebf47ba4-3d4c-4e93-9065-c305dc0fe1dd)


Excluding these two, this is the picture that we get.

![beer](https://github.com/user-attachments/assets/6b8d4315-5ec8-4f36-84b3-d07fe51b8c14)

The 2 biggest groups are Czech and German beers which shouldn't be surprising. The two countries produce lots of widely known beers which are sold worldwide. On the other hand, the Italian beers emerged as the number 3 previous years which is unexpected. What is also unexpected is the decline of the American beers as this subcategory also has some famous beers. However, I found that this decline is not as severe as the graph suggests. The main issue here is that Systembolaget started labeling certain beers as "International marks" since the beers started to be brewed in multiple countries (or for other reasons). For this, I investigated the Brooklyn Brewery which is one of the biggest beer sellers to both Sweden and Europe. I noticed that Systembolaget started labeling some of their beers as "International" around year 2018. It turns out that the "International" beers by the Brooklyn Brewery were as much as 46% of the entire American beer sales during previous year. Now, if one tracks all (originally) American beers that are labeled now as "International" and adds their sales to the sales of the American beers, the number of liters of the American beers sold rises from 1,694,503.242 to 3,815,795.649 which is 225% difference. But still, there's a decline of the American beers sold. It will also be interesting to see whether the number will drop even more due to the American foreign policy, their imposed tariffs and reluctance of many Swedes to buy American products. 
