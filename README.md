
# Recipe Analysis

Analysis of recipes for EECS398 at the University of Michigan

**by** Vijay Ravi \| **email:** <a href="mailto:vijjr@umich.edu">vijjr@umich.edu</a>

# Introduction

The goal in this project was to analyze the recipes and associated ratings as found on foods.com since 2008. Included is 83,782 recipes, and an additional 731,927 independently sourced ratings, which totals to 234,429 matching recipe/ rating observations

The goal of this analysis is to predict information about the nutrition for each recipe, primarily information about the calorie and protein breakdown. Hopefully as a result, a trend will become apparent, making it possible to predict the caloric value of a recipe given some indicators. 

Together these datasets include information about recipe nutrition, time to prepare, the number of steps, ratings for each recipe, and more. A detailed breakdown is provided below. Note that some irrelevant features were dropped. 
<br><br>

| Column | Description |
| ----------- | ----------- |
| `id` | A unique ID for each recipe / rating |
| `minutes` | The time to complete each recipe |
| `tags` | A list of tags associated with a recipe |
| `nutrition` | The nutrition information (i.e. calories, protein, fats, etc) |
| `n_steps` | The number of steps in a recipe |
| `rating` | The rating provided |

# Data Cleaning and Exploratory Data Analysis



## Cleaning the Data

| name                               |   minutes |   contributor_id | submitted   | tags               | nutrition                                 |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | ingredients                                                                            |   n_ingredients |   user_id |   recipe_id | date       |   avg_rating |   protein_ratio |   calories |   protein |
|:-----------------------------------|----------:|-----------------:|:------------|:-------------------|:------------------------------------------|----------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------|----------------:|----------:|------------:|:-----------|-------------:|----------------:|-----------:|----------:|
| impossible macaroni and cheese pie |        50 |           531768 | 2008-01-01  | 60-minutes-or-less | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0] |        11 | ['heat oven to 400 degrees fahrenheit', 'grease a pie plate 10 x 1 1 / 2 inches', 'mix 2 cups cheese and the macaroni', 'sprinkle mixture in the plate', 'beat remaining ingredients , except the 1 / 4 cup cheese , until smooth , 15 seconds in a blender on high , or 1 minute with a hand beater', 'pour into plate', 'bake until knife inserted in center comes out clean - about 40 minutes', 'sprinkle with 1 / 4 cup cheese', 'bake until cheese is melted , 1 to 2 minutes', 'cool 10 minutes', 'serves 6 to 8 people'] | ['cheddar cheese', 'macaroni', 'milk', 'eggs', 'bisquick', 'salt', 'red pepper sauce'] |               7 |    240552 |      275022 | 2008-04-07 |            3 |          10.619 |      386.1 |        41 |
| impossible macaroni and cheese pie |        50 |           531768 | 2008-01-01  | time-to-make       | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0] |        11 | ['heat oven to 400 degrees fahrenheit', 'grease a pie plate 10 x 1 1 / 2 inches', 'mix 2 cups cheese and the macaroni', 'sprinkle mixture in the plate', 'beat remaining ingredients , except the 1 / 4 cup cheese , until smooth , 15 seconds in a blender on high , or 1 minute with a hand beater', 'pour into plate', 'bake until knife inserted in center comes out clean - about 40 minutes', 'sprinkle with 1 / 4 cup cheese', 'bake until cheese is melted , 1 to 2 minutes', 'cool 10 minutes', 'serves 6 to 8 people'] | ['cheddar cheese', 'macaroni', 'milk', 'eggs', 'bisquick', 'salt', 'red pepper sauce'] |               7 |    240552 |      275022 | 2008-04-07 |            3 |          10.619 |      386.1 |        41 |
| impossible macaroni and cheese pie |        50 |           531768 | 2008-01-01  | course             | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0] |        11 | ['heat oven to 400 degrees fahrenheit', 'grease a pie plate 10 x 1 1 / 2 inches', 'mix 2 cups cheese and the macaroni', 'sprinkle mixture in the plate', 'beat remaining ingredients , except the 1 / 4 cup cheese , until smooth , 15 seconds in a blender on high , or 1 minute with a hand beater', 'pour into plate', 'bake until knife inserted in center comes out clean - about 40 minutes', 'sprinkle with 1 / 4 cup cheese', 'bake until cheese is melted , 1 to 2 minutes', 'cool 10 minutes', 'serves 6 to 8 people'] | ['cheddar cheese', 'macaroni', 'milk', 'eggs', 'bisquick', 'salt', 'red pepper sauce'] |               7 |    240552 |      275022 | 2008-04-07 |            3 |          10.619 |      386.1 |        41 |
| impossible macaroni and cheese pie |        50 |           531768 | 2008-01-01  | main-ingredient    | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0] |        11 | ['heat oven to 400 degrees fahrenheit', 'grease a pie plate 10 x 1 1 / 2 inches', 'mix 2 cups cheese and the macaroni', 'sprinkle mixture in the plate', 'beat remaining ingredients , except the 1 / 4 cup cheese , until smooth , 15 seconds in a blender on high , or 1 minute with a hand beater', 'pour into plate', 'bake until knife inserted in center comes out clean - about 40 minutes', 'sprinkle with 1 / 4 cup cheese', 'bake until cheese is melted , 1 to 2 minutes', 'cool 10 minutes', 'serves 6 to 8 people'] | ['cheddar cheese', 'macaroni', 'milk', 'eggs', 'bisquick', 'salt', 'red pepper sauce'] |               7 |    240552 |      275022 | 2008-04-07 |            3 |          10.619 |      386.1 |        41 |
| impossible macaroni and cheese pie |        50 |           531768 | 2008-01-01  | preparation        | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0] |        11 | ['heat oven to 400 degrees fahrenheit', 'grease a pie plate 10 x 1 1 / 2 inches', 'mix 2 cups cheese and the macaroni', 'sprinkle mixture in the plate', 'beat remaining ingredients , except the 1 / 4 cup cheese , until smooth , 15 seconds in a blender on high , or 1 minute with a hand beater', 'pour into plate', 'bake until knife inserted in center comes out clean - about 40 minutes', 'sprinkle with 1 / 4 cup cheese', 'bake until cheese is melted , 1 to 2 minutes', 'cool 10 minutes', 'serves 6 to 8 people'] | ['cheddar cheese', 'macaroni', 'milk', 'eggs', 'bisquick', 'salt', 'red pepper sauce'] |               7 |    240552 |      275022 | 2008-04-07 |            3 |          10.619 |      386.1 |        41 |

