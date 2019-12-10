# Reddit-Post-Classification
A classification model that leverages data web-scraped from Reddit and applies Natural Language Processing as well as classification algorithms to classify sub-reddits.

# Problem Satement
* Reddit relies on users to organize their posts into sub-reddits, which are often mis-classified

* Build a model to accurately reclassify  the posts back to their subreddits.

#  Goal:
* Collect posts from two subreddits using Reddit's API

* Use NLP to train a classifier on which subreddit a given post came from

# Background of the subreddits used:

* r/travel is a community about exploring the world.

* r/awardtravel is a place to discuss burning airline miles and hotel points.

# Notebook Links

  * [Model and Insights](https://github.com/payalchodha/Reddit-Post-Classification/blob/master/model%20and%20insights.ipynb)
  * [Sub-reddit Extraction](https://github.com/payalchodha/Reddit-Post-Classification/blob/master/subreddit%20extraction.ipynb)
  
# Executive Summary
The project started by scraping r/travel and r/awardtravel for data. The process of extracting from reddit is fairly simple: 
 *  A basic request set up to access the API
I managed to scrape about 15,000 posts in total.

I made an app on reddit to register and get the keys and password using praw.To extract the title and selftext,I used PushshiftAPI. Once I extracted the titlw and selftext (as body). Then I began the process of cleaning up the data. The cleaning process was fairly simple, as it mostly consisted of dropping null values, stripping all text that was not composed of letters, removing emojis,replacing the [removed] and [deleted] values with nothing. The last major cleaning step I did was to concatenate together the title and body for each post,because if there was no body the title became the body. I then saved the dataframes to a csv file so I could model cleaned data.

So,during preprocessing I removed the urls and links too.Then I combined the dataframes for both the subreddits,as it would be easier to model that ways. And then I looked at the common words that occurred most frequently and added those words to the list of stop words. The last preprocessing step I took was to lemmatize the text; lemmatizing  reduces every word to its dictionary value and is a bit gentle than stemming.

I ran each model twice: once with count vectorization and once with TFIDF vectorization
Every model was optimized with grid-searching(to tune the hyperparameters in a better way)
Models that I considered were:
1. Logistic Regression
2. Multinomial Naive Bayes
3. Random Forest
Once I had my best parameters and best estimator I made a confusion matrix(the confusion gives the clearest visualization of how the model treats each class in the data).I also generated an ROC-AUC curve.

Then, I also wanted to test my model on an unseen data.So I also pulled some extra data from reddit API,stored it in the test.csv and tested my model on that.It performed very good on that.

# DATA dictionaries:
|Feature|Type|API|Description|
|---|---|---|---|
|target |integer|none|The binary column where 1 is for the post came from travel subreddit and 0 for awardtravel| 
|Status |string|Reddit|The title and selftext combined|

  
# Recommendations:
* Logistic regression performs good with cvec  and has even better accuracy score for Tfidf, and it also doesn’t show high variance.
* So I recommend employing Logistic Regression with TfidfVectorizer  moving forward

# Conclusions:

* My model was able to predict with good accuracy the classification of a certain post.That's why it can be leveraged by Reddit to suggest subreddits to a user while writing a post.

* Also it can unlock ways to better target the awardtravel customers for the credit card offers etc.
 
 
 
