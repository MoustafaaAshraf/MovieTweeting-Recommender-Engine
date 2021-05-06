# Movietweeting, Movie Recommendation Engine
Movie Recommender Engine using data collected from Twitter

<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#Some-stats" data-toc-modified-id="Some-stats-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Some stats</a></span></li><li><span><a href="#A-Movie-Rating-Dataset-Collected-From-Twitter" data-toc-modified-id="A-Movie-Rating-Dataset-Collected-From-Twitter-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>A Movie Rating Dataset Collected From Twitter</a></span></li><li><span><a href="#Ratings-from-Twitter" data-toc-modified-id="Ratings-from-Twitter-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>Ratings from Twitter</a></span></li><li><span><a href="#Data-Preparation" data-toc-modified-id="Data-Preparation-4"><span class="toc-item-num">4&nbsp;&nbsp;</span>Data Preparation</a></span></li><li><span><a href="#The-Recommender-Engine" data-toc-modified-id="The-Recommender-Engine-5"><span class="toc-item-num">5&nbsp;&nbsp;</span>The Recommender Engine</a></span><ul class="toc-item"><li><span><a href="#Knowledge-Based-Recommendations" data-toc-modified-id="Knowledge-Based-Recommendations-5.1"><span class="toc-item-num">5.1&nbsp;&nbsp;</span>Knowledge-Based Recommendations</a></span><ul class="toc-item"><li><span><a href="#Part-I:-How-To-Find-The-Most-Popular-Movies" data-toc-modified-id="Part-I:-How-To-Find-The-Most-Popular-Movies-5.1.1"><span class="toc-item-num">5.1.1&nbsp;&nbsp;</span>Part I: How To Find The Most Popular Movies</a></span></li><li><span><a href="#Part-II:-Adding-Filters" data-toc-modified-id="Part-II:-Adding-Filters-5.1.2"><span class="toc-item-num">5.1.2&nbsp;&nbsp;</span>Part II: Adding Filters</a></span></li></ul></li></ul></li></ul></div>


## Some stats

- Total number of ratings: 	902,957
- Number of unique users: 	70,483
- Number of unique items: 	37,191

## A Movie Rating Dataset Collected From Twitter

MovieTweetings is a dataset consisting of ratings on movies that were contained in well-structured tweets on Twitter. This dataset is the result of research conducted by [Simon Dooms] (http://scholar.google.be/citations?user=owaD8qkAAAAJ) (Ghent University, Belgium) and has been presented on the CrowdRec 2013 workshop which is co-located with the ACM RecSys 2013 conference. Please cite the corresponding paper if you make use of this dataset. The presented slides can be found [on slideshare] (http://www.slideshare.net/simondooms/movie-tweetings-a-movie-rating-dataset-collected-from-twitter).

## Ratings from Twitter

This dataset consists of ratings extracted from tweets. To be able to extract the ratings, The creators query the Twitter API for well-structured tweets. The creators have found such tweets originating from the social rating widget available in IMDb apps. While rating movies, in these apps, a well-structured tweet is proposed of the form:

"I rated The Matrix 9/10 http://www.imdb.com/title/tt0133093/ #IMDb"

On a daily basis the Twitter API is queried for the term "I rated #IMDb". Through a series of regular expressions, relevant information such as user, movie and rating is extracted, and cross-referenced with the according IMDb page to provide also genre metadata. The numeric IMDb identifier was adopted as item id to facilitate additional metadata enrichment and guarantee movie uniqueness. For example, for the above tweet the item id would be "0133093" which allows to infer the corresponding IMDb page link (add http://www.imdb.com/title/tt). The user id simply ranges from 1 to the number of users.

## Data Preparation

Script in file: **1. Data Preparation.ipynb** 

The data consists of two dataframes: 
1. Movies: contains data about each movie like the name, data of release and genre. Movies are indexed using the same id as the other dataframe.
2. Reviews: contains data about each review placed using a user id and a movie id, the data of the review.

For each of the datasets, there are a couple of cleaning steps we need to take care of:

1. Movies
    * Pulling the date from the title and creating new column
    * Dummy the date column with 1's and 0's for each century of a movie (1800's, 1900's, and 2000's)
    * Dummy column the genre with 1's and 0's


2. Reviews
    * Creating a date out of time stamp

   
## The Recommender Engine

As the project is a part of learning process, three types of recommender engines are goin to be implemented through the course of project:

   
### Knowledge-Based Recommendations

Script in file: **2. Knowledge-Based Recommendation.ipynb** 

    - A knowledge based recommendation is one in which knowledge about the item or user preferences are used to make a recommendation.
    - Knowledge based recommendations are pretty common when purchasing luxury items. 
    - Often a rank based algorithm is provided along with knowledge based recommendations to bring the most popular items in particular categories to the user's attention.

#### Part I: How To Find The Most Popular Movies

For this notebook, we have a single task.  The task is that no matter the user, we need to provide a list of the recommendations based on simply the most popular items.

For this task, we will consider what is "most popular" based on the following criteria:

    - A movie with the highest average rating is considered best
    - With ties, movies that have more ratings are better
    - A movie must have a minimum of 5 ratings to be considered among the best movies
    - If movies are tied in their average rating and number of ratings, the ranking is determined by the movie that is the most recent rating

With these criteria, the goal for this notebook is to take a **user_id** and provide back the **n_top** recommendations.  Use the function below as the scaffolding that will be used for all the future recommendations as well.

#### Part II: Adding Filters

Users usually like to choose the popular movies within certain categories, like genre and year of release. In this part I will add a functionality to the script to enable the user to filter the most popular movies based on genre and year. 

