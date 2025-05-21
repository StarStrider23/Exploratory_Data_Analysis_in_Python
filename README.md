# Exploratory Data Analysis in Python

Project by Alexsey Chernichenko

## Project Background and Overview

This is an exploratory data analysis of Systembolagets sales during the years 2009 - 2024. Systembolaget is a government-owned chain of liquor stores in Sweden. It is the only retail store allowed to sell alcoholic beverages that contain more than 3.5% alcohol by volume. 

The dataset used can be found in https://www.omsystembolaget.se/foretagsfakta/systembolaget-i-siffror/forsaljningsstatistik/

Overall there are 16 files, each with 17 columns and around 15k to 47k rows (depending on table). 

## Metrics 

- Artnr - Item number, unique to each item

- Varunr - Product number, not unique to each item, but shared between the same products which differ in some way (volume, for instance)

- Kvittonamn - Receipt name

- Namn - Name of the item

- Producentnamn - Alcohol beverage companies

- Varugrupp - Alcohol category

- Varugrupp detalj - Alcohol subcategory

- Rubrik - Yet another subcategory
 
- Aktuellt pris - Price 

- Volym i ml - Volume of the bottle in ml

- Buteljtyp - Bottle type

- Land - Country where the beverage was made

- Region - Country's region

- Ursprung - Origin (for most of the items it is the same as Country or Region)

- Ekologisk - Ecological (for products that were made according to necessary ecological rules)

