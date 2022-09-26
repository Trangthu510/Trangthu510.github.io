---
layout: post
title: Life Expectancy and Related Variables
author: [Trang Duong]
categories: [Statistic]
tags: [alcohol, life, heath-expenditure]
math: true
---

**Howdy!** Just a fun fact: "48% of people worldwide, aged over 15, claim to have never drunk alcohol"
{: .message }

- toc
{: toc }

## Introduction:
The pandemic has brought huge attention to the worldwide human wellness. One of the crucial indicators is life expectancy at birth. Life expectancy at birth reflects life expectancy at the point in time the data is collected. This number is calculated using life tables that contain the death rates of different age groups (ie. ages: 1-5, 5-10, 10-15, etc) in a certain year that are then averaged to estimate life expectancy for people born in that year.
The World Bank Open Data collects worldwide life expectancy at birth data, along with other measures of world health issues using information from the United Nations Populations Division.. So what individual factors affect life expectancy? In reality there are infinite factors that could impact longevity. Being able to identify correlation between different factors and life expectancy can help governments and aid agencies instigate widespread improvements in life expectancy. Our project explores the relationship between life expectancy at birth (years) , domestic general government health expenditure (% of GDP) and total alcohol consumption (liters of pure alcohol, projected estimated, 15+ years of age) within a random sample of records from 60 countries based on 2018 data from the World Bank Open Data. Before randomly selecting 60 countries, entities with missing data (zero values) were removed. Additionally there is not always consensus on what constitutes a country- countries with disputed/controversial borders were removed from the pool.

First, a single linear regression was produced, with the explanatory variable (X) of government health expenditure and response variable (Y) of life expectancy, 2018. An R2 value of .41 indicates 41% of the variation in life expectancy can be predicted by domestic government health expenditure. The R value of .61 shows moderate positive correlations between the variables. A paired t-test found there was enough evidence to show a linear relationship.

To improve the model, alcohol consumption was added as an additional explanatory variable to create a multiple linear regression model. However, we did not find that the MLR model was significantly better than the SLR model. Further investigation showed that alcohol consumption and government health expenditure had a linear relationship creating an issue with multicollinearity. This highlights a main difficulty in creating a model to explain life expectancy. A MLR should not be built with collinear explanatory variables. Future work would be to explore additional variables such as crime rates or average distance to a hospital to see if they can predict life expectancy in a MLR model. Given the results of the SLR, we would recommend keeping government health expenditure as a possible explanatory variable, but removing alcohol consumption. A more experienced statistician would know to check for collinearity before creating a MLR model.

## What variable may have a relationship with life expectancy?
- Health Spending
* WHO tracks health spending in three main categories by country: government, external, private
* 522 page methodology guide
- Focus on: Domestic Government Health Expenditure (% of GDP)
* Sample Mean of ~3%, some spending much more


## Single Linear Regression:
- For my analysis, 60 countries were randomly selected and 2018 life expectancy at birth, general government health expenditure (% of GDP), and total alcohol consumption (liters of pure alcohol, projected estimated, 15+ years of age) were collated.

- For the y-value, life expectancy at birth, there was a mean of 71.85 years in the 60 country sample and a standard deviation of 8.07 indicating the spread. 

- For the x-value, domestic general government health expenditure , there was a mean of 3.54% of GDP worldwide and a standard deviation of 2.45 indicating the spread. 

### Scatterplot and linear regression line for (x, y)
Y: 2018 Life Expectancy at birth, total (years)
X: 2018 Domestic general government health expenditure (% of GDP) Y=2.1313X+64.3

