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

# Clustering
We have used K-Nearest Neighbor algorithm (KNN) to get the 10 nearest neighbors of each movie based on the users’ ratings for this movie.  
# Function getting similar movies
We implemented “get_movie_recommendation” function which takes the entered movie name by user and it checks if it is a substring of any movie title in “title” column in our dataset then it appends all matching results into “movie_list”. If the list is empty, it will display to the user that the movie is not found. In case there is one matching result only, the 10 most similar movies will be displayed with their distances to the required movie. Otherwise, it displays the matching results with their indices to the user. The user picks the required movie by entering the movie’s index then the function displays the 10 most similar movies with their distances. Inside the function, we also print both mean and standard deviation of distances between results and the required movie. We also print the percentage of distances which are less than 0.4 (near movies).   
*Note: the matching process is done without considering case sensitivity.*  
# Sample Test Cases
First test case: getting the 10 most similar movies to “Iron Man” movie  
STEP1: Displaying the matching results to let the user pick the required movie  
![image](https://user-images.githubusercontent.com/64103395/179246677-ed9fda0d-f483-43c6-8be7-5e42f0cf86b2.png)  
STEP2: Displaying 10 most similar movies for “Iron Man” based on the user's rating   
![image](https://user-images.githubusercontent.com/64103395/179246888-52ee0f0d-9ff8-47bb-b978-d608e18b0e3f.png)  
STEP3: Displaying a bar graph of the distances of these movies  
![image](https://user-images.githubusercontent.com/64103395/179248646-05d67a32-e647-49ca-9df5-c92ee9264f4f.png)
