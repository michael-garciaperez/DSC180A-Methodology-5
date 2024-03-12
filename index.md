---
layout: default
title: "Mitigating Director Gender Bias in Movie Recommender Systems"
---

## Introduction

Studies in sociology and media studies have revealed a **gender gap** in the film industry, with an **underrepresentation** of **female directors** in film production.
- In over 2000 films released between 1994 and 2016, only **5%** of the directors were **female**.[[^1]]
- In top-grossing films released between 2007 and 2021, the ratio of **male to female** directors was **11:1**.[[^2]]

The implications of this disparity on recommendation systems are not widely researched.
- Most studies look at bias from a statistical perspective (e.g., popularity bias).

Many content distribution platforms (like Netflix) utilize recommendation models for personalized user content.
- A recommender system filters information (e.g., user and item data) to provide personalized suggestions to users.
- We investigate whether this gender bias is embedded into various recommendation models, developed using different similarity metrics and algorithms.

Widely adopted bias mitigation tools (e.g., [IBM's AI Fairness 360](https://aif360.readthedocs.io/en/stable/index.html)) are optimized for **regression** and **classification** tasks, not recommendation tasks.
- Our project fills this gap by investigating whether bias mitigation techniques developed for regression and classification tasks can be **extended to recommendation systems**.

Our aim is to develop a **fair** movie recommender system that minimizes biases associated with the **director's gender**.

## Methods

The [data](https://grouplens.org/datasets/movielens/1m/) for **user ratings** is sourced from [MovieLens](https://movielens.org/), an online platform that provides personalized movie recommendations based on users' viewing preferences and rating history.
- We gather over a million anonymous ratings of approximately 3,900 movies made by 6,040 MovieLens users who joined the platform in 2000.

The [data](https://figshare.com/articles/dataset/U_S_movies_with_gender-disambiguated_actors_directors_and_producers/4967876) on the director's gender comes from Northwestern University's Amaral Lab, which looks at the gender breakdown of the crew of U.S. films released between 1894 and 2011.

[IMDb's dataset](https://datasets.imdbws.com/) on titles and identifiers is utilized to combine the two datasets mentioned above.

Full procedures on data cleaning and merging can be found in the report linked on the page.

To prepare our data for model development, we **binarize** the director gender column.
- Binarization involves categorizing the variable into two distinct groups based on a specified threshold.
- Movies can have more than one director, so we note the proportion of directors for each movie who identify as male.
    - We convert this proportion to 1 if the movie is fully directed by males, and 0 if the movie involves at least one female director (i.e., is not entirely male directed).

![Distribution of Rating Scores](../images/rating_dist.jpeg)

- Ratings in the dataset range from a **discrete** number **between 1 and 5**.
- Most ratings are on the **higher side** with a score of 4. There are less low ratings of 1 and 2 in our dataset.

We further separate this by the **director's gender** to compare the **proportion of ratings** between male versus female directors.

![Proportion of Ratings by Director Gender](../images/prop_ratings.jpeg)

- **Entirely-male directed** movies received a **greater proportion** of **5 star** ratings.
- This leads us to define the rating of **5 stars** as a high rating, using this definition later to assess for bias on whether fully male-directed movies are **advantaged** to receive **5 star** rating prediction.

Note that there **is** a strong **class imbalance** within the dataset, where **most movies are entirely-male directed**. 
- Refer to the report for a full breakdown on the class imbalance.
- Because of **similar utility performance** in **predictive models** across **director genders**, plus the time-constraints of the project and limited resources, we decide not to correct the class imbalance.

## Model Development & Evaluation

Your model development content goes here.

## Bias Mitigation

Your content goes here.

## Conclusion & Results

Your conclusion and discussion content goes here.

## References

[^1]: Karniouchina, E. V., Carson, S. J., Theokary, C., Rice, L., & Reilly, S. (2023). *Women and minority film directors in Hollywood: Performance implications of product development and distribution biases.* Journal of Marketing Research, 60(1), 25-51. [DOI: 10.1177/00222437221100217]

[^2]: Smith, S. L., Choueiti, M., & Pieper, K. (2018). *Inclusion in the Director’s Chair. Examining 1,100 Popular Films.* [https://ca-times.brightspotcdn.com/32/1f/434e9de042a9a366c08aac1ed1db/inclusion-in-the-director-2.8.22%20Final.pdf]

