# ANLY502 - Massive Data Analytics<br>Big Data Project

## Introduction

In this project, I work with a pretty large dataset of JSON data (~500GB) using the tools we've learned in class. The data set is about the reddit achieve. And in this project, I filtered the data and concentrated only on the jewelry subreddit. Since the text for different subject would have extremely different words and content. Concentrating on only one subreddit will reduce the complexity of the model and make both predictive modeling and topic modeling easier and produce higher accuracy.   
  
First, let us explore the data set:   

| type        | name           | description  |
| ------------- |:-------------:| -----:|
| String    | id | this item's identifier, e.g. "8xwlg" |
| String      | name      |  Fullname of comment, e.g. "t1_c3v7f8u" |
| String | kind      |    All things have a kind. The kind is a String identifier that denotes the object's type. Some examples: Listing, more, t1, t2 |
| String | author     |    the account name of the poster |
| String | author_flair_css_class     |   the CSS class of the author's flair. subreddit specific |
| String | author_flair_text      |    the text of the author's flair. subreddit specific |
| String | banned_by      |    who removed this comment. null if nobody or you are not a mod |
| String | link_author     |   present if the comment is being displayed outside its thread (user pages, /r/subreddit/comments/.json, etc.). Contains the author of the parent link |
| String | link_id      |   ID of the link this comment is in |
| int | score     |   the net-score of the link. note: A submission's score is simply the number of upvotes minus the number of downvotes. If five users like the submission and three users don't it will have a score of 2. Please note that the vote numbers are not "real" numbers, they have been "fuzzed" to prevent spam bots etc. So taking the above example, if five users upvoted the submission, and three users downvote it, the upvote/downvote numbers may say 23 upvotes and 21 downvotes, or 12 upvotes, and 10 downvotes. The points score is correct, but the vote totals are "fuzzed". |
| boolean | score_hidden     |   Whether the comment's score is currently hidden. |
| String | subreddit     |   subreddit of thing excluding the /r/ prefix. "pics" |
| String | subreddit_id     |   the id of the subreddit in which the thing is located |
| String | distinguished     |   to allow determining whether they have been distinguished by moderators/admins. null = not distinguished. moderator = the green [M]. admin = the red [A]. special = various other special distinguishes http://redd.it/19ak1b |
| long | created_utc     |   the time of creation in UTC epoch-second format. Note that neither of these ever have a non-zero fraction. |
| boolean | score_hidden     |   Whether the comment's score is currently hidden. |

```
root
 |-- archived: boolean (nullable = true)     
 |-- author: string (nullable = true)     
 |-- author_cakeday: boolean (nullable = true)     
 |-- author_created_utc: long (nullable = true)     
 |-- author_flair_background_color: string (nullable = true)     
 |-- author_flair_css_class: string (nullable = true)     
 |-- author_flair_richtext: array (nullable = true)     
 |    |-- element: struct (containsNull = true)     
 |    |    |-- a: string (nullable = true)     
 |    |    |-- e: string (nullable = true)     
 |    |    |-- t: string (nullable = true)     
 |    |    |-- u: string (nullable = true)     
 |-- author_flair_template_id: string (nullable = true)     
 |-- author_flair_text: string (nullable = true)     
 |-- author_flair_text_color: string (nullable = true)     
 |-- author_flair_type: string (nullable = true)     
 |-- author_fullname: string (nullable = true)     
 |-- author_patreon_flair: boolean (nullable = true)     
 |-- body: string (nullable = true)     
 |-- can_gild: boolean (nullable = true)     
 |-- can_mod_post: boolean (nullable = true)     
 |-- collapsed: boolean (nullable = true)     
 |-- collapsed_reason: string (nullable = true)     
 |-- controversiality: long (nullable = true)     
 |-- created_utc: long (nullable = true)     
 |-- distinguished: string (nullable = true)     
 |-- edited: string (nullable = true)     
 |-- gilded: long (nullable = true)     
 |-- gildings: struct (nullable = true)     
 |    |-- gid_1: long (nullable = true)     
 |    |-- gid_2: long (nullable = true)     
 |    |-- gid_3: long (nullable = true)     
 |-- id: string (nullable = true)     
 |-- is_submitter: boolean (nullable = true)     
 |-- link_id: string (nullable = true)     
 |-- no_follow: boolean (nullable = true)     
 |-- parent_id: string (nullable = true)     
 |-- permalink: string (nullable = true)     
 |-- removal_reason: string (nullable = true)     
 |-- retrieved_on: long (nullable = true)     
 |-- score: long (nullable = true)     
 |-- send_replies: boolean (nullable = true)     
 |-- stickied: boolean (nullable = true)     
 |-- subreddit: string (nullable = true)     
 |-- subreddit_id: string (nullable = true)     
 |-- subreddit_name_prefixed: string (nullable = true)     
 |-- subreddit_type: string (nullable = true)     
```

