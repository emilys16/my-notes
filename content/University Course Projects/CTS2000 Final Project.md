---
title: CTS*2000 Final Project - Python Exercise 3 Upgrade
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
upo_flairs = []

#For every submission in top posts (max 500 posts)
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
    # Submission flair tag
    upo_flairs.append(submission.author_flair_text)


upo_dataframe = pandas.DataFrame({'Title': upo_title, 'Content': upo_content, 'Sentiment': upo_sentiment, 'Score': upo_score,'Upvote Ratio': upo_upvote, 'Flair':upo_flairs})
pandas.set_option("display.max_rows", None)
upo_dataframe.head(500)
```

## Step 3: Organize the DataFrame by the Score column 
```python
# Import re and pandas libraries
import re
import pandas 

# Print organzied values based on score
sorted_upo_dataframe = upo_dataframe.sort_values(by='Score', ascending=False)
pandas.set_option("display.max_rows", None)
sorted_upo_dataframe.head(500)
```

## Step 4: Investigating Prevalent Themes Using NLTK
 First I will find the frequency distribution of the word lemmas in the subreddit posts and use the post common tag. From the most common tag I will check the list of words tagged and compare that with the word frequency. 

Since the most common tag is NN (proper noun), below is printing the words that go with the NN tag. It is clear that the words Movie, Christmas, and People are common themes right now in the subreddit (at the time of coding this). 

To better visualize the the most prevalent themes on the subreddit, I created a pie chart to display the 15 most common themes. 
```python
# Importing NLTK libraries 
import pandas as pd
import nltk
from nltk.tokenize import word_tokenize
from nltk.tag import pos_tag
from nltk.stem import WordNetLemmatizer
from collections import Counter

# Install NLTK libraries
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
nltk.download('stopwords')
nltk.download('wordnet')
```

```python
# Initialize an instance of the lemmatizer
lemma = WordNetLemmatizer()

# Sort the DataFrame by Title
sorted_upo_dataframe = upo_dataframe.sort_values(by='Title', ascending=False)

# Initialize an empty list to store all proper nouns
all_proper_nouns = []

# Iterate over each title in the DataFrame
for upo_title in sorted_upo_dataframe['Title']:
    # Tokenize the title into words
    words = word_tokenize(upo_title)

    # An empty list that will store the lemmatized version of the list
    upo_lemma = []

    # For every word in the subreddit post title:
    for word in words:
        # Append the lemmatized version of that word to the list:
        upo_lemma.append(lemma.lemmatize(word))

    # Tag every word in the corpus
    upo_tags = pos_tag(upo_lemma)

    # For every tag in the upo_tags list:
    for word, tag in upo_tags:
        # If the tag contains 'NN'
        if "NN" in tag:
            # Append it to the proper_noun_list
            all_proper_nouns.append(word)

# Print the most common tags
upo_tag_fd = nltk.FreqDist(tag for (word, tag) in upo_tags)
print("Most common tags:", upo_tag_fd.most_common())

# Print top 50 of the proper nouns        
print("Top 20 proper nouns:", all_proper_nouns[:50])

# Count unique proper nouns
word_counter = Counter(all_proper_nouns)
unique_words = len(word_counter)

print(f"The number of unique proper nouns is {unique_words}. \n")

# Print the most common proper nouns
print("Most common proper nouns:", word_counter.most_common(50))
```

```python
import matplotlib.pyplot as plt

# Get the most common proper nouns and their counts
most_common_nouns = word_counter.most_common(15)

# Create a DataFrame from the most common nouns
common_nouns_df = pd.DataFrame(most_common_nouns, columns=['Word', 'Count'])

