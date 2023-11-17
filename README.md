# DSC80 Project 3 - Recipes 

by Aadhya Naveen (anaveen@ucsd.edu)
---

## Introduction

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

# Data Cleaning
(1) Replaced all zeros with np.nan - This indicates that the values are actually missing instead of of low amount. For example, when we replace the 0 for np.nan in the ratings columns, it indicates that the value is actually missing instead of the recipe getting a low rating.
(2) Created a series called 'avg_rating' based of the ratings columns - which instead took the average rating of each recipe since there were duplicates in the dataset. Then did a merge to add this column to the dataset.
(3) Dropped columns like 'user_id', 'recipe_id', 'date', 'contributor_id', 'review' and 'submitted' because I did not need them in the analysis that I was doing. 



