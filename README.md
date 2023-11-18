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
|   total_fat |
|------------:|
|    36.5782  |
|   164       |
|    36.4444  |
|     2       |
|    14       |
|     0       |
|    36.9148  |
|     2       |
|    34       |
|     8.15385 |
|    23       |
|    16.5849  |
|    31.2414  |
|    33.5204  |
|     1       |
|    14.2692  |
|    30.1789  |
|    38.5263  |
|     5       |
|    21       |
|     0       |
|    36       |
|    33.3804  |
|    46       |
|   110       |
|    36       |
|    52       |
|    45.069   |
|    10       |
|    29.4444  |
|    43.9298  |
|    35.6889  |
|    32       |
|    29       |
|    33.8142  |
|    70       |
|    74       |
|    29.7059  |
|    11       |
|    25.2308  |
|     5.33333 |
|     0       |
|    30.2702  |
|    24.8947  |
|    48.0789  |
|    79       |
|    31.1301  |
|     4.2963  |
|    82       |
|    31.8162  |
|    47       |
|    91.3043  |
|    59.3311  |
|    42.6214  |
|     4       |
|    29.5     |
|    25.8679  |
|    38.5217  |
|    13       |
|    19.1633  |
|    38.7795  |
|     9.14815 |
|    40.7895  |
|    19.2299  |
|    43.5526  |
|    10.7576  |
|    36       |
|    13.6     |
|    46.4375  |
|    50.1538  |
|    10       |
|    30.0722  |
|    31.912   |
|    14.5     |
|    75.5684  |
|    15.8219  |
|    84.1202  |
|    37.2606  |
|    31.8345  |
|    19.7966  |
|    33.7302  |
|    56.0737  |
|    27.15    |
|    30.3371  |
|    24.0588  |
|    11.8043  |
|    29.2138  |
|    22.6316  |
|    25.9556  |
|    44.8966  |
|    33.8091  |
|    26.1414  |
|    13       |
|    20.2368  |
|    33.0213  |
|    34.0938  |
|    49.625   |
|    18.0042  |
|    48.6591  |
|    30.978   |
|    73       |
|    71.0104  |
|    16.9253  |
|    12       |
|    27.3383  |
|    46.6327  |
|    32.9483  |
|    39.8722  |
|    25.1064  |
|    30.5524  |
|    25.6841  |
|    37.6734  |
|    37.9721  |
|    14.6807  |
|    23.5859  |
|     9       |
|    31.5093  |
|    87.5273  |
|     9.85366 |
|    23.7396  |
|    42.2597  |
|    32.2209  |
|    27.3495  |
|    28.3673  |
|    33.5019  |
|    32.3569  |
|    29.481   |
|    67.4533  |
|    27.5318  |
|    28.0323  |
|    23.9682  |
|    37.25    |
|    59.5294  |
|    29.0182  |
|    95.5686  |
|    28.4411  |
|    25.8204  |
|    28.3673  |
|    45.2847  |
|    32.4517  |
|    26.0345  |
|    28.9292  |
|    34.4452  |
|    35.19    |
|    24.8144  |
|    21.7986  |
|    25.658   |
|    24.7175  |
|    27.0722  |
|    31.0741  |
|    26       |
|    32.3133  |
|    32.947   |
|    29.0155  |
|    29.0764  |
|    30.7182  |
|    30.2409  |
|    30.4199  |
|    28.0685  |
|    29.3555  |
|    31.0105  |
|    42.3574  |
|    21.0836  |
|    38.2205  |
|    40.9143  |
|    83       |
|    32.7525  |
pivot_table_avg_rati
