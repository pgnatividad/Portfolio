

## Problem Statement:
We are to make a binary classifier model out of scrapped Reddit posts to determine which two subreddits(of our choosing) the posts are from. The two subreddit chosen were: r/ChicagoBulls and r/Thunder 

## Scraping:
Scraping was performed using Pushshift to fetch more than the 1k limit of Reddit's API. Data was gathered from 3 years deep. The window of 3 years was chosen since team trajectories change a significant amount in a short time frame. The team 5 years ago is a significantly different team for what it is today. The three year window would give a general idea of what the team is like today. The data was fetched in 1 year increments to help perform sentiment analysis year after year. Three batches of data were used for modeling: A batch filted with atleast 1 comment in the post, a batch with atleast 4 comments, and a batch with atleast 10 comments. The different number of comments was used to filter "higher quality" posts that promoted discussion.

## Modeling:
Models were created for each batch of posts. Pipelines were used to streamline the optimization process. Transformers used were CountVectorizer and TfidfVectorizer. Estimators used were Logistic Regression, Multinomial Naive Bayes, and Binomial Naive Bayes. The best dataset to model from was the 4 comment batch. The best transformer was TfidfVectorizer with a Ngram Range of 1, 15000 features, and the standard English stopwords. The best estimator was Logistic Regression with a C of 1 and Ridge as the penalty.

## Metrics:
|Metrics|Values|
|-|-|
|Training Accuracy|95.501 %|
|Test Accuracy|92.175 %|
|Sensitivity|0.952|
|Specificity|0.889|
|ROC AUC Score|0.978|


## Top 10 Words for R/Thunder:
|Word|ln Odds|
|-|-|
|thunder|10.6|
|westbrook|7.83|
|russ|7.34|
|okc|7.14|
|adams|5.59|
|presti|4.45|
|melo|4.25|
|roberson|4.07|
|billy|4.01|
|russell|3.93|

## Top 10 Words for R/ChicagoBulls:
|Word|ln Odds|
|-|-|
|bulls|-14.3|
|lauri|-6.10|
|chicago|-6.03|
|jimmy|-5.16|
|wade|-5.08|
|lavine|-4.82|
|rondo|-4.65|
|markkanen|-4.62|
|dunn|-4.53|
|hoiberg|-4.38|

## Analysis:
The words most indicitive of the team were proper nouns. They primarily consisted of the players but also included coaches, team name, city, name of the team, and general managers. The model has low bias and low variance. The training and test score were within 3.5% of each other. The model was great at predicting Thunder posts but was less accurate at predicting Bulls post. The model had a high ROC AUC score showing that there was great separation between the two populations. 

## Sentiment Analysis:
Anova analysis shows that there is a difference betwen the Bulls and Thunder subreddits for all three scores especially in the negative category. A sentiment analysis of the the posts on r/Thunder through 3 years did not reveal any trends. Performing Anova analysis of the sentiment scores through the 3 years did not show any a p-values below an alpha of 0.05

## Next Steps:
There is a lot more potential to add complexity to the project. The two teams chosen are in different conferences and (at the time of the project) different trajectories. The teams have very little reason to overlap, so they are distinct from each other. More teams can be added to this project. Teams that are divisional rivals with either team or teams that have trade interest in the Thunder or Bulls players. It is interesting to note that for the Bulls one indicitive word was 'Lebron' who is a player for the Lakers. For the Thunder, an indicitive word was 'rockets' a rival team. Another challenge with modeling with multiple teams is that logistic regression can not be used. Another estimator such as Random Forest or Naive Bayes needs to be used. 