####There are in total 476259744 entries of data.    

## Code
All the code are in the Mini Project.ipynb file.

## Methods section:
Subset of the data: jewelry subreddit subset.     
     
**Tools used for analyzing:     ** 
1. **Explore Analysis:**, boxplot, calculate the math statistics and create summary table.       
2. **Sentiment Analysis:**, calcualte the sentiment score (range from -1 to 1 for which -1 means most negative and 1 means most positive)     
3. **Natural Language Processing:** word count. Count the occurency of each word, plot the distribution of the mostly used words.     
4. **Predictive modeling:** utilize logistic regression model to predict the score using sentiment score, no_follow, send_replies and stickied.     
5. **Topic modeling:** use body text and tokenize to fit in LDA modeling to indentify the cluster of the text in the jewelry subreddit.     

### Cleaned, prepared the dataset:

|summary|         body|             score|subreddit|
| ------------- |:-------------:| -----:|-----:|
|  count|    476259744|         476259744|476259744|
|   mean|          NaN| 9.162615413071737| Infinity|
| stddev|          NaN|137.10764547617944|      NaN|
|    min|             |            -22280|  0010110|
|    max|󾓪󾓪❤💜💙󾓪󾓪|             90192|    zzzzz|

Check the subreddit column:

|          subreddit|  count|
| ------------- |:-------------:|
|     TrueOffMyChest| 165117|
|              anime|1062856|
|    youtubecomments|    416|
|             travel| 120783|
|         mistyfront|  18853|
|  BeautyGuruChatter| 148001|
|        SeriousFIFA|   7594|
|            ukraina|  16353|
|theendoftheworldrpg|     10|
|          machinist|     31|
|          bookshelf|   3632|
|          kitchener|   9744|
|UnresolvedMysteries| 166471|
|        creepypasta|   9059|
|       WorldBitBank|    652|
|         MensRights| 162145|
|           Warcraft|    454|
|       couchsurfing|   2335|
|          left4dead|    500|
|          upcycling|   1578|

The data with 476259744 entries has data for multiple subreddit, different subreddit would have very different content and doing text analysis between different subreddit would bring inconsistency and bias. Therefore, I would like to only focus on one subreddit. From the subreddit column, we can chose different subreddit to conduct the analysis. In this project, I only consider the data in jewelry subreddit group to focus on one topic when doing analysis, predictive modeling and topic modeling.   

Here is the summary of the filtered dataset: 

|summary|                body|             score|
| ------------- |:-------------:| -----:|
|  count|                6543|              6543|
|   mean|              1001.0|2.5324774568240866|
| stddev|   1400.071426749364| 3.152712761917903|
|    min|
You admit a 300%...|               -15|
|    max|                  😄|                53|

To Further clean the data, we would consider how to deal with null values. In different models I dealed with null values in different ways. For predictive model which use logistic regression to predict the socre, I drop all the null value rows to fit the model. And for topic modeling and sentiment analysis, I ignore the null values. Since if the body text is null for an entry, the sentiment score would be calculate as 0 which is neutral sentiment. In addition, for the topic modeling section, I also drop the null values to eliminate the weight for null value entries and to generate better results.

### Visualize the dataset    
I create three plot for the data:       
         
