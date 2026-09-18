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

The table and the figure below show Systembolaget's reported revenue between 2009 and 2024. Overall, revenue follows a clear upward trend throughout the period, with the exception of a decline in 2022. The most pronounced year-on-year increase occurred between 2019 and 2020 when revenue increased by approximately 13.6%.

<img width="456" alt="Снимок экрана 2025-05-21 в 14 52 55" src="https://github.com/user-attachments/assets/ccc71f2b-a0ca-46fd-9288-29d3e5d51548" />

<img width="1200" height="400" alt="446110114-a1c48bcb-b035-439e-8a2d-a5c1612e012b" src="https://github.com/user-attachments/assets/23df05a7-d3c9-46e4-8d01-b4af8863aa77" />


The increase coincides with the COVID-19 pandemic and the restrictions introduced in Sweden during 2020–2022. These included restrictions on the number of customers permitted in stores, restrictions on opening hours for bars and restaurants, and limitations on the number of people allowed to gather. Changes in consumer behaviour during this period may therefore have contributed to the unusually large increase in Systembolaget's revenue. However, the available data does not allow the effect of these factors to be isolated, and the observed increase should not be interpreted as evidence of a direct causal relationship. Systembolaget's publicly available sales statistics also do not provide sufficient information to determine the contribution of online sales to the change.
Revenue subsequently declined in 2022 before returning to an upward trajectory. This suggests that at least part of the unusually large increase observed in 2020 was temporary, although the longer-term upward trend remained.

To obtain an indicative forecast of future revenue, an ARIMA model was fitted using the Darts forecasting framework. Auto-ARIMA was used to select the model specification. The annual dataset contains only 16 observations, which places substantial limitations on the reliability of long-term time-series forecasting. The model should therefore be regarded as an exploratory forecasting tool rather than a precise prediction of future revenue.

