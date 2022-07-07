# Project 3: Web APIs & NLP
Joshua Willey

### Problem Statement

The subreddits r/WorldNews and r/UpliftingNews both consist of reports from around the world.  r/WorldNews contains posts pertaining to major news from around the world, excluding US-internal politics.  r/UpliftingNews, on the other hand, is a place where users share positive stories that lift the spirits to counter the cynicism that is present in much of today's media.  The purpose of this analysis is to build a model that will differentiate between posts from each subreddit, and will be able to pick whether future posts belong in the globally-concerned r/WorldNews or the positive environment of r/UpliftingNews.


### Data Collection

To train the model, I gathered data from both subreddits between the dates of March 1, 2022 and April 24, 2022.  55,716 total posts were gathered, 51,718 from r/WorldNews and 3,998 from r/UpliftingNews.  For this model, I evaluated the text in each post's title.


### Data Processing

To prepare the data, I combined the posts from both subreddits into a single dataframe.  I then removed all non-ASCII characters and vectorized the cleaned titles, which removed punctuation, made all letters lowercase, and tokenized the individual words.  For vectorization, I ran both CountVectorizer and TfidfVectorizer, testing both on a basic Logistic Regression model.  I also tried several methods of dealing with the imbalance of data, including Random Oversampling, AMOTE, ADASYN, and the balanced_class_weight LR parameter.  After testing combinations of vectorizers and balance handling methods in my Logistic Regression model, I chose TfidfVectorizer and Random Oversampling.


### Model Evaluation

I fit the data to three separate classification models: Logistic Regression, Random Trees, and Naive Bayes.  The goal was to achieve a model that would be sensitive enough to detect the minority class (r/UpliftingNews), but would still exceed the accuracy of the baseline model.  Ultimately, none of the models I test were able to significantly exceed the baseline score of 92% accuracy.  The Random Forest model achieved the most sensitivity, with a recall score of .104 and a balanced accuracy score of .542.  However, this was at the expense of precision, which dropped to .295, and accuracy, which measuread .018.  The Logistic Regression model achieved slightly higher than baseline accuracy, at almost 93%, but had poor sensitivity to the minority class.


### Conclusion

Both subreddits closely follow current events, and thus have a lot of overlap.  None of the models were able to show significant improvement on the baseline model.  In future testing, I may try to add stopwords in the vectorization process to reduce overlap, and possibly add a sentiment analyzer to pick up on what should be the more positive r/UpliftingNews.