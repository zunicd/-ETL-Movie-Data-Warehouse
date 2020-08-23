# ETL - Movie Data Warehouse

## Objective

This was a team project and its purpose was to find two movie datasets and perform ETL on them to migrate them to a production database.

We are keeping our data warehouse focused on the following subjects:

- does the size of a movie’s budget mean better user and critic ratings

- does the size of a movie’s budget impacts Facebook likes.

  

## EXTRACT

### Data Sources:

We are compiling data on movies from two datasets, one from [Kaggle](https://www.kaggle.com/):

[https://www.kaggle.com/rounakbanik/the-movies-dataset?select=movies_metadata.csv](https://www.google.com/url?q=https://www.kaggle.com/rounakbanik/the-movies-dataset?select%3Dmovies_metadata.csv&sa=D&ust=1590628490638000)

***Resources/movies_metadata.csv*** 

-  **Number of records:**     45,466
-  **Number of Columns**:   24



and the second one from [data.world](https://data.world/):

https://data.world/data-society/imdb-5000-movie-dataset

***Resources/movie_metadata_dw.csv*** 

-  **Number of records:**      5,043
-  **Number of Columns**: 28

This dataset contents a lot of Facebook information about movies, directors and actors.

Both datasets were formatted as CSV files.  

After loading the data from both datasets into Pandas dataframes in a Jupyter notebook, we performed the following transformation on each dataframe:

- We identified all of the columns we want to keep, not including any extraneous columns that we found unnecessary.  We used those columns to create new Pandas dataframes that include only those columns we chose.

  

## TRANSFORM

### Data Cleanup & Analysis

#### Transformation

We performed the following transformations on each dataframe:

-  We **renamed** any columns in both tables with the similar, or confusing column names.
- In order to have the same identifying **primary key -- “imdb_id”** -- in each file, we had to extract the IMDB id number from the “movie_imdb_link” in the second table.  Then, we would have unique id numbers in both tables that could be used to join data.
  

#### Cleaning

- We looked at each dataframe to see if it contained any **null value**s.  Then, based on the results we dropped all of the rows that did not contain a primary key value for “imdb-id” and those that had NaN values in the other columns as well.

- We looked for **duplicate values** in the “imdb-id” column and dropped any duplicate rows, keeping only the first instance of each value.

  

#### Reformatting

- We discovered some issues with spaces in the titles.  We had to replace a special character “ \xa0” with a space to show the proper title string.
- We discovered that the “genres” column included a list of various dictionaries with multiple genres identified.  We cleaned up that column to include the name of each genre separated by comma.
- We had to do the similar genre cleanup in the Facebook movie dataframe.



## LOAD

### Data Storage:

We are compiling data on movies from multiple datasets so that our users can perform data analysis and query the final data.

The final database will be stored in MongoDB (movies_db) and includes the following tables:

- IMDB Metadata (dataframe df) - Collection name in MongoDB:  movies
- Facebook Metadata (dataframe dffb) - Updated the Facebook data into the original MongoDB collection.

Please see the Jupyter notebook included that shows the detailed steps we completed to load our final data.  MongoDB was chosen as the final database because of all of the following reasons:

- Document oriented
- High performance
- High availability and scalability
- Dynamic and flexible - No rigid schema.
- Heterogeneous Data
- No Joins
- Distributed
- Data Representation in JSON or BSON
- Easy Integration with other tools
- MongoDB is built for the cloud.

Once the data was loaded completely, we did some queries to make sure that we could retrieve the information for specific IMDB ids.  We also examined the final data as it appeared in MongoDB Compass Community to see how the data could be queried and used by our developers.

Our custom Movie Data Warehouse is ready :)



## Tools / Techniques Used:

- Python

- jupyter notebook

- Pandas

- MongoDB

- PyMongo

  

#### Team Members:

- Damir Zunic ([zunicd@yahoo.com](mailto:zunicd@yahoo.com))
- Andrea Johnson ([asjohnson099@gmail.com](mailto:asjohnson099@gmail.com))
- Mike Terhorn ([miketerkhorn@gmail.com](mailto:miketerkhorn@gmail.com))
- Sacha Stikeleather ([sestikeleather22@gmail.com](mailto:sestikeleather22@gmail.com))

