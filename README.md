# Text-Mining-Project
codes of my final project for Text Mining Course
### Introduction 
With the current downward of the beer industry, wine has become one of the alcoholic beverages that have passed to play a relevant role on the focus of beverages manufacturers and marketing companies. It is also known that millennials and generation z are very oriented in consuming high-quality products (and not necessarily branded) even though they cost more. 

According to Forbes, high-quality wine consumption has reached such levels that Amazon started a wine delivery service in Seattle to bring the tasting room experience online. Amazon Wine executive Steve Johnson focused on certain variables to select the wines for the tastings: "we offer product pages where sellers can choose to include tasting notes, professional ratings and awards, enhanced imagery, videos and more."  As is common knowledge, Amazon utilizes big data to support achieving optimal results with its decisions, and wine selection is part of this methodology. 

With this in mind, our team decided to analyze a dataset which contains vast information about wine tasting by experts (sommeliers) to determine how their reviews translate into significant insights that can drive action in businesses. 

### Data Description
The dataset that has been used for this report was taken from the public data platform  Kaggle. Originally, these reviews were scraped from WineEnthusiast which is a digital platform containing information and products around the wine industry. This website is the world’s leading source of wine-related merchandise, thus being a source of vast information about preferences and trends in the market. The selected dataset was updated in 2017, and consists of 130k rows and 10 columns, the columns contain information about different aspects of the sample and are specified as follows:

1.	Country: Where the wine was made. Consumers feel very identified with this feature. This is an important factor as weather determines some of the grapes’ most important characteristics. Wines in this sample are heavily concentrated in three countries United States (42%), France (17%) and Italy (15%). The remaining 26% is split into 40 other countries.
2.	Description: This is the sommelier’s actual review of the product. It is entered on a text format, which makes it ideal for a text mining project. 
3.	Designation (grapes’ vineyard within the winery). This is a particularly dispersed characteristic which makes it harder to obtain insights from it. More specifically, between the 130,000 wines tested there are around 40,000 different designations.
4.	Points: this is an evaluation on a 1 to 100 scale. However, sommeliers will only submit a review for wines that have scored over 80 points; subsequently, there won’t be any information on this dataset regarding low scoring wines. The mean of these scores is 88 points with a standard deviation of 3.04, what seems kind of tight for high scores.
5.	Price: The price per bottle is entered all in the same currency to facilitate its analysis, in this case, the unit is US dollars. 
6.	Province: The province or state within a country that the wine is from. 
7.	Region_1: The wine growing area within a province or state (ie Napa). Within the US wines, 28% of the wines sampled come from the Napa Valley region.
8.	Region_2: Sometimes there are more specific regions specified within a wine growing area (ie Rutherford inside the Napa Valley), but this value can sometimes be blank
9.	taster_name: This is the name of the Sommelier that has submitted the review. One important factor to consider is that around 20% of the reviews come from the same sommelier: Roger Voss. Having a large portion of the reviews coming from the same expert can be a potential issue as there might be some biases involved in his perception of the different wines being sampled.
10.	taster_twitter_handle: This is the name of the twitter account of the sommelier. Twitter is a widely used platform for wine connoisseurs where they can share these kinds of reviews with their followers.
11.	Title: The title of the wine review, which often contains the vintage if you're interested in extracting that feature. The vintage is also a great indicator of the wine’s quality and value.
12.	Variety: The type of grapes used to make the wine (ie Pinot Noir).
13.	Winery: The winery that made the wine. The brand is becoming an increasingly important piece of information as consumers tend to pick local wineries over big brands. This means that there are a growing number of wineries in the industry.



### Objectives for the Analysis 

Based on what each column represents, we determined that the relevant analysis will be done about the Description column since it is the one that contains the words that relate to the wine characteristics. Based on the relationships we can find with the other variables, reads columns, we will be able to translate our findings into actionable recommendations to business involved in the wine industry. 

