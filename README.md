# Friend-recommender-Yelp-reviews

**Methodology**
A simple overview of our recommendation system is that it will take in text input of an existing
user ID and output 5 people to meetup with. To create this, we will try out a couple different
approaches which are outlined below.


**Matrix-Based approach**
As a baseline, we first explored similarities between users using principal component analysis
and clustering. Since we also have text data for the reviews, we also tried expanding on our
approach by using natural language processing.


**Similarity by category breakdown**
For this method, we classified and clustered the user database based on the categories of
businesses the users highly rated in reviews. Each step of the process is expanded upon below.



**Data pre-processing**
In addition to the data cleaning performed to the raw data, there were some extra filtering
conditions we implemented to combat the size of the dataset. Since the analysis is at the level
of the user, even after the initial cleaning, we still had 158,745 total users. Thus, we limited
analysis to only users with more than 150 reviews which brought our total users down to 49,607.
To prepare for the creation of the matrix, we grouped the reviews by user_id and then merged
the categories of all the businesses that user reviewed into one large list of categories. In the
context of our analysis, this represented the interests of the users.


**Similarity by keywords used in written reviews**
Text preprocessing
For this part of our project, we need the dataset with all user information and their
corresponding reviews across different businesses. We have the dataset filtered out with all the
positive ratings; file named ‘reviews’ with features ‘user_id’, ‘business_id’, ‘text(review)’, ‘useful’
etc. We limited the data size by filtering out useful factor for reviews > 0.0 and include only
users with review count >100. These steps draw down our entire data for this task to just 1000
users and around 150,000 data points (multiple rows/ reviews for a given user).
We further processed the user reviews using the following NLP functions in nltk module:
● Stop words removed using the predefined words dataset in English
● Text processed using Lemmatizer to remove text extensions
● Removed repetitive words in a given user review
● Parts of speech tagging (POS) to include only ‘Nouns’ and ‘Adjectives’



**Build vectorized matrix**
We separated this task in two ways by characterizing the keywords containing food items and
keywords from overall review.
Vectorizing Food items mentioned(bag of words):
Bag-of-words approach, as what it indicates in the name, assumes all the words are hold
in bags where the order of words is ignored. We concatenated all the reviews given by each
user in the dataset and each user’s review set is parsed to filter only food names using the food
dataset available in nltk.corpus module. We used count vectorizer in sklearn.feature_extraction
to generate a matrix with users and frequency of food items used in their reviews. The final
matrix of dimensions (985,576) was generated for this task.

**Vectorizing keywords from entire review:**
We count the frequency of each word 𝑤𝑖 occurring in one document 𝑑𝑗. Then adopt 𝑐𝑖,𝑗 to denote
this value. A more advanced representation is called 2-gram, which partly overcomes the
shortage of disregarding orders. A 2-gram term is a contiguous sequence of n items. i.e., for a
sentence ‘This is nice.’, the collection of 2-gram terms is ‘this is’ and ‘is nice’. This partition utilizes
the context information and captures more textual structure from raw data. However, the cost is
the increment of the number of features which is not good for prediction. With comparable
advantages for both methods, we have implemented both frequency count and 2-gram and tested
an analysis which works better in terms of prediction accuracy.

**Create user groupings**
With the resulting sparse matrix, we normalized the data and performed PCA to get a reduced
dimension version of the data (n_components=3). To determine the optimal number of
dimensions to reduce to, we looked at the percent of variance explained and picked the number
that explained more than 90%. Once we got the reduced data, we were able to proceed with kmeans
clustering. Finally, to determine the ideal number of clusters, we used the elbow method
and 15 clusters were recommended.
