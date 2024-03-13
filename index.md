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

![Distribution of Rating Scores](https://raw.githubusercontent.com/michael-garciaperez/DSC180B-Capstone-Project/main/assets/images/rating_dist.png)

- Ratings in the dataset range from a **discrete** number **between 1 and 5**.
- Most ratings are on the **higher side** with a score of 4. There are less low ratings of 1 and 2 in our dataset.

We further separate this by the **director's gender** to compare the **proportion of ratings** between male versus female directors.

![Proportion of Ratings by Director Gender](https://raw.githubusercontent.com/michael-garciaperez/DSC180B-Capstone-Project/main/assets/images/prop_ratings.png)

- **Entirely-male directed** movies received a **greater proportion** of **5 star** ratings.
- This leads us to define the rating of **5 stars** as a high rating, using this definition later to assess for bias on whether fully male-directed movies are **advantaged** to receive **5 star** rating prediction.

Note that there **is** a strong **class imbalance** within the dataset, where **most movies are entirely-male directed**. 
- Refer to the report for a full breakdown on the class imbalance.
- Because of **similar utility performance** in **predictive models** across **director genders**, plus the time-constraints of the project and limited resources, we decide not to correct the class imbalance.

Utilizing AIF360 to assess for bias, we measure the **Disparate Impact** and **Statistical Parity Difference** of our dataset.

- Disparate Impact Before Mitigation: ~0.694
  - The **3/4ths rule** is a standard threshold used for disparate impact analysis. If the favorable outcome rate for a group is < 75% (a.k.a. 3/4), bias is present in the dataset.
  - The Disparate Impact value of ~0.69 maps to a percentage of ~69%, which is < than 75%. There is a **bias in how 5-star ratings** are distributed between the different genders of the directors.
  - Movies with **female directors** are getting 5-star ratings about **69% as often** as **fully male-directed** movies.
  - Fully male-directed movies, as the **privileged group**, are **more likely** to achieve the **favorable outcome** compared to movies with female directors.

- Statistical Parity Difference Before Mitigation: approx. -0.068
   - A Statistical Parity Difference **close to 0** shows **no difference** in the proportion of **favorable outcomes** between different groups.
   - Our value is close to 0 and does **not show a discernible bias**.

While the Statistical Parity Difference does not notably capture bias, the **Disparate Impact** shows a strong indication of **bias based on the director gender**.

## Model Development & Evaluation

AIF360's bias mitigation techniques are optimized for classification and regression tasks, so first examine bias mitigation in our dataset on a **classifier model**.
- We evaluate the efficacy of bias mitigation techniques within a classifier before extrapolating these insights to recommender systems.

Random Forest (Classification Algorithm):
- We use a **Random Forest Classifier** to predict whether a user will **give a movie a perfect rating (5 stars)** based on various movie attributes, including the year of release, genre, and **whether or not the movie is entirely-male directed**.
  - Full details on model development (e.g., training/testing data, hyperparameter tuning) can be found in the report.

Bias Metrics Before Mitigation:
- Disparate Impact: ~0.668
     - The Disparate Impact suggests that the unprivileged group is at a disadvantage compared to the privileged group, as they are less likely to receive favorable outcomes.
- Statistical Parity Difference: approx. -0.0743
      - The Statistical Parity Difference is not a strong indicator of bias due to this value being close to 0.

Accuracy Before Mitigation: ~0.787
- Refer to the report for full breakdown on utility measures including precision, recall, and f1-score.
- Refer to the report for figures on the ROC-AUC Curve, Precision-Recall Curve, and Feature Importances Bar Plot.

Recommender Systems
- We develop several recommender systems using various similarity metrics and matrix calculations.
- Mathematical formulas for each similarity metric can be found in the definitions section of the report.
- To examine patterns in the director gender breakdown of recommended movies, we look at the recommendations for two different users with different rating histories.
- User 1:
    - graph
    - Only ~5% of User 1's rating history included at least one female director.
    - User 1 did not have a very diverse rating history in terms of director gender.
- User 2908:
    - graph
    - User 2908 had the greatest representation of female directed movies in the dataset, as ~44% of the movies they have rated featured female directors.

Recommender System using Jaccard Similarity
- A Movie-User matrix is created based on user ratings. The recommendation algorithm relies on Jaccard Similarity between movies to generate personalized recommendations for a user.
- Recommendations for User 1:
    - graph
    - The top 10 recommended movies for User 1 do not provide diverse suggestions.
    - All the recommended movies are entirely male-directed, introducing bias and overlooking potentially good recommendations directed by females.
- Recommendations for User 2908:
    - graph
    - User 2908's recommended movies did not have any female directors, every movie recommended was entirely male-directed.
    - Despite User 2908 having a more gender diverse rating history, the Jaccard recommender system performed the same as it did for User 1, who had low gender diversity in ratings.

We investigate whether recommender systems using **different similarity measures** are able to provide more diverse recommendations. We look at **Cosine Similarity**, a popular measure for capturing nuanced relationships between items and users, and **Pearson Correlation**, which captures linear relationships between variables.

Recommender System using Cosine Similarity
- Cosine similarity evaluates the similarity between movies based on the cosine of the angle between their respective feature vectors, representing user ratings.
- The higher the cosine similarity value, the more alike two movies are considered to be in terms of user ratings.
- Recommendations for User 1:
    - graph
    - For User 1, the Cosine Similarity recommender system exhibited the same behavior as the Jaccard Similarity recommender system. Each of the top 10 movie recommendations are fully directed by males.
- Recommendations for User 2908:
    - graph
    - User 2908's recommended movies using Cosine Similarity were more diverse than their recommended movies using Jaccard Similarity, but still had a lot less movies featuring female directors than their rating history.

Recommender System using Pearson Correlation
- This model measures the linear correlation between two movies based on the ratings provided by users.
- A higher Pearson correlation indicates greater similarity in user ratings between two movies.
- It identifies the common users who have rated both movies, then computes the correlation coefficient based on their ratings.
    - If there are no common users, the correlation is considered to be zero.
- Recommendations for User 1:
    - graph
    - Recommendations for User 1 exhibited an increase in diversity concerning the gender of movie directors (compared to the Jaccard and Cosine similarity models).
    - 20% of User 1's recommended movies featured a female director, a notable increase compared to the ~5% average observed within User 1's watch history.
- Recommendations for User 2908:
    - graph
    - User 2908's recommended movies using Pearson Correlation performed the same as Jaccard Similarity, with no movies featuring female directors.
- For User 1, the recommender system using Pearson Correlation yielded the greatest percentage of female directed movies (20%), whereas it was Cosine Similarity (10%) for User 2908. -    - User 1 received more diverse recommendations using Pearson, even though they rated less female directed movies than User 2908.

It is inconclusive which similarity function yields in the least biased recommendations, since it varies per user.

Beyond similarity metrics, recommender systems can use **Singular Value Decomposition (SVD)**, a Matrix Factorization-based algorithm that  captures latent factors underlying user preferences.

Recommender System using Singular Value Decomposition
- The recommender model uses an SVD object, which is trained to optimize predictive performance using user-item interactions.
- This algorithm allows us to make predictions for specific movies for users.
- The model's utility is evaluated using Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE).
    - RMSE tends to penalize large errors more than smaller ones due to the squaring operation.
        - It is useful for comparing models and understanding the spread of errors, but it is not very intuitive for human interpretation.
    - MAE provides a more straightforward and human-friendly interpretation.
        - It represents the average magnitude of errors without considering their direction (i.e., whether they are overestimations or underestimations).
        - MAE gives the average absolute error, making it easier to understand/interpret in real-world terms.
            - For example, if the MAE is 5, it means, on average, that the model's predictions are off by 5 units from the actual values.
- Bias metrics:
    - Disparate Impact Before Mitigation: ~0.38
        - This metric indicates a significant disparity in favorable outcomes between movies directed by males and those directed by females, with a value of ~0.38 suggesting unequal representation in the recommended items.
    - Statistical Parity Difference Before Mitigation: approx. -0.052
        - The negative value of approx. -0.052 does not significantly indicate a bias favoring movies directed by females in receiving favorable outcomes.
- Utility:
    - RMSE (Root Mean Squared Error) Before Mitigation: ~0.71
        - The RMSE value signifies the average discrepancy between predicted and actual ratings, reflecting the prediction accuracy of the model in prioritizing entirely-male directed content.
    - MAE (Mean Absolute Error) Before Mitigation: ~0.56
        - The model's average deviation from actual ratings is approximately 0.56 units, allowing insight into prediction accuracy without considering the direction of errors.
- To convert the predictions to recommendations, we recommend the user movies that they are predicted to give 5 stars.
    - Both User 1 & User 2908 received all entirely-male directed movies as recommendations, despite having a stark contrast in the diversity of their rating history.
    - User 1:
        - graph
    - User 2908:
        - graph

## Bias Mitigation

A pre-processing technique called **reweighing** is employed as a bias mitigation strategy.
- Pre-processing techniques are applied to the training data from which a model is learned.
- More information on these terms can be found in [AIF360's glossary](https://aif360.res.ibm.com/resources#glossary).

The dataset is reweighed using the **Reweighing technique**, which **adjusts the instance weights** in the different groups and labels to mitigate bias.
- More information on Reweighing in particular can be found through the [documentation](https://aif360.readthedocs.io/en/latest/modules/generated/aif360.algorithms.preprocessing.Reweighing.html).

Random Forest Pre-Processing Bias Mitigation
- A Random Forest Classifier is **trained on the reweighed dataset**.
- This approach aims to address bias in the original model's predictions by reweighing instances based on the protected attribute 'all_male_director' before training the model.
- Bias Metrics After Mitigation:
    - Disparate Impact: ~1.0
    - Statistical Parity Difference: ~0.0
    - The bias metrics **improved significantly**, with the Disparate Impact being approximately 1 and the Statistical Parity Difference close to zero, **indicating a fair model**.
- After retraining on the reweighed data, the Random Forest Classifier with 100 estimators achieved an **accuracy of ~0.79**, which **did not increase or decrease** compared to the original accuracy of  ~0.79.
- This suggests that the reweighing technique **successfully mitigated bias**, resulting in a **fairer model** while maintaining **similar predictive accuracy**.

The similarity metrics used in our recommender models above (Jaccard, Cosine, and Pearson correlation) rely on the dataset to calculate similarities between movies.
- Since the dataset exhibits bias towards male-directed content, these similarity metrics also favor male-directed movies in recommendations.
- By applying reweighing, the transformed dataset aims to mitigate such bias, ensuring that similarity calculations consider a more balanced representation of movies directed by individuals of different genders.

We develop the models again using the same similarity metrics (Jaccard, Cosine, and Similarity) on the **transformed dataset**.
- The percentage of movies with female directors in the recommendations stayed the same as before for all similarity metrics for User 1 and User 2908.

Like the other similarity metrics above, **SVD** relies on user-item interaction data to make recommendations.
- By using a reweighted dataset to adjust the representation of male-directed and female-directed movies, we investigate whether there is a difference in recommended movies before and after mitigation.
- Bias Metrics:
    - Disparate Impact After Mitigation: ~0.6295
        - The Disparate Impact After Mitigation showed a more fair result.
        - The Disparate Impact Before Mitigation was ~0.38, increasing to ~0.63 after. This value **approached 1** and indicates a **more fair model**.
    - Statistical Parity Difference After Mitigation: approx. -0.004
        - The Statistical Parity Difference was low to begin with (i.e., close to 0) and did **not indicate bias** in that metric itself.
- Utility:
    - RMSE After Mitigation: ~1.2134
        - RMSE increased from ~0.71 to ~1.21.
    - MAE After Mitigation: ~0.989
        - MAE increased from ~0.56 to ~0.989.
    - Model utility **worsened after Reweighing** was applied.
    - There appears to be a **trade-off between model utility and fairness**, as the **predictive capabilities worsened** and will not perform as well.

- To convert the predictions to recommendations, we recommend the user movies that they are predicted to give 5 stars.
    - The model performed the same as before bias mitigation, both User 1 & User 2908 continue to receive all entirely-male directed movies as recommendations.

## Results

Reweighing as a pre-processing bias mitigation technique was **successful** for the **Random Forest Classifier**, but remains **limited** in its application to **recommender systems**.

Despite applying the reweighted dataset to the recommender models utilizing Jaccard and Cosine Similarity and Pearson Correlation, there was **no difference** in the diversity of movie recommendations.
- The movie recommendations continued to exhibit a dominance of male-directed content, indicating that the reweighing technique did not effectively mitigate gender bias in these particular models.
- It appears that reweighing the dataset **did not impact** the **calculation of the similarity metrics**, resulting in the same top 10 movie recommendations before and after bias mitigation in the model.

However, **reweighing** the recommender system using **SVD** was able to yield a **Disparate Impact closer to 1**, effectively **mitigating some bias** in the **predictions of rating scores**.
- Before graph
- After graph
    - After applying Reweighing, the **proportion of 5 star ratings** (perfect ratings, the favorable outcome) became **more equal** between entirely-male directed movies & movies featuring female directors. 
- The **model utility decreases** though, making Reweighing not the ideal choice due to lower predictive performance.
- When **predictions** were **converted to recommendations**, there was still a **dominance of male-directed content**.

## Discussion
The efficacy of AIF360's Reweighing technique on bias mitigation in recommender systems is subject to ongoing discourse.
- Reweighing made no difference in the similarity metric based recommender systems.
- Rhe predictions from SVD saw a substantial bias mitgiation. Yet, when the SVD predictions are converted to recommendations, there continues to be a dominance of entirely male-directed films being recommended.
- 
There is potential for AIF360 as a bias mitigation tool in recommender systems, although the success of bias mitigation techniques depends on the underlying calculations of the recommender system.

Because of the underrepresentation of female film directors in the dataset, reweighing adjusts the distribution of instances across different groups.
- This may lead to a reduction in the sample size of the majority group to achieve parity, which loses data and can limit the model's ability to capture the full complexity of the dataset.

Additionally, simply examining the director's gender in movie recommender systems is not enough to consider.
- It is essential to consider how gender can intersect with other demographic factors.

Lastly, while the bias mitigation techniques in this project were able to achieve a far model in terms of statistical fairness metrics, these techniques do not fully address the underlying systemic biases present in society.
- **Technosolutionism**: the reliance on technological solutions to address complex social issues, ignoring broader societal, ethical, and political implications.
- Bias mitigation alone cannot effectively address biases without the work of fields such as sociology, cultural, and media studies to work towards changing the dynamics that influence film production, distribution, and consumption.

## References

[^1]: Karniouchina, E. V., Carson, S. J., Theokary, C., Rice, L., & Reilly, S. (2023). *Women and minority film directors in Hollywood: Performance implications of product development and distribution biases.* Journal of Marketing Research, 60(1), 25-51. [DOI: 10.1177/00222437221100217]

[^2]: Smith, S. L., Choueiti, M., & Pieper, K. (2018). *Inclusion in the Director’s Chair. Examining 1,100 Popular Films.* [https://ca-times.brightspotcdn.com/32/1f/434e9de042a9a366c08aac1ed1db/inclusion-in-the-director-2.8.22%20Final.pdf]
