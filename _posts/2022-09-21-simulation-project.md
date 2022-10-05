---
title: STOCHASTIC SIMULATION MODEL DEVELOPMENT FOR COVID-19 HOSPITALIZATION
date: 2022-05-20
layout: post
author: [Trang Duong]
categories: [Simulation]
tags: [hospital, queing system]
topics: data analytics
summary: "In this paper, the group developed a stochastic simulation model for Healthcare System management during the COVID-19 pandemic. The model focuses on the Emergency Department (ED) from the diagnosis of patient arrivals with COVID-19 to the death or discharge of the patient from the hospital. It also considers the fact that once admitted and initial tests are conducted, patients who are assigned to a bed in the Intensive Care Unit (ICU) or a Regular Impatient Bed will often switch between the 2 as their condition improves or worsens. The patients who have the most serious cases of COVID-19 will be placed in ICU beds which are the bottleneck to hospitals effectively saving COID-19 patients due to their low resource capacity. As a result, the model focuses heavily on utilizing ICU beds most effectively. This model was developed with the purpose of aiding Hospitals in minimizing COVID deaths with the optimal allocation of resources with a focus on ICU beds. Our results showed that at least 90 ICU are needed to serve the same amount of arrival for COVID-19 patients without any wait time. Since the model can be applied to a variety of different hospital’s situation, it can be used by hospital manager’s find out their possible capacity and solutions to improve services."
---

- toc
{: toc } 

## INTRODUCTION:  
In the past 20 years, simulation has been an important tool for hospitals as decision support systems. Before COVID-19, simulation models created for hospitals served various purposes such as the optimization of staff scheduling, resource allocation, and the minimization of patient wait times. However, such models are not of use unless the data they are developed from is accurate and representative of real-time hospital processes. The recent growth in use of simulation in the hospital setting can therefore be at least partially due to the improvement in technology and analytics that allows for a high-volume of real-time discrete data for use. 

In this project, I developed a discrete-event simulation model of an emergency department dealing with COVID-19 treatment of patients. This simulation will be used to assess the system performance of the emergency department, predict future responses, and guide decision making at the management level. We will be considering various hospital resources including nurse and doctor staff, equipment (ventilators), and hospital beds (both regular and ICU). Using anonymous hospital data about COVID-19 patient admittance and through research about typical hospital ICU and regular bed capacities, we were able to accurately capture the treatment process of patients with COVID-19. This typically involves movement between both ICU and regular impatient beds before the patient exits the system through hospital discharge after recovery or through death.

## PROBLEM DESCRIPTION:

<img src="/assets/Simulation-photos/logical-thinking.png" alt="Logical simulation model thinking" width="653" height="145">

First, the patient arrives into the system. The patient will either be admitted to the hospital or rejected. Patient admission to the hospital is based on severity. Due to limited hospital resources, only the patients who are at the highest risk will be admitted. Admission is also dependent on if there is space in the Emergency Department (ED) and enough resources available for the patient. After Admission, patients are given a series of lab tests and initial treatments to determine the severity of the disease. During the triage process step, the patient’s tests and vital measurements are reviewed in order to decide whether the patient should be sent to the ICU or a regular impatient bed. The ICU is reserved for the most severe cases of COVID-19 in which patients require ventilators to help their breathing and constant monitoring by hospital staff. 

Once the patient is assigned a bed, they may not remain there for the entirety of their hospital stay. If their disease worsens, they may move from a regular impatient bed to an ICU bed. While if a patient in an ICU bed begins to improve, they may be moved to a regular impatient bed for the remainder of their stay. This is so the limited ICU beds and resources can be reserved for only the patients who really need it. Although in reality patients may move multiple times between an ICU bed and a regular impatient bed, for simplicity purposes in our model we will assume that patients will only move once between the two. For example, if a patient moves from an ICU bed to a regular impatient bed, our model assumes that they will remain in a regular impatient bed until they leave the system. 

A patient may leave the system through death or recovery and discharge. Death may occur in patients either in the ICU or in regular impatient beds. Recovery and discharge can similarly occur in patients located in either beds. 

## DATA DESCRIPTION:

### DESCRIPTION:
Two datasets are provided to support the project, including:
(1) “hospitalization.csv” including the hospital admission information and (2) “ICU.csv” including ICU admission information. Input model parameters were estimated using the given dataset.

The first step was to prepare the data for use in the model by performing some data cleaning. Each patient used the same PAT_ID but a different PAT_ENC_CSN_ID since they could re-enter the hospital for several times. Therefore, I assumed to consider a re-enter patient as a new one for every different visit. 

Secondly, In order to more effectively utilize the ICU data from the second dataset, the group merged this dataset with the hospitalization data. This way, it was easier to observe which patients were hospitalized in the ICU, and which remained in regular impatient beds. Since the dates in the ICU dataset only contain the day of patient arrival/departure and not the specific time, the group decided to ignore the time part of the date in the hospitalization data. For example, patient 15134993 was admitted on April 1 2020 at 16:41:00 (shown in the dataset as 01APR2020: 16:41:00). The group removed the time portion of this entry so the hospital admission time now shows only 01APR2020. 
 
### PROBABILITY CALCULATION:
To simplify the model, I assumed that only one transfer at most occurs for patients. This means that if a patient is transferred from a regular to ICU bed, they will stay in the ICU bed and not transfer back to a regular bed. With this information, several probabilities were calculated. 

<img src="/assets/Simulation-photos/probability-calculation.png" alt="Probability Calculation" width="628" height="274">

### PLOT OF PATIENT ARRIVALS:
In order to apply the Non-Stationary Poisson process into the simulation model, I first have to calculate different lambda for each periods (in here I divided into weeks) and then I ploted them to easily understand their distribution.

