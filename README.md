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
'nutrition': gives nutritional content of the recipe in the form of a list [calories, total fat, sugar, sodium, protein, saturated fat, carbs] [NOTE]for this particular analysis, we will be looking at the total fat content of each recipe!
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
This is a the average_rating column graphed in with the values frequency. Some of the trends show slightpositive increase until the average rating reaches four until it declines until it reaches five for an extreme spike. There is a huge spike at five votes, as it has the maximum frequency count. 

### Bivariate Analysis
<iframe src="assets/bivariate.html" width=800 height=600 frameBorder=0></iframe>
This visualization is a scatterplot with average rating on the x axis and total fat on the y axis. As pictured, we can see that as the ratings increase (reach the 4-5 range) there tends to be higher concentration of lower total fat values. However, there are a couple of 5 star rating recipes that have total fat values over 1000 and some in the 3000 range area. 

### Pivot Tables, Aggregate Statistics
|   average_rating |   total_fat |
|-----------------:|------------:|
|             1    |    36.5782  |
|             1.33 |   164       |
|             1.5  |    36.4444  |
|             1.67 |     2       |
|             1.75 |    14       |
|             1.8  |     0       |
|             2    |    36.9148  |
|             2.13 |     2       |
|             2.17 |    34       |
|             2.25 |     8.15385 |
|             2.29 |    23       |
|             2.33 |    16.5849  |
|             2.4  |    31.2414  |
|             2.5  |    33.5204  |
|             2.56 |     1       |
|             2.6  |    14.2692  |
|             2.67 |    30.1789  |
|             2.75 |    38.5263  |
|             2.8  |     5       |
|             2.83 |    21       |
|             2.86 |     0       |
|             2.88 |    36       |
|             3    |    33.3804  |
|             3.07 |    46       |
|             3.09 |   110       |
|             3.12 |    36       |
|             3.14 |    52       |
|             3.17 |    45.069   |
|             3.19 |    10       |
|             3.2  |    29.4444  |
|             3.25 |    43.9298  |
|             3.29 |    35.6889  |
|             3.3  |    32       |
|             3.31 |    29       |
|             3.33 |    33.8142  |
|             3.36 |    70       |
|             3.38 |    74       |
|             3.4  |    29.7059  |
|             3.41 |    11       |
|             3.43 |    25.2308  |
|             3.44 |     5.33333 |
|             3.45 |     0       |
|             3.5  |    30.2702  |
|             3.56 |    24.8947  |
|             3.57 |    48.0789  |
|             3.59 |    79       |
|             3.6  |    31.1301  |
|             3.62 |     4.2963  |
|             3.65 |    82       |
|             3.67 |    31.8162  |
|             3.69 |    47       |
|             3.7  |    91.3043  |
|             3.71 |    59.3311  |
|             3.75 |    42.6214  |
|             3.77 |     4       |
|             3.78 |    29.5     |
|             3.79 |    25.8679  |
|             3.8  |    38.5217  |
|             3.81 |    13       |
|             3.82 |    19.1633  |
|             3.83 |    38.7795  |
|             3.85 |     9.14815 |
|             3.86 |    40.7895  |
|             3.88 |    19.2299  |
|             3.89 |    43.5526  |
|             3.9  |    10.7576  |
|             3.91 |    36       |
|             3.92 |    13.6     |
|             3.93 |    46.4375  |
|             3.94 |    50.1538  |
|             3.95 |    10       |
|             3.96 |    30.0722  |
|             4    |    31.912   |
|             4.07 |    14.5     |
|             4.08 |    75.5684  |
|             4.09 |    15.8219  |
|             4.1  |    84.1202  |
|             4.11 |    37.2606  |
|             4.12 |    31.8345  |
|             4.13 |    19.7966  |
|             4.14 |    33.7302  |
|             4.15 |    56.0737  |
|             4.16 |    27.15    |
|             4.17 |    30.3371  |
|             4.18 |    24.0588  |
|             4.19 |    11.8043  |
|             4.2  |    29.2138  |
|             4.21 |    22.6316  |
|             4.22 |    25.9556  |
|             4.23 |    44.8966  |
|             4.24 |    33.8091  |
|             4.25 |    26.1414  |
|             4.26 |    13       |
|             4.27 |    20.2368  |
|             4.28 |    33.0213  |
|             4.29 |    34.0938  |
|             4.3  |    49.625   |
|             4.31 |    18.0042  |
|             4.32 |    48.6591  |
|             4.33 |    30.978   |
|             4.34 |    73       |
|             4.35 |    71.0104  |
|             4.36 |    16.9253  |
|             4.37 |    12       |
|             4.38 |    27.3383  |
|             4.39 |    46.6327  |
|             4.4  |    32.9483  |
|             4.41 |    39.8722  |
|             4.42 |    25.1064  |
|             4.43 |    30.5524  |
|             4.44 |    25.6841  |
|             4.45 |    37.6734  |
|             4.46 |    37.9721  |
|             4.47 |    14.6807  |
|             4.48 |    23.5859  |
|             4.49 |     9       |
|             4.5  |    31.5093  |
|             4.51 |    87.5273  |
|             4.52 |     9.85366 |
|             4.53 |    23.7396  |
|             4.54 |    42.2597  |
|             4.55 |    32.2209  |
|             4.56 |    27.3495  |
|             4.57 |    28.3673  |
|             4.58 |    33.5019  |
|             4.59 |    32.3569  |
|             4.6  |    29.481   |
|             4.61 |    67.4533  |
|             4.62 |    27.5318  |
|             4.63 |    28.0323  |
|             4.64 |    23.9682  |
|             4.65 |    37.25    |
|             4.66 |    59.5294  |
|             4.67 |    29.0182  |
|             4.68 |    95.5686  |
|             4.69 |    28.4411  |
|             4.7  |    25.8204  |
|             4.71 |    28.3673  |
|             4.72 |    45.2847  |
|             4.73 |    32.4517  |
|             4.74 |    26.0345  |
|             4.75 |    28.9292  |
|             4.76 |    34.4452  |
|             4.77 |    35.19    |
|             4.78 |    24.8144  |
|             4.79 |    21.7986  |
|             4.8  |    25.658   |
|             4.81 |    24.7175  |
|             4.82 |    27.0722  |
|             4.83 |    31.0741  |
|             4.84 |    26       |
|             4.85 |    32.3133  |
|             4.86 |    32.947   |
|             4.87 |    29.0155  |
|             4.88 |    29.0764  |
|             4.89 |    30.7182  |
|             4.9  |    30.2409  |
|             4.91 |    30.4199  |
|             4.92 |    28.0685  |
|             4.93 |    29.3555  |
|             4.94 |    31.0105  |
|             4.95 |    42.3574  |
|             4.96 |    21.0836  |
|             4.97 |    38.2205  |
|             4.98 |    40.9143  |
|             4.99 |    83       |
|             5    |    32.7525  |
