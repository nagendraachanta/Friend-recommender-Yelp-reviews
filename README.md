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
