
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

4. The final step is to drop irrelevant features, and those features were `id`, `rating`, `review`, `description`, `steps`

The following is a representation of the cleaned dataset:

|   recipe_id |   minutes | tags               |   avg_rating |   calories |   protein |   n_steps |
|------------:|----------:|:-------------------|-------------:|-----------:|----------:|----------:|
|      275022 |        50 | 60-minutes-or-less |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | time-to-make       |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | course             |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | main-ingredient    |            3 |      386.1 |        41 |        11 |
|      275022 |        50 | preparation        |            3 |      386.1 |        41 |        11 |

## Univariate Analysis

Before beginning the analysis, a plot was constructed to see the most common tags in the dataset. This information was important to factor in bias, and get a better understanding of the kind of tags that are most commonly seen.

<iframe
  src="assets/top-10-tags.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>

The next step was to see the average protein / calorie ratio across the data, and undestand where the skew lies. From below it is apparent that the data is right skew, indicating that many recipes have higher protein compared to the associated calories. The most common protein to calorie ratio was around 5, which can be used as comparison for our predictive model later.

<iframe
  src="assets/protein-ratio-dist.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>

## Bivariate Analysis

Now with the bivariate data, it was useful to see if the number of steps per recipe was correlated with the protein/ calorie ratio. As seen below, most recipes tend to have few steps, and vary widely. There also appears to be a very weak negative linear relationship, which could be of use later when building the model. 

<iframe
  src="assets/protein-ratio-steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Finally a bubble plot was created to visualize the linear relationship of protein / calorie ratio and the average rating for recipes, with an additional parameter of number of steps to tie everything together and see how they relate. It appears that majority of recipes are given high ratings, with higher protein to calorie ratio recipes getting higher ratings on average. Those with higher ratings and high ratios also appear to have comparatively less steps, which fits with our previous analysis. 

<iframe
  src="assets/bubble-plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Aggregations

Another useful metric is aggregations, and below is a pivot table showing the mean values of minutes and number of steps across the binned protein calorie ratio and rating. Key observations are that the highest rated recipes with the highest protein calorie ratio have short prep time, and there are no low rated recipes with very high protein content relative to the calories.  

|   ('minutes', 'Low') |   ('minutes', 'Medium') |   ('minutes', 'High') |   ('minutes', 'Very High') |   ('n_steps', 'Low') |   ('n_steps', 'Medium') |   ('n_steps', 'High') |   ('n_steps', 'Very High') |
|---------------------:|------------------------:|----------------------:|---------------------------:|---------------------:|------------------------:|----------------------:|---------------------------:|
|              82.0619 |                147.567  |               42.1401 |                   nan      |             10.5517  |                 9.81947 |               8.24638 |                  nan       |
|              69.8968 |                120.265  |              240.206  |                     5      |             10.5317  |                10.5942  |              12.2065  |                    2       |
|              81.1059 |                106.62   |              106.54   |                    41.0526 |              9.94521 |                 9.57153 |               8.97671 |                    9.78947 |
|             102.648  |                121.601  |              108.329  |                    45.0248 |              9.75447 |                10.0727  |               9.27802 |                    8.71281 |
|             110.514  |                 97.4084 |               89.7127 |                    41.4274 |              9.71389 |                10.4905  |               9.43699 |                    7.74062 |

## Imputations

Due to the prevalence of null values, an imputation strategy must be employed to make meaningful predictions in the later part of this analysis. In this dataset, the only relevant feature that must be filled is the average rating. Below is the distribution before imputation. 

<iframe
  src="assets/impute-before.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The imputation strategy is to impute the mean average rating for each tag group, since tag is likely to be a discerning factor for a recipe's rating. Below is the distribution after imputation. Note that the distribution stays the same, with more values being added to the higher ratings. 

<iframe
  src="assets/impute-after.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