- Etiskt - Ethical (Haven't found any specific information about this label)

- Försäljning i liter - Sales in liters 

- Artikel ID - Item's ID (yet another unique number)

## Project Goals

The goal of the project is to analyse Systembolagets sales by studying and answering the following questions:

1. What was the revenue of Systembolaget during the years 2009-2024? How did it change percentually?

2. What will be the company's revenue in the next 5 years?

3. What are the main categories of the alcohol and how well does they sell?

4. What is the average price of a bottle of alcohol and how has it changed throughout the years?

5. What is the average price of a bottle of lager beer and how has it changed throughout the years? What will be the prices in 2025-2030?

6. What are the origins of wines that are sold the most?

7. What are the most bought categories of the liquer?

8. What are the origins of the beers that are sold the most?


## Results

### 1+2. 

Below are Systembolagets revenue (in SEK) for the years 2009-2024. 


<img width="456" alt="Снимок экрана 2025-05-21 в 14 52 55" src="https://github.com/user-attachments/assets/ccc71f2b-a0ca-46fd-9288-29d3e5d51548" />



![Revenue](https://github.com/user-attachments/assets/a1c48bcb-b035-439e-8a2d-a5c1612e012b)

We see that, with the exception of year 2022, the company's revenue has only grown. Observe the 13.6% procent jump from year 2019 to 2020, which looks anomalous. This is probably due to the COVID-19 pandemic that started in february 2020 in Sweden. It lasted around 2 years and most of the restrictions were lifted around the same month year 2022. While the restrictions in Sweden were milder than in any other country, there were certain restrictions that people followed. The relevant ones are number of people that were allowed to be in stores simultaneously (this concerns Systembolaget), bars closing at 20:00 and maximum number of people sitting at a table, which was 4. This, people's caution and desire to enjoy themselves by still being able to drink alcoholic beverages are what probably resulted in such a jump. There's also a chance that Systembolagets online sales grew as well. However, Systembolaget doesn't provide any such statistics. The situation normalised after year 2022, which can be observed on the graph. 

In order to predict the revenue for the next 5 years, I used the darts module and the ARIMA model, AutoARIMA to be more specific since dart's ARIMA model requires at least 30 data points and there are only 16 available at the moment. The ARIMA model is one of the basic models, but it is proven to be a good one. It is suitable since the revenue the data is non stationary (i.e. exhibits a trend, an upward trend to be specific) and has no seasonality. The last reason is why I didnät use SARIMA, for instance. Anyhow, the prediction for the revenue for years 2025-2030 is below. 

![Revenue prediction](https://github.com/user-attachments/assets/5a92a19d-6c27-4812-bf86-c19547c155bd)

It is probably hard to read off the values, but one can extract them by using the mean() function. The future revenues are 50,342,852,500 SEK, 51,690,479,000 SEK, 52,976,455,100 SEK, 54,333,607,100 SEK and 56,024,699,600 SEK. Of course, making predictions aren't easy. There are just too many variabls and things that may go wrong. After all, nobody expected the outbreak of the COVID-19 virus.

### 3. 

The main alcoholc categories are Wine, Beer, cider & other drinks, Whisky and Alcohol free drinks. Below is a graph that shows how well each of the categories has been selling throughout the years.

![Alc_cat](https://github.com/user-attachments/assets/1299618e-1c1e-4133-acec-f7658a04e2f1)

It's no suprise that Beer, cider & other drinks and Wine are the mst dominating on the market. Then comes the Spirits (or liquer) category which is followed by the Alcohol free, which looks like 0 on this scale (but of course it is not). The Beer, cider & other drinks and Wine products outsell the Whisky products by as much as 7-10 times. One can also see (allegedly) the COVID-19 effect. It is clearly visible on the Beer, cider & other drinks line, a tad less on the wine line and practically invisble on the Whisky line, but this is due to the scale of the picture. Plotting only the Spirits and the Alcohol free drinks shows that the last category actually experienced decrease in sales during the 1st year of the pandemic, which is interesting. 

![Spirits+AlcFree](https://github.com/user-attachments/assets/70a4ec1c-d716-4316-b2e0-493816b39f69)

### 4.

It is intersting to inspect average price of a bottle of alcohol. For this, I added a restriction - a bottle shouldn't be greater than 1000 ml. This is volume of most bottles/cans/packs that alcohol is sold in and Systembolaget also sells kegs and other products with more volume. 

![Avg_alc](https://github.com/user-attachments/assets/246cd786-131a-4c88-81a9-e53e68d337b9)

Anyway, it should come as no surprise that the Spirits category is the most expensive with the average price for a bottle being around 455 SEK at year 2024. It follows then by the Wine (229 SEK), Alcohol free (31 SEK) and Beer, cider & other drinks (29 SEK). What is interesting here is the fact that a bottle of beer/cider/other is cheaper than its Alcohol free counterpart. This wasn't the case 10 years ago (22.45 SEK vs 23.3 SEK), but the Alcohol free category saw a big price increase (from 22.45 SEK to 25.25 SEK) year 2016, which is 11% growth, while the Beer, cider & other drinks only grew 0.8% during the same period. We can also notice that the price curves became more steep the past few years. 

### 5.

Now, let's inspect light lager beer. After all, this is probably the most sold product. How much does a person in Sweden pay on average for a bottle a lager beer? For this, I tracked only the beers that have been sold constantly during these years. There are only 62 such products. Thus, we can also investigate how price on the same beers has changed.

![Avg_lag](https://github.com/user-attachments/assets/270ae411-9d1a-4f99-b8c3-84bdf977555f)

It costed around 16 SEK in 2009 and now the average price is around 22 SEK which is a 27% increase. Once again, we can see that during the last few years, the curve became more steep. The increase was 6.3% during the years 2022 and 2023 and just 2.5% the last year. 

Now, what will be the average price in the future?


![Avg_lag_pred](https://github.com/user-attachments/assets/fb3cf92d-c8f6-4813-86c6-9eba9950b3b6)

The same model (ARIMA) predicts the following average prices for the next 5 years: 22.18 SEK, 22.48 SEK, 23.11 SEK, 23.39 SEK and 23.76 SEK. Percentually, the  growths are roughly between 1.1% and 2.7% which isn't anything outrageous and within the past frames. 

### 6.

Now, let's investigate the 2nd biggest alcohol group - wines. Below is a graph that shows top 7 countries whose wine customers prefered to buy the most. 

![wine](https://github.com/user-attachments/assets/d0d7dc1f-2438-4793-85d2-9f5b62518120)

The market is dominated by the Italian wines which then is followed by the French and Spanish wines, which almost go neck to neck. But what is interesting to see on this graph is the decline of the sales of the South African and Australian wines. During the years 2009-2011, the two were #1 and #3, but ever since they steadily declined whereas the other sales either stayed unchanged or grew. Now, of course this doesn't necessarily imply that Systembolaget should waive these particular wines. After all, they are still the fourth and fifth biggest groups, but perhaps one could start thinking about decreasing the selection of the South African and Australian wines. To make decisions on what to constrain, one could look at how each wine from South Africa and Australia performs. 

However, this is only one alternative of what this decline might indicate. The other possibility is that Systembolaget itself started buying less of the South African and Australian wines and there's just much less to buy. Although, this would mean that Systembolaget now buys ca 2 times less of these wines than 16 years ago. In order to find out if this is true one would need to investigate delivery data which is unfortunately unavailable. 

Finally, here are top 20 countries in the same category.

![wine1](https://github.com/user-attachments/assets/f90a799c-b332-4748-8d52-0e8d21f50929)

### 7. 

What are the most popular liquer groups? Systembolaget categorises things differently prior and after to the year 2016 for some reason. That's why I investigated the data from the year 2016 and after.

![spirits](https://github.com/user-attachments/assets/7609e38d-0d28-4139-9edf-ea9aec594a4b)

The categories Drinks & Cocktails (which mostly is comprised of other liquers than whisky such as gin, vodka, rum, etc) and Whisky lead the sales and one can also see noticeable jumps around the years of the pandemic. After 2022, there's a small decrease in sales of these 2 categories. 

### 8. 

Finally, let's investigate the beer subcategory. It is strongly dominated by the Swedish beers (what a surprise, huh?) to the extent where one can't really see the other countries except for the "International marks" which represent beers brewed in multiple countries. 

![beers](https://github.com/user-attachments/assets/101f228a-f99f-4610-9287-18c53fef2e73)

Excluding these two, this is the picture that we get.

![beers1](https://github.com/user-attachments/assets/cf90f37a-155f-4241-b2c0-7d1d9f3c3dad)

The 2 biggest groups are Czech and German beers which shouldn't be surprising. The two countries produce lots of widely known beers which are sold worldwide. On the other hand, the Italian beers emerged as the number 3 previous years which is unexpected. What is also unexpected is the decline of the American beers as this subcategory also has some famous beers. However, I found that this decline is not as severe as the graph suggests. The main issue here is that Systembolaget started labeling certain beers as "International marks" since the beers started to be brewed in multiple countries (or for other reasons). For this, I investigated the Brooklyn Brewery which is one of the biggest beer sellers in Sweden and Europe. I noticed that Systembolaget started labeling some of their beers as "International" around year 2018. It turns out that the "International" beers by the Brooklyn Brewery were as much as 46% of the entire American beer sales during previous year. Now, if one tracks all (originally) American beers that are labeled now as "International" and sums their sales with the sales of the American beers, the number of liters of the American beers sold rises from 1,694,503.242 to 3,815,795.649 which is 225% difference. But still, there's a decline of the American beers sold. It will also be interesting to see whether the number will drop even more due to the American foreign policy, their imposed tariffs and reluctance of many Swedes to buy American products. 
