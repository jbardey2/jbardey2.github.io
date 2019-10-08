---
layout: post
title:      "King County Housing Analysis"
date:       2019-10-08 11:05:58 +0000
permalink:  king_county_housing_analysis
---


For the Module 1 Project in the Flairon Data Science bootcamp we were given a dataset of 21 attributes of houses in King County, WA. The target variable was sales price, and 20 other columns had various other attributes or statistics about the homes.  Our job was to take this data and use it to make a Linear Regression model to accurately predict the sale price for houses in Kings County.  We have seen similar data earlier in this course and been taught methods to handle it, but for the first time, with this project we were given free reign to play with the data and really examine it on our own.  To this end, we employed the OSEMN process of Data Science: Obtain Data, Scrub it, Exploratory Data Analysis, Model the Data and finally iNnterpret your findings.  

In this case, the Obtain step of the project was straightfoward and simple.  We were given a dataset in the github repo for the project and simply used the command
`df = pd.read_csv('kc_house_data.csv')` .  A quick call of  `df.head()` to preview the first 5 rows of the data set and we are off to the races!   In the real world, and likely later on in this course, whether or not we are using the OSEMN framework, the step of Obtaining data for our projects will be more of a challenge; whether we need to query databases for relevant data or perform web scraping, or perhaps other methods I do not yet know. 

To be completed...