1.**Boxplot of the score:** the first plot is the distribution boxplot of the score that users give. From the boxplot, the mean is 2.5324774568240866 median is 2 max is 53 and min is -15. The distribution of negative score are more sparse than the distribution of positive scores. Therefore, in the following predictive modeling section. I choose the bin to be the median to create balanced classes for prediction. 
     
2.**Boxplot of sentiment score:** the sentiment score boxplot is the distribution of a collective sentiments that I get from body text. From the plot, we can get that most text have sentiment socre greater than 0 the mean is around 0.3.
     
3.**Word Count Plot:** this plot gives the distribution of the most frequent word and the occurrence of each:    
[('like', 1357), ('would', 1289), ('ring', 1169), ('get', 919), ('gold', 829), ('one', 683), ('stone', 622), ('look', 611), ('make', 595), ('good', 588), ('could', 563), ('jewelry', 557), ('want', 548), ('jeweler', 547), ('know', 523), ('much', 510), ('something', 509), ('really', 504), ('also', 499), ('think', 496), ('go', 496), ('see', 474), ('find', 465), ('stones', 413), ('might', 405), ('going', 397), ('silver', 378), ('probably', 375), ('wear', 365), ('work', 363), ('diamond', 355), ('price', 355), ('thank', 354), ('even', 348), ('take', 346), ('made', 345), ('looking', 339), ('lot', 334), ('looks', 327), ('sure', 327), ('need', 327), ('rings', 326), ('buy', 299), ('pretty', 297), ('chain', 294), ('diamonds', 282), ('people', 282), ('cut', 281), ('white', 278), ('custom', 264)]    

From the matrix, like, ring, gold, stone, jewelry price diamonds are all words that occurs most frequently. This confirms our subreddit group and also gives us a sense of what kind of topic are most concerned by users.    
     
          
### Modele the dataset    
1.**Predictive Modeling:** I utilize logistic regression model to predict the score using sentiment score, no_follow, send_replies and stickied.       
         
          
**Logistic regression**: is the appropriate regression analysis to conduct when the dependent variable is dichotomous (binary).  Like all regression analyses, the logistic regression is a predictive analysis.  Logistic regression is used to describe data and to explain the relationship between one dependent binary variable and one or more nominal, ordinal, interval or ratio-level independent variables.     
The model include:   
 |-- body: string (nullable = true)
 |-- no_follow: boolean (nullable = true)
 |-- score: double (nullable = true)
 |-- send_replies: boolean (nullable = true)
 |-- stickied: boolean (nullable = true)
 |-- senti: double (nullable = true)
 
The predictive accuracy is 0.6803125591954718, and from the roc curve, the result is not satisfying. There are several potential reasons that account for the high error rate. For example: the data set is not large enough, the feature used in nor correlated, the model should include more features in the model, logistic regression is not a good model to fit the data.     
     
          
2.**Topic Modeling:** is a type of statistical modeling for discovering the abstract “topics” that occur in a collection of documents. Latent Dirichlet Allocation (LDA) is an example of topic model and is used to classify text in a document to a particular topic. It builds a topic per document model and words per topic model, modeled as Dirichlet distributions.In my model, I set the cluster size to be 3 and the number of word topic returen to be 5.     
The result retured from the topic model:    
topic:  0
['would', 'like', 'ring', 'jeweler', 'going']

topic:  1
['ring', 'silver', 'gold', 'like', 'would']

topic:  2
['stone', 'look', 'like', 'stones', 'would']

From the result, we can conclude: there are topics including jeweler-ring: which may discuss the ring in general, ring-silver-gold: which may discuss whether to buy silver ring or gold ring, stone-stones: which may discuss the jeweler with stone. In general the topice modeling did a great job in greate different cluster for the text.     


### Correaltion analysis:
I calculate the correlation between socre and sentiment score:  0.06128591083584731.   
The result indicate there are no correlation between sentiment score we generated from the body text and the score. Which could also explain why the predictive model does not have a satisfy result for prediction.      

### Future Work:     
1. Improve the accuracy of the predictive model: to include more features, use other predictive models.    
2. Do topic modeling for more clusters and return more topic words.   
3. Do the analysis for different subreddit group
 