# Plotting the pie chart
plt.figure(figsize=(10, 7))
plt.pie(common_nouns_df['Count'], labels=common_nouns_df['Word'], autopct='%1.1f%%', startangle=140)
plt.title('Distribution of Most Common Proper Nouns')
plt.axis('equal')
plt.show()
```

## Questions: Reddit API Findings 
#### Based on your initial findings, which posts generate the most response from users - positive, negative, or neutral posts?

Based on my initial findings, posts with a positive sentiment score generate the most responses from users. This is shown by sorting based on the submissions sentiment and score. 

#### What can you infer about the general tone and atmosphere of this subreddit? Is the community more supportive, critical, humorous, or argumentative? Use both overall trends and specific examples (i.e. quotes from the posts) to support your analysis.

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

#### Compare the results to a different subreddit (e.g. r/AmItheAsshole vs. r/mildlyinteresting or r/politics vs. r/conspiracy) How do the type of posts and user interactions differ? Do the results align with your expectations, why or why not?

Comparing the results of Unpopular Opinion and Am I The Asshole subreddits that type of posts and user interactions are quite different. *Unpopular Opinion* comment sections are debating the unpopular opinion, while *Am I The Asshole* comment sectons are giving advice or justificatoin for a yes or no answer to the submissions question. The results align with my expectations because of the type of post structure and community norms are different. Each subreddit has a different purpose. 

#### What further questions would you like to investigate? How might you continue to refine and enhance your code in order to expand upon your study?

I would like to investigate what themes are most prevalent and how the framing of the opinion impacts the responses received. 

To enhance and refine my code I would add a column for the authors flair. By adding this attribute I will be able to analyze the autHors writing style and what themes they like most. By using "author_flair_text" I can gain useful data about the authors perspective and role in the subreddit community. 
___
# Final Project Reflection

## Problems, Objectives, and Methods
### Change 1 - Max Rows
The first change I made to this exercise was the the layout of the DataFrame. The DataFrame had a "..." in the middle to separate the top rows and bottom rows while omitting the middle information collected. I implemented display settings as mentioned in Week 7's Jupyter Notebook "Pandas-Continued." This will allow me to see all the data I need to work with.  I added `pandas.set_option("display.max_rows", None)` to each code block in steps 2 and 3 that displayed a DataFrame.
##### **Results:**
By switching to a larger view of the DataFrame it made it easier to access each post that was scrapped from the subreddit. 
### Change 2 - Flairs
The second change was adding flairs. Using the reflection response from the initial project submission, I said that to enhance and refine my code, I wanted to add flairs to gain useful information about the author's role in the subreddit community.  I did this by adding `upo_flairs` to the step 2 submission dictionary lists and adding it to the for loop to add a flairs column to the DataFrame.
##### **Results:**
Before doing this assignment, I did not know much about a flair. I now know that User flair on Reddit is used to create a visual flag next to community members' names to highlight the user's areas of knowledge. When using the PRAW function, I did not expect to get the contributor's username; I thought it meant more about the genre or themes they know most. Now I know they signify more who a moderator is to support community guidelines. The User Flairs on the unpopularopinion subreddit are water yummi, adhd kid, waterholic, and snoo_thoughtful.
### Change 3 - Frequency Distribution, Data Visualization
Using the reflection response from the initial project, when asked what further I would do to investigate, refine, and enhance my code, I said that I wanted to examine what themes were most prevalent. To do this, I researched further to build off Week 8's Jupyter Notebook on NLTK and Spacey. I created a step 4 to the assignment to display the code and results from this investigation. I found the most common themes by finding the most frequent words and frequency distribution from the top 50 hot subreddit posts from unpopularopinion. Furthermore, to demonstrate the themes, I created a pie chart as taught in Week 6's Jupyter Notebook "Pandas Intro."
##### **Results:**
By collecting the individual words from the subreddit post titles, I was able to find the most prevalent themes by cross-referencing the most frequent words. At the time of creating this code, the major themes on the subreddit were Movies, Christmas, People, and Games.
## Reflection
Through this process, I learned that there is no specific way that something is coded, as I had many different iterations of my code. I learned that I can always add more to the project and ways to improve. When I first started the final project, I was unsure what I wanted to change, but once I started adding to the subreddit analysis, especially when working more with NLTK, I knew I wanted to add more to contextualize the themes of the subreddit. In this process, I learned to utilize skills from all lectures to improve my code. I used concepts from Week 6's intro to pandas, Week 7's pandas continued, Week 8's NLTK and Spacey, Week 9's API setup, and Week 10's Reddit Mining. 

Though I added flairs to the dataset, I could still explore how they could impact the analysis. For example, I could have conducted a deeper analysis to see if posts by certain flairs (such as moderators or frequent contributors) received more engagement (upvotes, comments). The flairs could also be used to segment the data and investigate how specific groups contribute to the overall sentiment of the subreddit. To continue to develop the project in the future, I could also expand the analysis to examine how different post characteristics (e.g., flair, title length, specific words) correlate with post engagement metrics (e.g., upvotes, comments). This could help answer questions about what kinds of posts are most likely to generate strong reactions or spark controversy.
___
## Works Cited
Athari. “Nltk in Python to Extract Information from Web Page.” _Stack Overflow_, 21 Feb. 2014, stackoverflow.com/questions/21930346/nltk-in-python-to-extract-information-from-web-page.

Mondaut, Jonathan. “Extracting Main Keywords from Web Scraped Text with BeautifulSoup, Pandas, and NLTK in Python.” _Medium_, 27 Mar. 2023, medium.com/@jonathanmondaut/extracting-main-keywords-from-web-scraped-text-with-beautifulsoup-pandas-and-nltk-in-python-2a54a89caec2. Accessed 8 Dec. 2024.

“Submission - PRAW 7.7.1 Documentation.” _Praw.readthedocs.io_, praw.readthedocs.io/en/stable/code_overview/models/submission.html.

“User Flair - Reddit Help.” _Reddit Help_, 18 Oct. 2024, support.reddithelp.com/hc/en-us/articles/15484503095060-User-Flair.
