# Movie-Recommendation
 NLP Project  
# Introduction  
The main idea of the project is to select the top 10 similar movies for each movie in the dataset based on the user’s ratings.  
# Dataset Summary  
This dataset describes 5-star rating and free-text tagging activity from [MovieLens], a movie recommendation service.  It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018. The data are contained in the files `movies.csv` and `ratings.csv`.    
# Movies Data File Structure(movies.csv):
Movie information is contained in ‘movies.csv’. Each movie has a unique ID, title and genre.  
# Ratings Data File Structure (ratings.csv):  
All ratings are contained in the file `ratings.csv`. Each line of this file after the header row represents one rating of one movie by one user, and has the following format:  
    userId, movieId, rating, timestamp  
The lines within this file are ordered first by userId, then, within user, by movieId.  
Ratings are made on a 5-star scale, with half-star increments (0.5 stars - 5.0 stars).  
Timestamps represent seconds since midnight Coordinated Universal Time (UTC) of January 1, 1970.  
# Data Preprocessing  
1.	Firstly, we performed an outer merge between two csv files; “movies” and “ratings” on “movieId” column into a new data frame called “RatedMovies”. We did this step in order to be able to use pivot_table() function in the next step which works on one dataframe.  
   ![image](https://user-images.githubusercontent.com/64103395/179240593-6f1a1683-52bc-46d4-a95d-1037f4914477.png)

2.	Out of the whole data, the most important features we will need are “userId”, “title” & “movieId” features. So, we continued preprocessing by using pivot_table() function which is used to reshape a given dataframe organized by given index and column values. Pivot_table() function is applied on “RatedMovies” dataframe setting the index to a list containing two columns; “movieId” and “title” while setting columns to “userId”. Then, creating a new dataset called “final_dataset” which is set to that new dataframe.   
   
3.	Filling undefined cells: it is done by just filling these cells by 0 instead of “NaN” using fillna() function. We also set “inplace” variable to true to apply the changes on the data frame itself.  
   ![image](https://user-images.githubusercontent.com/64103395/179240930-5405f307-0d29-4fd7-9606-09a698c559e4.png)

# Features Extraction
We have applied this step to remove outliers from both users and movies datasets based on two conditions:
1.	Removing movies that have been rated by 5 users or less.  The following graph shows the relation between movies and the number of users rating these movies:  
   ![image](https://user-images.githubusercontent.com/64103395/179242385-1e8eba21-b2f5-4028-aece-5e145e540f30.png)

2.	Removing users that have rated 15 movies or less.  The following graph shows the relation between users and the number of movies rated by them:  
   ![image](https://user-images.githubusercontent.com/64103395/179242768-67ab83d0-d069-4d80-b965-3694b210b56f.png)

