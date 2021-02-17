### Problem Statement

Formula 1 is a sport most widely viewed in Europe. This project seeks to explore ways in which Formula 1 can efficiently market itself to viewers outside of Europe. Specifically, we will try and find ways of marketing towards Nascar viewers given that they have already demonstrated an interest in motorsports and should be an easier population to convert to Formula 1. 

### Methodology

We will begin by web scrapping posts from Formula 1 and Nascar subreddits. Using these web scraped posts we will use text vectorization and Multinomial Naive Bayes and random forest classification that will model how important certain words are for determining if a Reddit post belongs to either Formula 1 or Nascar subreddits. Once a model with sufficient accuracy is created we can then look at the feature importance of each word. By determining which words are most important to Nascar viewers we can then get a better idea of ways to market Formula 1 to Nascar viewers.

---

### Data Collection
Using the [pushshift api](https://www.kaggle.com/c/dsir-1019-project-2-regression-challenge/data) I gathered 1,000 posts from the [Nascar subreddit](https://www.reddit.com/r/NASCAR/) and 1,000 posts from the [Formula1 subreddit](https://www.reddit.com/r/formula1/). 100 posts were collected at a time across even intervals. Because most posts in these subreddits are images, only the posts titles were used in the analysis.

--- 

### Data Cleaning and Exploration

To begin, duplicate posts were first dropped from the data frame. After removing duplicates, I then explored the average number of words for titles to look for outliers. The longest post ended up being 56 words. I determined this was not an outlier. The distribution of outliers can be found below.

![Average Post Word Count](https://git.generalassemb.ly/albertfrantz/Submissions/blob/master/projects/project_3-master/Images/word_count.PNG)

Interpretation: Title word count is right-skewed with most titles being about 10 words. No major outliers.

The most important data cleaning process for this research was determining words to exclude from the analysis that would not provide useful marketing information. I discovered that the most common words were ones that did not provide useful marketing information so I decided to include English stopwords. After further analysis, I also determined that certain words including 'Nascar' and 'formula1' should be removed as they once again did not provide marketing information. After removing common English words as well as specific racing words and racing drivers the most common words were found. After these adjustments were made the 15 most common words can be found below.

![15 Most Common Words](https://git.generalassemb.ly/albertfrantz/Submissions/blob/master/projects/project_3-master/Images/common_words.PNG)

Interpretation: We now have the most common words that may be useful for marketing formula 1 to Nascar fans.

---

### Modeling

My goal was to create a model that could accurately predict subreddits given text while also being interpretable for marketing strategy. I decided to use two models: multinomial Naive Bayes and random forest classification. I decided on these models as they generally work very well on text data, are white-box models, and provide interpretable results which are essential for answer my question. I needed these models to perform better than the baseline model which accurately predicts subreddits 50.1% of the time. After testing both models with cvec and tfidf vectorization I determined that tfidf vectorization performed the best. I also chose tfidf because it weighs unique words more heavily. 

#### Multinomial Naive Bayes Model Results

The multinomial Naive Bayes model had a training accuracy score of 97% and a testing accuracy score of 78%. Overall the model performed well but was also overfit. 

#### RandomForestClassifier Model Results

After testing over 5,000 different models I found the best RandomForestClassifier model had a training accuracy score of 73% and a testing accuracy score of 72%. This model was far less overfit than the multinomial Naive Bayes model. For this reason, I decided to continue analysis with the RandomForestClassifier model. The model uses the following parameters:

* max depth = 10
* estimators = 200

Overall my model was a major improvement over the base model. My RandomForestClassifier had an accuracy score of over 20% higher than the base-line model.

---

### Recommendations

Now that an accurate model had been created I looked at the feature importance of each word in the dataset. Looking at the feature importance would allow me to see the distinguishing features between Nascar and Formula 1 and allow Formula 1 to better market to Nascar Fans. 

Looking at the top 15 most important features one specific word seemed especially important. As shown in the bar chart below 'Daytona' was the 6th most import word in determining subreddit. 

![Top 15 Feature Important Words](https://git.generalassemb.ly/albertfrantz/Submissions/blob/master/projects/project_3-master/Images/top_15.PNG)

'Daytona' references the Daytona 500 in Florida. Given that Nascar viewers identify more strongly with the Daytona 500 over any other race it may be in formula 1’s best interest to begin marketing themselves at the Daytona 500 or even begin a new race, in Florida. There are current plans to begin a new Grand Prix in Florida in 2022, so this analysis confirms that this is likely a great strategy and could convert many Nascar fans to Formula 1. 

I next looked at Nascar manufacturers to see what company Formula 1 should try and recruit. Once again by looking at feature importance we can see that Ford is who Nascar viewers identify with most. Formula 1 may want to incentivize Ford to come to formula 1. In bringing ford to formula 1 perhaps loyal Nascar fans would follow suit. Ford also has the benefit of previously working with many Formula 1 teams building engines in the early 2000s. In converting Nascar fans to formula 1 we should focus on creating a new ford team over creating a new Chevrolet or Toyota team. 

![Nascar Manufacturer Feature Importance](https://git.generalassemb.ly/albertfrantz/Submissions/blob/master/projects/project_3-master/Images/manu_imp.PNG)

Finally, I looked at the Nascar sponsorships. Nascar also tends to attract specific advertisements that connect with fans. Fans seem to especially notice the brands: Monster, Sprint, Fox, and Xfinity. Given these brands' connections to Nascar, it may be worthwhile continuing with further research to see how these brands market themselves to Nascar viewers. In understanding their brand strategy perhaps Formula 1 can adapt some of their methods and attract Nascar fans to formula 1 by similar methods. 

![Nascar Sponsor Feature Importance](https://git.generalassemb.ly/albertfrantz/Submissions/blob/master/projects/project_3-master/Images/sponsor_imp.PNG)

In following these three recommendations I believe Formula 1 can increase international viewership. 