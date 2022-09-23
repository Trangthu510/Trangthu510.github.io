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

## Single Linear Regression:
- For my analysis, 60 countries were randomly selected and 2018 life expectancy at birth, general government health expenditure (% of GDP), and total alcohol consumption (liters of pure alcohol, projected estimated, 15+ years of age) were collated.

- For the y-value, life expectancy at birth, there was a mean of 71.85 years in the 60 country sample and a standard deviation of 8.07 indicating the spread. 

- For the x-value, domestic general government health expenditure , there was a mean of 3.54% of GDP worldwide and a standard deviation of 2.45 indicating the spread. 

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