### T-test and Confidence Interval:
- T-test
Ho: B1 = 0 or Domestic Government Health Expenditure has no relationship with Life Expectancy at birth without any other explanatory variables in the model.
Ha: B1 ≠ 0 or Domestic Government Health Expenditure has a significant relationship with Life Expectancy at birth without any other explanatory variables in the model.
alpha= 0.05
Test statistic for t-test has the p-value is: 2.3355E-08 < 0.05
Reject Ho. There is significant evidence for the existing relationship between the explanatory variable (Domestic Government health expenditure) and the response variable (Life Expectancy at birth), meaning that there is a linear relationship between two variables.
Additionally, a confidence and prediction interval were created for a random X value with the range of the sample data. Creation of the prediction intervals is an indicator how the model could be used to predict life expectancy using an additional country’s government health expenditure data.
Calculations:
Xp = 4 (randomly selected within range [0.4258, 9.9462]), Y-bar = 72.8252(by equation), Sxx=354.3828, s=2.4508, t value=2 at df=58
- 95% Confidence Interval for E(yp)
Lower bound=72.8252-2*2.4508*sqrt(1/60+(4-3.5431)^2/354.3828)=72.18 Upper bound=72.8252+2*2.4508*sqrt(1/60+(4-3.5431)^2/354.3828)=73.47 Therefore, 72.18< E(yp)|Xp = 4 <73.47.
The 95% confidence interval for E(yp) is between 72.18 and 73.47 at Xp = 4.
- 95% Prediction Interval for yp
Lower bound = 72.8252-2*2.4508*sqrt(1+1/60+(4-3.5431)^2/354.3828) = 67.8815 Upper bound = 72.8252+2*2.4508*sqrt(1+1/60+(4-3.5431)^2/354.3828) = 77.7689 Therefore, 67.8815< yp < 77.7689.
The 95% prediction interval for yp is between 67.8815 and 77.7689 at Xp = 4.

### Conclusion: 
Based on the ANOVA and T-test there is evidence for a linear relationship between Domestic Government health expenditure and life expectancy. This makes sense given the shape of the scatterplot. It should be noted that given the size of the dataset, and complexity required to calculate life expectancy and health expenditure, it is impossible to independently verify that each of the 60 countries collects this data accurately and in a way that allows for comparison. Verification would require time and resources well beyond the scope of this project. However an r-squared value of only 41% means that much of the variation in life expectancy can not be predicted by health expenditure alone. Adding in additional variables to create a multiple linear regression may create a model that can better predict variation in life expectancy. Alcohol consumption is a good additional variable because alcohol is consumed worldwide , has an impact on health and behaviors, and consumption patterns can vary greatly around the globe.

## Multi Linear Regression:
In order to better account for the variation of life expectancy, alcohol consumption was added to the model as an additional explanatory variable to produce a multiple linear regression model.
Total alcohol consumption data is provided by the World Health Organization which in turn collects data from government organizations and industry researchers- such as the IWSR International Wine and Spirit Research. There are not set standards for how countries collect this data which create shortcomings - there are potentially widely different sampling standards used. Additionally, asking people to self report can create inaccuracies. Industry research and sales records can come up short, especially in countries where ‘moonshine’ and/or illegally produced alcohol is common.

## Estimated Regression model:
Y: 2018 Life Expectancy at birth, total (years)
X1: 2018 Domestic general government health expenditure (% of GDP)
X2: 2018 Total Alcohol Consumptions per capita (liters of pure alcohol, projected estimates, 15+ years of age)
ŷ = 2.0568X1 + 0.11X2 + 63.9175

## Conclusion:
Conclusions
Both explanatory variables have a significant relationship with life expectancy. However, using both explanatory variables in a multiple linear regression model will not yield significantly better results than using a SLR with government health expenditure. Further investigation shows that multicollinearity becomes an issue when using alcohol consumption and government health expenditure as explanatory variables in the same MLR. With additional time and resources a better MLR model could be created using government health expenditure and other explanatory variables, given that additional variables are checked for collinearity. Additionally, with more time and resources more could be done to ensure the 60 countries selected do not contain any outliers. A deeper look into the collection methodology employed in certain countries could find that their methods are too different to allow for this type of analysis. Also looking at the life expectancy of countries overtime could allow for creatiation of a more meaningful model than 2018 data alone. A multitude of other variables could be explored to try and explain life expectancy such as average happiness, climate/weather conditions, crime rates and many more.

### Tables

A

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

