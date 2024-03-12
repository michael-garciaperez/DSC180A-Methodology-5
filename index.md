---
layout: default
title: "Mitigating Director Gender Bias in Movie Recommender Systems"
---

## Introduction

Studies in sociology and media studies have revealed a **gender gap** in the film industry, with an **underrepresentation** of **female directors** in film production.
  - In over 2000 films released between 1994 and 2016, only **5%** of the directors were **female**.[[^1]]
  - In top-grossing films released between 2007 and 2021, the ratio of **male to female** directors was **11:1**.[[^2]]

However, the implications of this disparity on recommendation systems is not widely researched.
  - Most studies look at bias from a statistical perspective (e.g., popularity bias).

Many content distribution platforms (such as Netflix) utilize recommendation models for personalized user content.
  - A recommender system filters information (e.g., user and item data) to provide personalized suggestions to users.
  - We investigate whether this gender bias is embedded into the outputs and suggestions of various recommendation models, developed using different similarity metrics and algorithms.

Widely adopted bias mitigation tools (e.g., [IBM's AI Fairness 360](https://aif360.readthedocs.io/en/stable/index.html)) are also optimized for **regression** and **classification** tasks, not recommendation tasks.
  - Our project fills this gap by investigating whether bias mitigation techniques developed for regression and classification tasks can be **extended to recommendation systems**.

Our aim is to develop a fair movie recommender system that minimizes biases associated with the gender of the director.

## Methods

The [data](https://grouplens.org/datasets/movielens/1m/) for **user ratings** is sourced from [MovieLens](https://movielens.org/), an online platform that provides personalized movie recommendations based on users' viewing preferences and rating history.
  - We gather over a million anonymous ratings of approximately 3,900 movies made by 6,040 MovieLens users who joined the platform in 2000.

## Model Development & Evaluation

Your model development content goes here.

## Bias Mitigation

Your content goes here.

## Conclusion & Results

Your conclusion and discussion content goes here.

## References

[^1]: Karniouchina, E. V., Carson, S. J., Theokary, C., Rice, L., & Reilly, S. (2023). *Women and minority film directors in Hollywood: Performance implications of product development and distribution biases.* Journal of Marketing Research, 60(1), 25-51. [DOI: 10.1177/00222437221100217]

[^2]: Smith, S. L., Choueiti, M., & Pieper, K. (2018). *Inclusion in the Director’s Chair. Examining 1,100 Popular Films.* [https://ca-times.brightspotcdn.com/32/1f/434e9de042a9a366c08aac1ed1db/inclusion-in-the-director-2.8.22%20Final.pdf]

