# Movie_Analysis







## Overview
Microsoft is looking to enter the film industry. This analysis is conducted to help the company choose an informed entry position. It analyses datasets containing film information to generate insights and recommendations. 

Data-backed answers to the proposed business questions suggest that Microsoft invests generously in Adventure, Action, Comedy and Drama genres.



## Business Problem
As a business, the main intention to join the film industry is the industry's potential for profit. Therefore, the business problem is to consider all available factors and make a decision that optimizes returns. 

This analysis proposes 3 business questions to help with the goal:
1. What are the most Popular Genres? 
2. Which Genres have the highest monetary returns?
3. Does a higher production budget translate to higher returns?

The selection of these questions is based on the type of data available and the intention mentioned above. 


## Exploratory Data Analysis
The data used in the analysis was sourced from [IMDB Developer](https://developer.imdb.com/non-commercial-datasets/) non commercial datasets collection. I used the following datasets:

 ```
title.basics.csv
title.ratings.csv
bom.movie_gross.csv
tn.movie_budgets.csv
```
They can all be accessed from the /data folder.


After loading into dataframes, The first section in the goes through the dataframes to inspect their shapes, column names, what each row represents and viewing sample rows from the head or tail of each. It ends with combining the `basics_df` and `ratings.df` into `combined_df` as the infomation they contain is highly related for the purposes of our analysis.

## Methods

### Data Preparation
This section presents the process of cleaning the data, alongside the reasoning for decisions in each step.


I find no duplicate rows and continue to create a function `null_percentages(data_frame)` that prints out the number of null values in a dataframe and their percentage 

To understand the distribution of data in the dataframe, I print out its measures of central tendency and dispersion using `describe()`. I also plot the histogram below and find the runtime_minutes column to be heavily skewed.

I chose to fill in the missing values with the median because it was least likely to be affected by outliers. Dropping the rows was not an option as I would lose over 10% of the data


### the most Popular Genres? 
From the business understanding, Microsoft would need to know which genres are doing best.\
*Assumption - the viewership of a movie is directly related to its weighted rating, as more reviewed genres are more likely to have been viewed and reviewed more.*

To answer this question, I needed to consider **weighted ratings** based on the average ratings and number of votes. I had chosen to use the Wilson score to determine the confidence level that a rating had based on the number but couldn't figure out how to make it work on time so I pivoted.

Instead, I found the top 5 genres by average rating and the top 5 by the number of votes (*see assumption above*), added both to a list and chose the top genres by how frequently they appeared in that list. I believe the logic holds.

## Question 2:Which Genres have the highest monetary returns?
As a business, Microsoft should also consider the performance in revenue of the genres.

By knowing the genres that perform best, the company would be hoping to replicate the success by joining the bandwagon.

To answer this question, I merged `movie_gross_df` and `basic_df` on columns 'title' and 'primary_title' respectively. After dropping unneeded columns, handling duplicates and dropping null values, I found the top 5 genres by gross by domestic gross and added the genres to a list.

Again, I used how often a genre appears in the list to judge the performance of the genres. 

### Question 3: Does a higher production budget translate to higher returns?

To gain a sense of how much to spend on the chosen Genre given their expected returns, Microsoft may want to understand the relationship between two.

I used `roi_df`that contained budgets and gross returns per film among other details  to answer this question. After basic preparation, a few type conversions and currency formatting, I shrunk the DataFrame to contain only the columns `production_budget` and `worldwide_gross`. Finally I plotted a beautiful pairplot to represent my asnwer to the question. 

## Results
**the most popular genres?**\
Comedy, Drama, Adventure and Action were the most popular genres in that order.

![Chart](images/question_1.jpg)

**genres have the highest monetary returns?**\
From the analysis, Microsoft should consider creating films in Adventure, Action, Comedy and Drama.

![Chart2](images/question_2.jpg)

**Does a higher production budget translate to higher returns?**

There is a moderate to strong positive correalation `(+0.74)` between a film's production budget and its returns. A positve return on investment is just what an investor would be looking for.

![Chart3](images/question_3.png)


## Conclusion

This project was completed successfully and answers to questions provided. My recommendations to the stakeholder are to invest in the genres identified above and consider allocating a healthy budget for the project for reasons this project has provided. 

I would recommend thet they take other factors beyond the scope of this project into consideration such as external and internal business environments.

## Repository Structure



```
├── README.md              <- The top-level README for reviewers of this project
├── index.ipynb            <- Narrative documentation of analysis in Jupyter notebook
├── Presentation.pdf       <- PDF version of project presentation
├── zippedData             <- All sourced externally
└── images                 <- Both sourced externally and generated from code
```
