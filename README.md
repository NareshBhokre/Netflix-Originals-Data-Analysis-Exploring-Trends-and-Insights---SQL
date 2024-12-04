# Netflix-Originals-Data-Analysis-Exploring-Trends-and-Insights - SQL Project
# Objective:
The objective of this project is to analyze the Netflix Originals dataset using MySQL queries to extract meaningful insights and trends. By performing various SQL operations such as GROUP BY, HAVING, ORDER BY, LIMIT, JOINS, WINDOW FUNCTIONS, and SUBQUERIES, participants will gain hands-on experience in data analysis and be better prepared for data analyst job roles.
# Dataset:
1. Netflix_Originals: https://docs.google.com/spreadsheets/d/14ExfGXNya1fBPs_SlZj4-q2GHLOa4LLbJ9ADJIwK480/edit?gid=979450355#gid=979450355
2. Genre_Details: https://docs.google.com/spreadsheets/d/17xAZ21LLYrS8Q6vZHqXyWxe_6SW2Pa-H1EUg__EWGTA/edit?gid=201028059#gid=201028059
# Datasets Description:
1. Netflix Originals: This dataset contains information about Netflix Originals including title, genre ID, runtime, IMDb score, language, premiere date, etc.
2. Genre Details: This dataset contains information about genres such as genre ID and genre name.
# Analyses to make:
1. What are the average IMDb scores for each genre of Netflix Originals?

  SELECT gd.Genre AS Genre, AVG(no.IMDBScore) AS Average_IMDB_Score FROM Netflix_Originals.no
  JOIN Genre_Details gd
  ON no.GenreID = gd.GenreID
  GROUP BY gd.Genre
  ORDER BY Average_IMDB_Score DESC;

2. Which genres have an average IMDb score higher than 7.5?

   SELECT gd.Genre AS Genre, AVG(no.IMDBScore) AS Average_IMDB_Score FROM Netflix_Originals no
   JOIN Genre_Details gd
   ON no.GenreID = gd.GenreID
   GROUP BY gd.Genre
   HAVING Average_IMDB_Score > 7.5;

3. List Netflix Original titles in descending order of their IMDb scores.

   SELECT Title as NetflixOriginaltitles, IMDBScore FROM netflix_originals
   ORDER BY NetflixOriginaltitles DESC;

4. Retrieve the top 10 longest Netflix Originals by runtime.

   SELECT title as NetflixOriginals, runtime FROM netflix_originals
   ORDER BY NetflixOriginals DESC
   LIMIT 10;

5.	Retrieve the titles of Netflix Originals along with their respective genres.

   SELECT Title, Genre FROM netflix_originals
   JOIN genre_details gd 
   GROUP BY Title, Genre;

6. Rank Netflix Originals based on their IMDb scores within each genre.

   SELECT Title as Genre, IMDBScore,
   RANK () OVER (PARTITION BY Title ORDER BY IMDBScore DESC) as IMDBRank from netflix_originals
   ORDER BY Genre, IMDBRank;

7.	Which Netflix Originals have IMDb scores higher than the average IMDb score of all titles?

   SELECT title, IMDBScore FROM netflix_originals
   WHERE IMDBScore > (SELECT AVG(IMDBScore) FROM netflix_originals);

8.	How many Netflix Originals are there in each genre?

   SELECT Genre, count (*) AS netflix_original_count FROM netflix_originals
   JOIN genre_details
   GROUP BY Genre
   ORDER BY netflix_original_count DESC;

9.	Which genres have more than 5 Netflix Originals with an IMDb score higher than 8?

    SELECT Title AS num_netflix_originals, IMDBScore FROM netflix_originals
    JOIN genre_details gd 
    HAVING num_netflix_originals > 5 AND IMDBScore > 8;

10.	What are the top 3 genres with the highest average IMDb scores, and how many Netflix Originals do they have?

    SELECT Genre, AVG(IMDBScore) AS avg_imdb_score, COUNT(Title) AS netflix_original_count FROM netflix_originals
    JOIN genre_details
    GROUP BY Genre
    ORDER BY avg_imdb_score DESC
    LIMIT 3;