Thus, the main objective of this analysis is to prove that there is a relationship of any kind between the words used in the reviews with other variables pictured in the dataset and that the reviews, as well as other relevant variables, can predict chosen responses. The goal is to be able to recommend a backward marketing strategy for wine producers and retailers.

As we could consciously note from the big picture of the dataset, there are some variables that are not significant for our objectives. However, quality and certain characteristics seem to influence the price. In the same manner, in order to predict winery correctly, description and price are used as predictors. 



### Methodology 

In order to perform a more comprehensive analysis of the dataset, we selected two different methodologies for this project. The selected methods were (1) supervised learning and (2) topic modeling which are explained in the following paragraphs. 

Supervised Learning

Supervised learning is based on human feedback and allows to use our humankind experience and perspective to guide the analysis. However, this analysis can be inaccurate or biased, to what we need to be paying attention to.

The first step was to clean the data to ensure that it is consistent and functioning without errors that can affect the final results. In order to do this, we choose two variables of interest as our predictors as it was mentioned before. They are description and price. The description is the only column that contains text data, and the price is a numerical value that can represent quality and certain types of wines.

We choose the variety and winery as two responses. We only include the top 10 varieties and top 24 wineries in the dataset because the variety and winery columns contain more than 1000 levels each. If we include all the levels in our final model, the performance of the models will be quite inaccurate.

Next, we extracted the features using different methods and built different classifiers to predict our response. We use the bag of words, 2-grams TF-IDF, and 3-grams TF-IDF. Ideally, the 2-grams and the 3-grams should extract more features than a bag of words and thus, give more accurate results.




### Text Classification

For text classification, we use the extracted features and implemented three classification method: Naive Bayes, Support Vector Machine and Logit Classifier. 

First, we divide our training and test dataset using the cross-validation method. We divide the datasets 10 times. For each time, we randomly select 20% from the original dataset as test dataset and the rest as training dataset. For each training and test data pair, we compute the precision rate of predicting winery using three different classification methods.  We use the different extracted features in the above part (2-gram TF-IDF, 3-gram TF-IDF, and bag of words) to fit in the classification model. These three classification methods can be derived from the packet “Sklearn” directly. Then we compute the average precision rate for each classification method based on ten training and test pairs.

Unsupervised Learning: Topic Modeling

Initially, we want to analyze reviews and categorize into different topics, for different wine reviews, there seems to contain mainly two topics, which is aromas and taste. So, we set the topic number equal to 2. To introduce sparseness, we set alpha and beta both equal to 0.5.

Pros and Cons

From the results we got for using column “description” and “price” to predict winery, we can see that the precision rate are not being improved a lot by including more covariate. This may because this method has overfit problem. The precision rates for all the three classifiers are close to 1. When the model is trying to fit the outliers in the training data, although it will have higher precision rate in the training dataset, it will lower the predict precision in test dataset. 

Since the reviewed data is constituted by unbiased opinions on different wines provided by experts, the Description text does not contain attitude; rather, it is just descriptive words. Therefore, we cannot perform sentiment analysis.

In addition, due to the nature of the review data, the descriptive words seem to contain the same topic, which is indistinguishable as indicated by poor performance generated by topic modeling(belwo). We will discuss in more detailed in the later chapter.



### Results and Discussion 

As it was previously explained, our methodology consisted in using the three different feature extraction methods (2-gram, and 3-gram, and bag of words) to fit the test data using the three text classification methods (Naive Bayes, Support Vector Machine and Logit Classifier) 


- Using review data (“description) to predict variety

The following shows the results:
Naive Bayes:
2-gram TF-IDF: 73.7%; 3-gram TF-IDF: 69.9%; Bag of words: 77.2%
Logit Regression:
2-gram TF-IDF: 66.1%; 3-gram TF-IDF: 48.3%; Bag of words: 82.2%
Supervised Vector Machins:
2-gram TF-IDF: 75.9%; 3-gram TF-IDF: 69.9%; Bag of words: 81.3%
The summarized table is shown in the appendix.