![Revenue prediction](https://github.com/user-attachments/assets/5a92a19d-6c27-4812-bf86-c19547c155bd)

The historical series exhibits a clear trend but no obvious recurring seasonal pattern at the annual frequency. For this reason, a non-seasonal ARIMA model was used rather than a seasonal ARIMA specification.

The resulting forecasts for the following five years are approximately:

| Year | Forecast revenue (SEK) |
| ---- | ---------------------- |
| 2025 |	50,342,852,500        |
| 2026 |  51,690,479,000        |
| 2027 |	52,976,455,100        |
| 2028 |	54,333,607,100        |
| 2029 |	56,024,699,600        |

The forecasts indicate continued revenue growth over the forecast horizon. However, they should be interpreted with considerable caution. With only 16 annual observations available for model fitting, there is limited information from which to estimate long-term dynamics or distinguish persistent trends from temporary changes. In addition, the model cannot anticipate structural changes in consumer behaviour, pricing, regulation, economic conditions or other unexpected events.

Consequently, the forecasts are best interpreted as an extrapolation of the historical revenue pattern under the assumptions of the fitted model, rather than as a definitive prediction of Systembolaget's future revenue.


### Sales by Main Alcohol Category 

The main alcohol categories in the dataset are Wine, Beer, Cider & Other Drinks, Spirits, Whisky, and Alcohol-Free Drinks. The figure below shows how sales in these categories have developed over the period 2009–2024.

![spirits](https://github.com/user-attachments/assets/204273f5-a15d-42f4-8d97-598dcd0181e7)

As expected, Beer, Cider & Other Drinks and Wine account for the largest volumes of sales throughout the period. The Spirits category follows, while Alcohol-Free Drinks represent a substantially smaller volume and therefore appear close to the zero line on the full-scale plot.

The difference between the largest and smaller categories is substantial: Beer, Cider & Other Drinks and Wine consistently sell several times more litres than Whisky. This difference in scale makes some of the changes in the smaller categories difficult to observe in the combined plot.

The period around 2020 also shows changes in several categories that coincide with the COVID-19 pandemic. The increase is particularly visible for Beer, Cider & Other Drinks and somewhat less pronounced for Wine. The effect is much harder to identify for Whisky because of the scale of the graph.

To examine the smaller categories in more detail, a separate plot was created for Spirits and Alcohol-Free Drinks. 

![Spirits+AlcFree](https://github.com/user-attachments/assets/44510a1c-18dc-4ee9-8be8-dedfa9ebc9f1)

The plot reveals that Alcohol-Free Drinks actually experienced a decline in sales during the first year of the pandemic. This contrasts with the overall increase observed in some of the larger categories and demonstrates why examining the categories separately can reveal patterns that are difficult to see in an aggregated plot.

These observations describe changes in sales volumes over time, but they do not by themselves establish the causes behind those changes. In particular, the data cannot distinguish between changes in consumer preferences, product availability, pricing, purchasing behaviour and other external factors.

### Average Product Prices by Category.

The next analysis examines how the average price of products has changed over time. To avoid products such as kegs and other large-volume packages distorting the comparison, products with a volume greater than 1,000 ml were excluded.

![Avg_alc](https://github.com/user-attachments/assets/246cd786-131a-4c88-81a9-e53e68d337b9)

In 2024, the Spirits category had by far the highest average product price, at approximately 455 SEK, followed by Wine at approximately 229 SEK. Alcohol-Free Drinks and Beer, Cider & Other Drinks had substantially lower average prices, at approximately 31 SEK and 29 SEK, respectively.

One interesting observation is that the average product price of Beer, Cider & Other Drinks is now slightly lower than that of Alcohol-Free Drinks. This was not the case at the beginning of the period. Around 2009, the corresponding averages were approximately 22.45 SEK for Beer, Cider & Other Drinks and 23.30 SEK for Alcohol-Free Drinks.

The difference between the two categories changed considerably over the following years. The average price of Alcohol-Free Drinks increased from approximately 22.45 SEK to 25.25 SEK in 2016, while the corresponding increase for Beer, Cider & Other Drinks was much smaller. This represents an increase of approximately 12% for Alcohol-Free Drinks over that period, compared with less than 1% for Beer, Cider & Other Drinks.

The price series also appear to become steeper in the later years, suggesting that average product prices have increased more rapidly in the most recent part of the dataset.

It is important to note that these figures represent average prices per product, rather than prices adjusted for the volume sold. Changes in the composition of products available in each category can therefore affect the averages. The results should consequently be interpreted as changes in the observed average product price rather than as a direct measure of inflation or changes in the price of an identical basket of products.

### Lighter Lager Prices

The next analysis focuses specifically on light lager beer. To investigate how prices have changed for comparable products, only light lager products that were present continuously throughout the entire period from 2009 to 2024 were included. This resulted in a set of 62 products.

![Avg_lag](https://github.com/user-attachments/assets/270ae411-9d1a-4f99-b8c3-84bdf977555f)

The average price of these products was approximately 16 SEK in 2009, compared with approximately 22 SEK in 2024, corresponding to an increase of roughly 27% over the period. As with the broader category analysis, the price increase appears to have become more pronounced in recent years. Between 2022 and 2023, the average price increased by approximately 6.3%, followed by an increase of approximately 2.5% in 2024.


![Avg_lag_pred](https://github.com/user-attachments/assets/fb3cf92d-c8f6-4813-86c6-9eba9950b3b6)

An ARIMA model was also used to produce an exploratory forecast of the average price for the following five years. The predicted values are:

| Year | Forecast average price |
| ---- | ---------------------- |
| 2025 |	22.18 SEK             |
| 2026 |	22.48 SEK             |
| 2027 |	23.11 SEK             |
| 2028 |	23.39 SEK             |
| 2029 |	23.76 SEK             |

The corresponding year-on-year increases are approximately 1.1–2.7%, depending on the year. These increases are within the range observed historically, although the recent period has also contained larger individual changes.

As with the revenue forecast, this should be regarded as an exploratory extrapolation rather than a precise prediction. The model is based on a relatively short annual time series, and future prices can be affected by factors that are not captured by the historical series.

### Wine Sales by Country of Origin.


Wine is the second-largest alcohol group by sales volume in the dataset. The figure below shows the seven countries whose wines accounted for the largest sales volumes during the period.

![wine](https://github.com/user-attachments/assets/6f46b9ef-e6b4-4a5e-8ea3-b5f97f9716da)

Italy consistently dominates the category, followed by France and Spain, whose sales volumes are relatively close to one another.
A notable pattern is the decline in sales associated with South African and Australian wines. Both countries were among the largest groups at the beginning of the period. During 2009–2011, South African and Australian wines ranked approximately first and third, respectively, whereas their relative sales volumes subsequently declined while several other countries remained stable or increased.
The observed decline could potentially be relevant when considering the composition of the product assortment. However, sales data alone are not sufficient to determine whether the decline reflects lower consumer demand, changes in the available product selection, changes in pricing or other factors.

For example, one possible explanation would be that Systembolaget offers fewer products from these countries than it did previously. If this were the case, lower sales would not necessarily indicate a corresponding decline in consumer demand. Unfortunately, the available sales data do not contain sufficient information about Systembolaget's historical purchasing decisions to distinguish between these explanations.

A more detailed analysis could therefore examine individual products from South Africa and Australia and investigate whether their sales declined individually or whether the decline is primarily associated with changes in the number of products available. Such an analysis would provide additional context for the aggregate country-level trends.
The figure below shows the twenty countries with the highest wine sales volumes over the period.

![wine1](https://github.com/user-attachments/assets/0f654445-c753-4ce9-bed3-ac8cf4219f20)

### Sales of Spirit and Liqueur Categories 

The classification of spirit and liqueur products changed between the earlier and later parts of the dataset. To avoid mixing different classification systems, this analysis focuses on the period from 2016 onwards, for which the categories are more consistently defined.
The results show that Drinks & Cocktails and Whisky account for the largest sales volumes among the categories examined. Both categories also show noticeable changes around the period of the COVID-19 pandemic.

![spirits](https://github.com/user-attachments/assets/7609e38d-0d28-4139-9edf-ea9aec594a4b)

Following 2022, sales in both categories show a modest decline. This pattern is visible in the data, although the analysis does not establish whether it was caused by changes in consumer behaviour, product availability, pricing or other factors.

The results illustrate the importance of taking changes in the underlying classification system into account when comparing categories over long periods. Restricting this analysis to the more consistently classified period reduces the risk of interpreting changes caused by reclassification as genuine changes in consumer demand.

### Beer Sales by Country of Origin 

The final analysis examines the country of origin of beer products. The category is strongly dominated by Swedish beers, making the differences between many of the other countries difficult to observe on the full-scale graph. Another substantial category is International, which contains beers associated with production in multiple countries or products whose classification has changed over time.

![beer1](https://github.com/user-attachments/assets/ebf47ba4-3d4c-4e93-9065-c305dc0fe1dd)


To make the differences between the remaining countries easier to examine, Swedish and International beers were excluded from the second plot.

![beer](https://github.com/user-attachments/assets/6b8d4315-5ec8-4f36-84b3-d07fe51b8c14)

Among the remaining countries, Czech and German beers account for some of the largest sales volumes. Italian beers have also become one of the larger groups in more recent years. In contrast, the data show a substantial decline in the recorded sales of American beers.
However, the decline in the American category appears to be partly affected by changes in classification. To investigate this, the sales history of Brooklyn Brewery products was examined as an example. Some Brooklyn Brewery products were classified as American beers in earlier years but were subsequently classified as International.

The effect can be substantial. In the analysis, products that were originally classified as American but later appeared under the International category accounted for a significant share of the recorded American beer sales. When these products are added back to the American category, the measured sales volume increases from approximately 1.69 million litres to 3.82 million litres, corresponding to roughly 225% of the original recorded volume.

This adjustment suggests that the decline in recorded American beer sales is partly a consequence of classification changes rather than a direct measure of declining demand for American beer. Nevertheless, even after accounting for the identified reclassified products, the adjusted series still shows a decline compared with earlier years.

The classification issue highlights an important limitation of analysing the raw country categories directly. Products can change classification when their production arrangements, labelling or other characteristics change, meaning that a change in the recorded category does not necessarily correspond to a change in consumer preferences.

It would be interesting to examine whether the sales of American-origin beers continue to change in subsequent years. However, attributing future changes to political developments, tariffs or consumer attitudes would require additional data on these factors. The present dataset alone cannot establish such a relationship.

Overall, the beer analysis demonstrates that aggregate category trends need to be interpreted together with the underlying product-level data. In this case, examining individual products helped reveal that at least part of the apparent decline in American beer sales was related to changes in classification rather than sales alone.
