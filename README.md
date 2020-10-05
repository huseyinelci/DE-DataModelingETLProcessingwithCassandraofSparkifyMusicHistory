<img src="https://github.com/huseyinelci2000/DE-DataModelingofSparkifySongPlay/blob/master/image/RDBS_Sparkify.jpg?raw=true" width="100%">

----

# Data Modeling ETL Processing with Cassandra
## Sparkify Music App History
This project is submission for the Nanodegree Data Engineering Program. In this project consists of putting into practice the following titles:
- Created **Data modeling** with CASSANDRA
- Processing **ETL pipeline** on Python

## 1.Introduction
A startup called Sparkify wants to analyze the data they have been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

They'd like a data engineer to create an Apache Cassandra database which can create queries on song play data to answer the questions, and wish to bring you on the project. Your role is to create a database for this analysis. You'll be able to test your database by running queries given to you by the analytics team from Sparkify to create the results.

## 2.Project Overview
In this project, you'll apply what you've learned on data modeling with Apache Cassandra and complete an ETL pipeline using Python. To complete the project, you will need to model your data by creating tables in Apache Cassandra to run queries. You are provided with part of the ETL pipeline that transfers data from a set of CSV files within a directory to create a streamlined CSV file to model and insert data into Apache Cassandra tables.

We have provided you with a project template that takes care of all the imports and provides a structure for ETL pipeline you'd need to process this data.

## 3. Datasets 
For this project, you will be working with one dataset: event_data. The directory of CSV files partitioned by date. Here are examples of filepaths to two files in the dataset:
```
	event_data/2018-11-01-events.csv
	event_data/2018-11-02-events.csv
	event_data/2018-11-03-events.csv
```
There is one dataset called event_data which is in a directory of **CSV** files partitioned by date. The filepaths are given as **event_data/yyyy-mm-dd-events.csv ** where **yyyy** indicates the year, **mm** indicates the month and **dd** indicates the year. The folder of **event_data** are:
- artist (string)
- auth (string)
- firstName (string)
- gender (char)
- itemInSession (int)
- lastName (string)
- length (float)
- level (string)
- location (string)
- method (string)
- page (string)
- registration (float)
- sessionId (int)
- song (string)
- status (int)
- ts (float)
- userId (int)

### 3.1 Project Template
To get started with the project, go to the workspace on the next page, where you'll find the project template (a Jupyter notebook file). You can work on your project and submit your work through this workspace.

The project template includes one Jupyter Notebook file, in which:

- you will process the event_datafile_new.csv dataset to create a denormalized dataset
- you will model the data tables keeping in mind the queries you need to run
- you have been provided queries that you will need to model your data tables for
- you will load the data into tables you create in Apache Cassandra and run your queries

### 3.2 Project Steps
Below are steps you can follow to complete each component of this project.
###### Modeling your NoSQL database or Apache Cassandra database
1. Design tables to answer the queries outlined in the project template
2. Write **Apache Cassandra** `CREATE KEYSPACE` and `SET KEYSPACE` statements
3. Develop your `CREATE` statement for each of the tables to address each question
4. Load the data with `INSERT` statement for each of the tables
5. Include `IF NOT EXISTS` clauses in your `CREATE` statements to create tables only if the tables do not already exist. We recommend you also include DROP TABLE statement for each table, this way you can run drop and create tables whenever you want to reset your database and test your **ETL pipeline**
6. Test by running the proper select statements with the correct `WHERE` clause

### 3.3 Queries

For NoSQL databases, we design the schema based on the queries we know we want to perform. For this project, we have three queries:

1. Find artist, song title and song length that was heard during sessionId=338, and itemInSession=4.
```Sql
SELECT artist, song, length from music_app_history 
WHERE sessionId=338 AND itemInSession=4
```
2. Find name of artist, song (sorted by itemInSession) and user (first and last name) for userid=10, sessionId=182.
```Sql
SELECT artist, song, firstName, lastName FROM user_session_history 
WHERE userId=10 and sessionId=182
```
3. Find every user name (first and last) who listened to the song 'All Hands Against His Own'.
```Sql
SELECT firstName, lastName FROM user_song_history
WHERE song='All Hands Againgst His Own'
```

### 3.4 Schema
For the first query: 
- Column 1 = sessionId
- Column 2 = itemInSession
- Column 3 = artist
- Column 4 = song
- Column 5 = length
- Primary key = (sessionId, itemInSession)

For the second query:
- Column 1 = userId
- Column 2 = sessionId
- Column 3 = artist
- Column 4 = song
- Column 5 = itemInSession
- Column 6 = firstName
- Column 7 = lastName
- Primary key = (userId, sessionId) with clustering column itemInSession

For the third query:
- Column 1 = song
- Column 2 = firstName
- Column 3 = lastName
- Primary key = (song) with clustering column artist, userId

### 3.5 Build ETL Pipeline
1. Implement the logic in section Part I of the notebook template to iterate through each event file in event_data to process and create a new **CSV** file in **Python**
2. Make necessary edits to Part II of the notebook template to include** Apache Cassandra** `CREATE` and `INSERT` statements to load processed records into relevant tables in your data model
3. Test by running `SELECT` statements after running the queries on your database

### 3.6 Build Instructions

Run each portion of `Project_1B_Project.ipynb`.


<a id="6"></a>
## Source, Licensing, Authors, and Acknowledgements

#### Source
The Source owner is [Sparkify](http://www.sparkify.com/)
#### Licensing
The data In this project is **OpenSource** and owner is  [Sparkify](http://www.sparkify.com/). Also, if _you plan to use this database in your article research or else_ you must taken and read main Source in the **Sparkify Dataset repository**.
#### Authors
Huseyin ELCI
  |  [Github](https://github.com/huseyinelci2000)  |  [Kaggle](https://www.kaggle.com/huseyinelci)  |  [Linkedin](https://www.linkedin.com/in/huseyinelci/)   |  
#### Acknowledgements
Thanks to [Udacity](https://www.udacity.com/) for editing and setting the projects.
Thanks to  [Sparkify](http://www.sparkify.com/) for providing cool data with which we can create a cutting edge project.
