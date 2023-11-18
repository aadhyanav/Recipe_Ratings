# DSC80 Project 3 - Recipes & Ratings

by Aadhya Naveen (anaveen@ucsd.edu)
---

## Introduction

### Question: Do recipes with higher average ratings tend to have lower levels of total fat?

Welcome! The dataset I have chosen illustrates recipes and various information like steps, categories, and ratings of each recipe. The data is pulled from a website called food.com, and as humans we know the importance of food in our day-to-day lives therefore, this analysis will provide insight on these recipes :)

The data is broken down into 2 csv files: RAW_recipes.csv and RAW_interactions.csv. I merged both of the dataset with the common column 'id' which refers to the unique recipe id. Once I merged the datasets, the number of rows in the dataset were 234,429.

As for my research question - I was curious on whether the ratings had any relationship with the total fat content of each recipe. Therefore my question is ** Do recipes with higher average ratings tend to have lower levels of total fat? **

Here's a breakdown on some of the important columns in the dataset.
'name': name of the recipe

'id': unique id of recipe

'nutrition': gives nutritional content of the recipe in the form of a list [calories, total fat, sugar, sodium, protein, saturated fat, carbs] [NOTE] for this particular analysis, we will be looking at the total fat content of each recipe!

'ratings': ratings for each recipe

---

## Cleaning and Exploratory Data Analysis

### Data Cleaning

(1) The data is broken down into 2 csv files: RAW_recipes.csv and RAW_interactions.csv. I merged both of the dataset with the common column 'id' which refers to the unique recipe id. Once I merged the datasets, the number of rows in the dataset were 234,429.

(2) Replaced all zeros with np.nan - This indicates that the values are actually missing instead of of low amount. For example, when we replace the 0 for np.nan in the ratings columns, it indicates that the value is actually missing instead of the recipe getting a low rating.

(3) Created a series called 'avg_rating' based of the ratings columns - which instead took the average rating of each recipe since there were duplicates in the dataset. Then did a merge to add this column to the dataset.

(4) Dropped columns like 'user_id', 'recipe_id', 'date', 'contributor_id', 'review' and 'submitted', 'steps', and 'tags' because I did not need them in the analysis that I was doing and they were taking up too much space. 

(5) In the nutrition column - it appears that each entry is a list when it is actually a string! Therefore, using the eval function I looped through each of the enteries and turned them into lists. Then, since the second element of the list refers to the total_fat, created a new column 'total_fat' which only has the fat portion of the nutrition list.

(6) Just to keep numbers clean and to make them easier to work with, I rounded the floats in 'total_fat' and 'average_rating' to 2 decimal places. This is so that runtime is faster and it would be easier to work with. 

| name                                |     id |   minutes | tags                                                                                                                                                                                                                        | nutrition                                    |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |   rating |   average_rating |   total_fat |
|:-------------------------------------|-------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|-----------------:|------------:|
| 1 brownies in the world    best ever | 333281 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |        4 |                4 |          10 |
| 1 in canada chocolate chip cookies   | 453467 |        45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |        5 |                5 |          46 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |

### Univariate Analysis
<iframe src="assets/average_rating.html" width=800 height=600 frameBorder=0></iframe>
This is a the average_rating column graphed in with the values frequency. Some of the trends show a slight positive increase until the average rating reaches four until it declines until it reaches five for an extreme spike. There is a huge spike at five votes, as it has the maximum frequency count. 

### Bivariate Analysis
<iframe src="assets/bivariate.html" width=800 height=600 frameBorder=0></iframe>
This visualization is a scatterplot with average rating on the x-axis and total fat on the y-axis. As pictured, we can see that as the ratings increase (reach the 4-5 range) there tends to be higher concentration of lower total fat values. However, there are a couple of 5 star rating recipes that have total fat values over 1000 and some in the 3000 range area. 

### Pivot Tables, Aggregate Statistics

|   rating |   total_fat |
|---------:|------------:|
|        1 |     37.0564 |
|        2 |     32.7669 |
|        3 |     31.6405 |
|        4 |     29.9404 |
|        5 |     31.7924 |

This is a pivot tabel that shows the mean total_fat for each rating in general. I used this because it is easier to look at since the cateogories for ratings are broader versus average_rating which has sperates the rating by .1 which is hard to find trends with. As we can see in the pivot table, there seems to be a slight decrease in fat as ratings increase. The mean total fat is about 37 for when the rating is 1 star, versus the total fat being about 32 when the rating is 5. But considering the distribution of ratings, it could be that since there are less observations with lower ratings the means tend to be higher. 

|   rating |   total_fat |
|---------:|------------:|
|        1 |          19 |
|        2 |          20 |
|        3 |          20 |
|        4 |          19 |
|        5 |          20 |

This pivot table focuses on the identical columns but examines the median instead of the mean. Considering that the mean can be significantly impacted by outliers and distribution patterns, analyzing the median offers an alternative viewpoint on the distribution of the "total_fat" column concerning ratings.

## Assesment of Missingness

### NMAR analysis
I think that the description column of the dataset is NMAR. 

### Missingness Dependency

Test #1
Null Hypothesis (H0): The distribution of "n_steps" when the description is missing is identical to the distribution of "n_steps" when the description is not missing.

Alternative Hypothesis (Alt Hyp): The distributions of "n_steps" are different between cases where the description is missing and cases where it is not.

Observed Statistic: The difference in means between the two groups.

Rationale: If there is a higher number of steps, it suggests that the description is more likely to be left blank. This is because detailed steps may make the inclusion of a description less necessary, leading to a potential difference in the distribution of "n_steps" between cases where the description is present and cases where it is missing.
<iframe src="assets/steps.html" width=800 height=600 frameBorder=0></iframe>

## Hypothesis Testing
H0: Average Ratings and total fat have no relationship, ratings are evenly distributed among different levels of fat 

H1: Recipes with average higher ratings tend to have lower levels of fat

Differences in means - Test Statistic 

Significance level - 0.05

Observed Pvalue: 3.22

Pvalue: 0.0

Reject null hypothesis that the two groups come from the same distriibution, but cannot conclude that high rating causes lower fat

