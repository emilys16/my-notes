---
title: ★ Data Mining with Reddit API - Python Exercise 3
draft: false
tags:
  - CTS2000
---
---
## Step 1: Choose a Reddit subreddit
```python
# Installing PRAW library
%pip install praw

import praw 

# Importing Reddit API credentials
reddit = praw.Reddit(client_id='ZUcLjBrHNZdgv6Cr_R-JBg',
                     client_secret='GglbjUOsuQbO2fTB79BFoaHhHo1H6w', 
                     password='MartyTheCat1',
                     user_agent='2024_CTS_Analysis', 
                     username='16ylime')

# Test credentials to use for unpopularopinion subreddit
print(reddit.user.me())
```

```python
# Loading posts from "Unpopular Opinion" into a DataFrame
upo_subreddit = reddit.subreddit('unpopularopinion')

# Stores the hot posts in UPO
upo_hot = upo_subreddit.hot(limit=500) 
```

## Step 2: Load a collection of at least 500 reddit posts into a DataFrame
```python
# Installing Vader Sentiment Analysis 
%pip install vaderSentiment
import vaderSentiment.vaderSentiment
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer

# Create an instance of the sentiment analyzer
sentimentAnalyser = SentimentIntensityAnalyzer()
```

```python
# Import re and pandas libraries
import re
import pandas 

# Pull submissions from subreddit 
upo_subreddit = reddit.subreddit('unpopularopinion')

# Submission dictionary lists
upo_title = []
upo_content = []
upo_sentiment = []
upo_score = []
upo_upvote = []

#For every submission in top posts (max 200 posts)
for submission in upo_subreddit.hot(limit=500):
    # Submission Title
    upo_title.append(submission.title)
    # Submission content
    upo_content.append(submission.selftext)
    # Submission sentiment score
    sentiment_scores = sentimentAnalyser.polarity_scores(submission.selftext) # Analyze sentiment of the content
    upo_sentiment.append(sentiment_scores['compound']) # Store the compound score
    # Net Score (up votes - down votes)
    upo_score.append(submission.score)
    # Percentage of total votes that are upvotes
    upo_upvote.append(submission.upvote_ratio)

upo_dataframe = pandas.DataFrame({'Title': upo_title, 'Content': upo_content, 'Sentiment': upo_sentiment, 'Score': upo_score,'Upvote Ratio': upo_upvote})
upo_dataframe.head(500)
```

## Step 3: Organize the DataFrame by the Score column 
```python
# Import re and pandas libraries
import re
import pandas 

# Print organzied values based on sentiment score
sorted_upo_dataframe = upo_dataframe.sort_values(by='Score', ascending=False)
sorted_upo_dataframe.head(500)
```

## Questions: Reddit API Findings 

### Based on your initial findings, which posts generate the most response from users - positive, negative, or neutral posts?

Based on my initial findings, posts with a positive sentiment score generate the most reponses from users. This is shown by sorting based on the submissions sentiment and score. 

### What can you infer about the general tone and atmosphere of this subreddit? Is the community more supportive, critical, humorous, or argumentative? Use both overall trends and specific examples (i.e. quotes from the posts) to support your analysis.

The subreddit is designed to share controversial opinions which can lead to debates and disagreements in the comments, but generally the community is respectful and able to see a variety of points of view. A good example is the comment, "Both are suited for different things. If you want the actual chicken taste the traditional wings are better. If you prefer the breaded taste the boneless ones are better" posted by UsedandAbused87. In the code below you can see that majority of the scores for the comments are positive. 
```python
submission_list = []
comment_list = []

import re
import pandas 

upo_subreddit = reddit.subreddit('unpopularopinion')

submission.comments.replace_more(limit=0)  # Ensure we fetch all comments and avoid "load more" instances
comments = submission.comments.list()

for comment in comments[:11]:
            try:
                # Skip comments containing "Welcome to" or FAQ
                if "Welcome to" not in comment.body and "FAQ" not in comment.body:
                    comment_list.append(comment.body)
                    print("------------------COMMENT--------------------")
                    print(f"Author: {comment.author}")
                    print(f"Score: {comment.score}")
                    print(comment.body)
            except AttributeError:
                # Some comments may not have a body or could be None
                print("Skipping a comment without a body.")
```

### Compare the results to a different subreddit (e.g. r/AmItheAsshole vs. r/mildlyinteresting or r/politics vs. r/conspiracy) How do the type of posts and user interactions differ? Do the results align with your expectations, why or why not?

Comparing the results of Unpopular Opinion and Am I The Asshole subreddits that type of posts and user interactions are quite different. *Unpopular Opinion* comment sections are debating the unpopular opinion, while *Am I The Asshole* comment sectons are giving advice or justificatoin for a yes or no answer to the submissions question. The results align with my expectations because of the type of post structure and community norms are different. Each subreddit has a different purpose. 

### What further questions would you like to investigate? How might you continue to refine and enhance your code in order to expand upon your study?

I would like to investigate what themes are most prevalent and how the framing of the opinion impacts the repsonses recieved. 

To enhance and refine my code I would add a column for the authors flair. By adding this attribute I will be able to analyze the autors writing style and what themes they like most. By using "author_flair_text" I can gain useful data about the authors perspective and role in the subreddit community. 
 