From the above table, for each classifier, using bag of words method to extract features will help to get a more accurate result. Among the three classifiers, Naive Bayes gives the best precision rate. From all the methods we tried, the best accuracy rate is 82.2% using bag of words to extract features and using Logit regression to do classification.

- Using review data (“description”) to predict winery

The following shows the results:
Naive Bayes:
2-gram TF-IDF: 37.4%; 3-gram TF-IDF: 29.3%; Bag of words: 44.7%
Logit Regression:
2-gram TF-IDF: 36.8%; 3-gram TF-IDF: 27.3%; Bag of words: 41.7%
Supervised Vector Machins:
2-gram TF-IDF: 39.5%; 3-gram TF-IDF: 29.4%; Bag of words: 40.0%
The summarized table is shown in the appendix.

From the above table, for each classifier, using bag of words method to extract features will help to get a more accurate result. Among three classifiers, Naive Bayes gives the best precision rate. From all the methods we tried, the best accuracy rate is 44.7% using bag of words to extract features and using Naive Bayes to do classification. 
- Using review data and price (normalize it as dummies) to predict winery 

Using the similar technique as above, but this time, we will predict winery by incorporating two different variable. We normalize the price as dummyvariables when building the model. Intersecting each feature extraction with each classification method provided the following results for the two proposed predictors

 - Naive Bayes:
2-gram TF-IDF: 34.5%; 3-gram TF-IDF: 29.6%; Bag of words: 48.1%

 - Logit Regression:
2-gram TF-IDF: 25.1%; 3-gram TF-IDF: 21.8%; Bag of words: 43.7%

 - Supervised Vector Machins:
2-gram TF-IDF: 24.2%; 3-gram TF-IDF: 21.4%; Bag of words: 42.1%
The summurized table is shown in the appendix. 

From the above table, for each classifier, using bag of words method to extract features will help to get a more accurate result. Among the three classifiers, Naive Bayes gives the best precision rate. From all the methods we tried, the best accuracy rate is 48.1% using bag of words to extract features and using Naive Bayes to do classification. Compared with the using only description to predict winery, include price as a dummy variable increase our precision a little bit, but not too much. The best accuracy is increased from 44.7% to 48.1%, which is improved by 7.6%

- Topic Modeling

The result of topic modeling is shown below. Since the topic modeling is the unsupervised learning, human evaluation of the model is proper in this context. From the result, we can find that the model didn’t perform very well. The first topic seems to talk about aroma and the second topic seems to talk about the wine flavor. But overall, it seems to have some indistinguishable words. 

Topic 0	flavor finish palate aroma fruit cherry note black wine nose
Topic 1	wine fruit flavor acidity drink ripe tannin rich age oak



### Conclusions

In conclusion, our main predictor (description variable, read reviews) can predict variety of the wine, which, as mentioned, refers to the type of wine according to its main characteristics and particularities. However, it does not seem to have any contundent link to wineries in which wines were made. We hoped that the reviews could have have certain wording that refers to particularities of wineries, but it seems that wineries are very difficult to distinguish in the blind tasting. The variety of the wines seems to be rationally predictable by sommeliers.

Under this focus, this study indicates that wineries cannot be distinguished in blind tastings as general as the one studied in this dataset. Our recommendation for these wineries owners is to direct their marketing strategy to local advertising and targeting, instead of base their marketing efforts on their brands, when this one cannot be differentiable.

However, for specific variety of wine manufacturers or sellers, this model is very favorable. A backward marketing strategy would direct the right terminology (similar to the one in the reviews) to the targeted market segment. This recommendation is assuming that firms are targeting customers who have made any research and know about quality based on reviews or other informative methods.  

On the other hand, we tried to improve our model by adding price as a predictor for the responses of variety and winery, and it was an unsuccessful attempt. We consider that the other variables would not help to improve the accuracy of the model either, so this is a limitation of this dataset. Another recommendation would be to expand and dig deeper into this topic since as stated at the beginning of this report, online wine consumers targeting looks like a very promising business nowadays. 