<img src="/assets/Simulation-photos/different-lambda.png" alt="Lambda Calculations" width="632" height="348">

## INPUT MODELING & PARAMETER ESTIMATION:
From the ICU data, the group was able to determine the exact patients who stayed in the ICU, these patients' arrival date into the ICU, and their departure date from the ICU. The group was able to calculate the duration of each patient’s ICU stay by calculating the difference between the departure and arrival dates. Each patient’s ICU stay duration was used to calculate the average number of days a patient spends in the ICU. 

However, the data provided included people that stay in an ICU bed upon arrival and also people who will transfer to an ICU bed from a regular bed. After sorting the data set by date-time, the group was able to determine the order of beds the patient stayed in (regular vs ICU) and what the next event would be for them based on the calculated probability. Therefore, we have two data sets for the ICU service time depending on the path the patient took between the ICU and regular beds. Following that logic, we have two distributions for ICU bed service time shown below using Arena.

### Arena service time for patients who stay in an ICU bed first (ICU queue)
Distribution: Lognormal 

Expression: 0.5 + LOGN(13.2, 30.4)

Square Error: 0.006599

### Arena service time for patients who move from a RB to ICU bed (transfer queue)

Distribution: Exponential   

Expression: 0.999 + EXPO(13.8)

Square Error: 0.005205

From the hospitalziation dataset, the group determined the number of days that a patient spends in the system by observing the hospital admission time and the end date. This was considered the amount of time that a patient stays in a regular hospital bed. Moreover, similar to the logic of the ICU bed above, we can also create two different distributions of service time depending on the order the patient stays in the ICU beds or regular beds. These distributions were found using Arena software. 

### Arena service time for patients stay in RB first (RB queue)
Distribution: Lognormal

Expression: 0.5 + LOGN(7.82, 8.32)

Square Error: 0.000663

### Arena service time for patients that move from an ICU bed to RB (transfer queue)

Distribution: Lognormal

Expression: 0.5 + LOGN(8.87, 13.3)

Square Error: 0.004928

***WHY different distributions are IMPORTANT?***
Because patient rates based on two real-data sets are changed all the time, which depend on different periods. Thus, different distributions will tell you a behind story about the pandemic situation and will make the model become much more realistic.
{: .message }

## SIMULATION IMPLEMENTATION METHOD:

### SIMULATION MODEL CODE:
The simulation code is run on Python. A brief overview of the steps conducted in the writing and implementation of the code is provided below: 

- Import code files which are used in the module. 

- Initiate the Random seed to ensure the same outcome every time.

- Define the patient waiting queues from SimClasses to record the patient’s waiting for the regular bed and ICU bed. 

- Define the queues to record the patients that are already being treated. 

- Initiate the DTStat from SimClasses for collecting the time of different processes in the system. 

Every detail of the code will be found in the Simulation Repository in my GitHub.

In this section, the main components of the simulation model code are further explained. This includes the patient arrival method (non-stationary method), the process for removing patients from the queues for both ICU and regular beds, and simulation loop.  

### SIMULATION MODEL VALIDATION:
### SIMULATION MODEL VERIFICATION:

<img src="/assets/Simulation-photos/queing-network.png" alt="Queing Network with p" width="620" height="208">

<img src="/assets/Simulation-photos/queing-network-calculation.png" alt="Lambda Calculations" width="635" height="274">

## OUTPUTS ANALYSIS:
Running the simulation model with the arrival rates previously calculated resulted in an average wait time of around 54 days for regular impatient beds and an average of about 48 days for ICU beds. Since this data is from the peak of the COVID-19 outbreak, it makes sense that the wait times would be so long as all hospitals were over capacity during this time period. In order to decrease the waiting time for both regular and ICU beds, the number of resources available (number of beds) will have to increase. To determine the optimal number of resources to decrease the wait times of both the ICU and regular beds to 1 hour or less, I have tested many resource levels over various simulation runs as shown in the sensitivity analysis. 
This simulation focuses on the usage condition and treatment time of the regular bed and ICU bed since the mean waiting time of beds shows the affordability of the healthcare system. Furthermore, simulation on the affordability of the health care system could indicate the reasons that may cause resource shortages in the future. From the statistics on the resource shortage found in the simulation result, improvement suggestions could be concluded.  This simulation doesn’t consider the number of deaths or the life of the patient after the treatment since there are various factors that may cause patient death or life after treatment from both regular bed and ICU bed. 

<img src="/assets/Simulation-photos/result-10reps.png" alt="Result of 10 replications" width="630" height="218">

### Input uncertainty qualification:
The Bootstrap method is applied in order to quantify the input model estimation uncertainty. Bootstrapping randomly samples the data with replacement to create a new bootstrap dataset. Then, the maximum likelihood calculation previously done in the parameter estimation was repeated on the new bootstrapped dataset.

### Sensitivity Analysis:
One more time, Bootstrap method is applied to compare to the non-bootstrap model. At the same time, changing the number of ICU bed and Regular bed affect directly on the result and make the difference between hospital's facility. 

## CONCLUSION:
I have developed a stochastic simulation model using real hospital data to support the model. Using this model, hospitals would be able to determine the optimal number of resources required to effectively serve all COVID-19 patients, therefore maximizing patient treatment and minimizing patient deaths. The main purpose of this model is focusing on simulating a model that yields a result close to the real data set. However, the group is also able to use this simulation to calculate different variables that the data set did not provide in the first place and to observe the effects of changes in variables on the system performance. Therefore, this simulation model can be altered to meet the specific needs of different systems. 

With future work, I hope to be able to expand the model to include more accurate measures of system performance using more advanced simulation techniques while also including additional resources and entity attributes such as hospital staff, ventilators and other hospital equipment, and patient severity levels. This will allow the model to be more flexible and useful to the end-users.


