---
layout: post
title:      "Northwind Database Analysis"
date:       2019-11-13 13:56:24 +0000
permalink:  northwind_database_analysis
---

For the Module 2 Final Project, we are tasked with using the Northwind database to demonstrate what we have learned about SQL and statistical analysis.  The famous Northwind database, which we first saw in an earlier Mod 2 lesson, is a free open-source dataframe created by Microsoft, which contains data from Northwind Traders, a fictitious food import/export company.   We are given schema of table information.

This Entity Relationship Diagram (ERD) shows us all of the tables contained in the database, the columns in each table containing the actual data, and the primary and foreign keys which inform us of the relationships between tables.  The ERD is an invaluable tool to the data scientist and it has been stressed to us many times to make a friend out of the database administrator in real world situations.  Access to a  properly maintained ERD (or at least some semblance of such) will save headaches and, most importantly, time when it comes to extracting useful data from the database.  

Simple first steps when dealing with the relational database are to print out a list of tables, and perhaps a quick little for loop to identify the columns inside each table.  From there comes the fun part:  SQL queries of the database using joins to extract useful columns of data from different tables to combine all together in a pandas dataframe to use for analysis and testing.  Even with our small toy database with just 13 tables, the possibilities are vast of ways to combine data from different tables into unique dataframes we can use to pose and answer interesting questions.  

Asking and answering relevant business questions is the high level goal of any data science project, it seems, and the very specific assignment for this project.  Flatiron was so kind as to provide us the first one, asking “Do discounts have a statistically significant effect on the number of products customers order? If so, at what level(s) of discount?”  From there, we choose 3 more of our own with the simple guideline that they be important information for the company.  Getting a good feel for the database, by exploring the ERD and performing SQL queries to combine data from different tables, helps guide the formation of these questions.

Once we have our important business questions, the job is to design experiments to answer them using statistical analysis and hypothesis testing.  The data needs to be explored and assumptions validated in order to determine which statistical test to use.  For our first question about discounts and products ordered, the data is split up into discounted and non-discounted orders. It is then plotted using sns.distplot to show a histogram of the data along with the estimated probability density function (PDF) , as well as the mean of the two samples which we will be comparing in our hypothesis testing.

Normality of samples is an assumption we need to check for several of the standard hypothesis tests we can employ, including the independent two-sample t-test we used to compare these samples.  An eyeball test of these distributions clearly shows they are not normally distributed, however, with big enough sample sizes, and these easily qualify at around 800 and 1300 we can relax that assumption.   I believe we have the power (magic?!) of the Central Limit Theorem to thank for this, and that may be a blog post for another time.  Next step is to check for equal variance, between the 2 samples before choosing our test. 
```
#Levene Test for equal variance
stats.levene(X, Y)
LeveneResult(statistic=14.832671704073421, pvalue=0.00012091378376079568)

```
The tiny p-value less than the test statistic allows us to reject the test’s null hypothesis of equal variance and choose a one-sided Welch’s t-test to compare our sample means.   We then test the following hypotheses:

𝐻0: 𝜇1=𝜇2  -- The average quantity of products per order is equal with or without discounts

𝐻𝐴: 𝜇1>𝜇2  -- The average quantity of products per order increases with a discount.

The null hypotheses for these tests always contain a measure of equality whether it is =, >=, or <=.  That there is no significant difference between the comparison groups.  The alternate hypothesis is set up to prove that there is a statistically significant difference and can state that the groups are not equal or that one is greater than or less than the other.  When coming up with these business questions, we seek to formulate the null and alternative hypotheses to shed an interesting light on some facet of the business using statistical significance.

Back to our example, we run the Welch’s t-test with the following code: ```t, p = stats.ttest_ind(X,Y, equal_var=False).```   The resulting p-value is compared to our alpha value of 0.05 (divided by 2 in this case for our one-sided test).  The p-value of  5.65641429030433e-10 is less than the alpha value and we reject the null hypothesis that the two means are equal.  Importantly, this does not prove our alternate hypothesis but it gives us the confidence to say there is almost no chance (the p-value expressed as a percentage) that the sales are equal with or without a discount.  We would feel comfortable telling the stakeholder that discounts do increase sales and recommend their continued usage, pursuant to further study on level of discount, effect on revenue (as opposed to just order numbers, etc).

There are several other statistical tests that we learned and can apply to carry out hypothesis testing:  one-sample t-test, ANOVA, Tukey ... but what is important is the process remains the same.  We split our populations into samples to be compared, for null and alternative hypotheses, explore the data with visualizations and summary statistics, and wisely choose which test to use.  After running the test, we interpret the results and make business recommendations.

All of the questions we seek to answer and hypothesis tests that we run to find those answers can help us gain valuable insights into just about any aspect of a business that we want to study.  And the job is never ending, except as time permits.  Each answer to a question can open the door to many more questions and hypotheses to form and test. This project allowed us to start with just the name of a company and a simple ERD and go on to appreciate the way statistical analysis and hypothesis testing, aided by SQL querying to extract relevant data, can lead us to a wealth of business insights.  
