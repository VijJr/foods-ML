
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

In the process of analysis, some cleaning had to be done before generating visualizations

## Cleaning the Data

1. The first steps in cleaning was to merge all of the provided `rating` with the corresponding recipes over the `id`. After this step, there were many ratings of value 0, which is impossible in the standard rating system, thus ratings of 0 were replaced with `NaN`.

2. Once the `rating` feature was usable, the average rating was calculated by finding the mean rating for each individual recipe. This average rating is used as a representative for each recipe

3. A minor issue within the data is that the tags were formatted as a string, so the next cleaning job was to splice the string into a python list for easier analysis down the line. This is then exploded into individual recipes with one tag each, creating many more observations. The explosion is done for the purposes of modeling tag distributions.

4. The final step was to drop irrelevant features, and those features were `id`, `rating`, `review`, `description`, `steps`

The following is a representation of the cleaned dataset:

|   recipe_id |   minutes | tags               |   avg_rating |   calories |   protein |   n_steps |
|------------:|----------:|:-------------------|-------------:|-----------:|----------:|----------:|
|      275022 |        50 | 60-minutes-or-less |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | time-to-make       |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | course             |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | main-ingredient    |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | preparation        |            3 |      386.1 |        41 |        11 |

## Univariate Analysis

<iframe
  src="assets/top-10-tags.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>