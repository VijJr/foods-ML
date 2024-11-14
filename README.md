
# Recipe Analysis

Analysis of recipes for EECS398 at the University of Michigan

**by** Vijay Ravi \| **Email:** <a href="mailto:vijjr\@umich.edu">vijjr\@umich.edu</a>

# Introduction

The goal in this project was to analyze the recipes and associated ratings as found on foods.com since 2008. Included is 83,782 recipes, and an additional 731,927 independently sourced ratings, which totals to 234,429 matching recipe/ rating observations

The goal of this analysis is to predict information about the nutrition for each recipe, primarily information about the calorie and protein breakdown. Hopefully as a result, a trend will become apparent, making it possible to predict the caloric value of a recipe given some indicators. 

Together these datasets include information about recipe nutrition, time to prepare, the number of steps, ratings for each recipe, and more. A detailed breakdown is provided below. Note that some irrelevant features were dropped. 

| Column | Description |
| ----------- | ----------- |
| `id` | A unique ID for each recipe / rating |
| `minutes` | The time to complete each recipe |
| `tags` | A list of tags associated with a recipe |
| `nutrition` | The nutrition information (i.e. calories, protein, fats, etc) |
| `n_steps` | The number of steps in a recipe |
| `rating` | The rating provided |

# Data Cleaning and Exploratory Data Analysis

