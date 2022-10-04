---
layout: post
title: AMPL APPLICATION IN MINIZING COST FOR DIETARY SOLUTION
author: [Trang Duong]
categories: [Optimization]
tags: [diet, minimum-cost, heathy]
math: true
---
**DO YOU KNOW WHAT !!?** "A BALANCED DIET IS HAVING FOOD ON BOTH HANDS"
{: .message }

- toc
{: toc }

## INTRODUCTION:
**'Dietary'** has always been a nightmare of everyone in this World.
- How to be balance between **favorite food** and **healthy food**?
- How to eat a lot without getting **fat**?
- How to have good food without paying a lot of **money**?
- How we know exactly amount of food should we eat?

A thousand questions are asked everyday by everyone and to be able to answer all of them, we need to **PAYING ATTENTION!!,** **DOING LOT OF RESEARCH,** and of course even **PAYING MONEY** just to get an answer.

This is the reason why I was strong interested in finding the answer and solving this problem. This small project is created based on setting up **a complex mathematical question**, using **AMPL** application to solve.
The data set contained very basic information about nutritions of **PARTS OF MY FAVORITE FOOD COLLECTION**.

Please enjoy my calculation and may be you will find out how interesting the project is :D :D.

## DATA FOR THE QUESTION:
I collected some main information about a list of foods nutrtions quantities.
The Food's characteristic included amount of: PROTEIN, FAT, FIBER, SUGAR and PRICE. The unit of all factors is counted per 100gr of food.

I have done some basic research to get these information from online websites: 
- <p><a href="https://www.fatsecret.com/Default.aspx/">100% FREE CALORIE COUNTER</a></p>
- <p><a href="https://www.nutritionix.com/">NUTRITIONIX TRACK APP</a></p>

And of course, all prices are recorded through **WHOLE FOOD MARKET** website, that I believe in their good quality of organic foods.

<img src="/assets/AMPL-photos/Food-data.png" alt="Food Nutritions" width="636" height="388">

## HOW TO IMPLEMENT THE QUESTION INTO AMPL:
### .mod/.dat/.run:
Creating three main types of compulsory files is the first step to implement the problem into AMPL.
By creating a model for the question, I was able to define the subjects, constraints and parameters of the problem. Specifically in this problem, I want to minimize the cost of grocery per day which still allow me to satisfy all requirements for Food's nutritions.

<img src="/assets/AMPL-photos/mod-file.png" alt="Example Model" width="621" height="384">

.dat file is a specific file for creating database. There is one limit of AMPL that you cannot copy or import data from other sources to AMPL. However, data related to optimization problem in basic level are not complicated because otherwise the mathematic within the problem will cause confusing for everyone.

<img src="/assets/AMPL-photos/dat-file.png" alt="Example Data Limit" width="646" height="468">

When you think about a problem, you need to know exactly what you wanna find out from the problem, what kind of limit will be suitable for you or even your company's problem.

## RESULT OF THE PROBLEM:
After running all the files on AMPL Console, I get the result as the picture below:

<img src="/assets/AMPL-photos/optimal-solution.png" alt="Result" width="612" height="301">

The result is an optimal solution to minimize the cost but at the same time satisfy all the requirements. 
Since the unit of all parameter is per 100gr, therefore, as the solution, I should eat per day:
- 50gr Broccoli
- 292gr Carrot
- 50gr Cereal
- 100gr Egg (equals to 2 eggs)
- 118gr Ground Pork
- 9gr Pork Belly
- 28gr Quinnoa
With this portion I will consume enough calories, protein, fat, fiber and sugar everyday. Moreover, it will only cost me $9.01.

Of course, there are always some food you prefer more or you wanna come up with a solution with exactly some type of foods. Thus, changing parameter and their contraints will help you to customize your solution. 

## CONCLUSION:
AMPL is useful app. Even to solve a problem that seems like easy but I do know that it will save you a lot of time and give you the best choice!

