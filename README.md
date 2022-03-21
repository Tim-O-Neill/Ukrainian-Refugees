#  Refugee Financial Impact on Asylum Countries
---

By looking at the costs of refugee crises, current and historical around the world, and estimating the number of people impacted by the conflict in Ukraine, can we project the estimated financial impact to those asylum countries of the refugee crisis in Ukraine?

### Authors:

Jason Meyers, Tim O'Neill, Ben Roberts, Tori Powers

## Table of Contents:

- Part 1: Executive Summary
- Part 2: Data Dictionary
- Part 3: Conclusion

## Part 1: Executive Summary
---
Since the pandemic began in 2020, our homes have become a sacred space more than ever before, especially with many working from home. And with many business turning toward the remote model as permanent, home offices and more space has become even more necessary. Combine that with historically low interest rates and the housing market has been a wild ride for homebuyers, new and experienced. Which leads to the dilemma that many may be facing, how to afford making their home a place they want to spend more time, whether that be through home renovations or purchasing a new home. There are many options out there for financing, but if someone is new to the process, it can feel overwhelming. So how can someone determine the correct type of financing? 

In order to know what a homeowner, or hopeful homeowner requires, two subreddits were looked at to compare language that is typically used for those interested in Home Improvement (r/HomeImprovement) and Real Estate (r/realestateinvesting). It is important to note that real estate investing does not solely focus on investment properties and includes various lending conversations. Approximately 2,000 posts per subreddit were pulled using Pushshift Reddit API.  Data collected included author, title, selftext, and time of the post.  Data was parsed and placed in a dataframe where it was then cleaned. Due to missing data from selftext, some rows were deleted that accounted for less than 0.5% of all of the data. Title and selftext were combined to analyze all of the subreddit posts and then lemmatized, rather than stemmed, in order to return valid words. Multiple classification models were fit, looking for the highest accuracy with the lowest false negatives and false positives. 

Models that were analyzed during this project include:

- [Logistic Regression](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/code/03_Models/03_Modeling_Logistic_Combo.ipynb)
- [AdaBoost Classifier](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/code/03_Models/03_Modeling_Boosting_Combo.ipynb)
- [Gradient Boosting Classifier](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/code/03_Models/03_Modeling_Boosting_Combo.ipynb)
- [Random Forest Classififer ](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/code/03_Models/03_Modeling_RandomForest_Combo.ipynb)

Each model's hyperparameters were tuned using either GridSearchCV or RandomizedSearchCV until the best fit was determined. [Logistic Regression](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/code/03_Models/03_Modeling_Logistic_Combo.ipynb) returned the best model with an accuracy score of 94.4%.  These results were well above the baseline of 50%. 

The flow of this project can be followed by reading into the following notebooks:

01: Data Cleaning
02: Initial EDA
03: Final Data Prep
04: Additional EDA
05: Models

## Part 2: Data Dictionary
---
Datasets used/created:

- [reddit_data_20220227-132529.csv](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/data/reddit_data_20220227-132529.csv): 
- [data_clean_20220227-141901.csv](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/data/data_clean_20220227-141901.csv):
- [data_clean_20220302-090710.csv](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/data/data_clean_20220302-090710.csv):
- [data_clean_combo_20220302-111425.csv](https://git.generalassemb.ly/powersjv/project_3/blob/3c22007a7d056a9b89e779dcea1dc88d32454d40/data/data_clean_combo_20220302-111425.csv): 

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**author**|*object*|data_clean_combo_20220302-111425.csv|Posting author's username.| 
|**title**|*object*|data_clean_combo_20220302-111425.csv|Title of posting.|
|**selftext**|*object*|data_clean_combo_20220302-111425.csv|Body of posting.|
|**createdutc**|*integer*|data_clean_combo_20220302-111425.csv|Time of posting in Unix Epoch.|
|**title_selftext**|*object*|data_clean_combo_20220302-111425.csv|Title and Selftext combined.|
|**title_text_length**|*integer*|data_clean_combo_20220302-111425.csv|The charcter length of the title and selftext combined.|
|**title_text_word_count**|*integer*|data_clean_combo_20220302-111425.csv|The word count of the title and selftext combined.|
|**subreddit_target**|*integer*|data_clean_combo_20220302-111425.csv|Binarized Target: 0: r/HomeImprovement, 1: r/realestateinvesting.|


## Part 3: Conclusion
---
This project's focus was to accurately identify which subreddit a posting belonged to, either r/HomeImprovement or r/realestateinvesting. This was acheived using a Logistic Regression model that produced an accuracy score of 94.4%. There can still be room for improvement by looking at those postings that were not accurately placed and determining why they were misplaced. Looking at the common words in each subreddit, there was some overlap, therefore removing those words may create an even better model to predict the approporiate subreddit. 

The implications of this project can be used in order to help determine the appropriate type of financing that is needed. An improved version of this model could be utilized on banking websites for customers to type in their situation and be directed to the appropriate office within the institution, personal loans or home mortgages. 

