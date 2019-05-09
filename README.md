# Data Modeling with Cassandra

## Introduction
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

They'd like a data engineer to create a Apache Cassandra database with tables designed to optimize queries on song play analysis. The data engineer will create a database schema and ETL pipeline for this analysis. The database and ETL pipeline will be tested by running queries provided by the analytics team from Sparkify and compare the outcome with expected results.

## Database Design
The tables are created to answer the queries outlined in the project:

1 - Get the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4

2 - Get only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182

3 - Get every user name (first and last) in music app history who listened to the song 'All Hands Against His Own'

### Tables
**song_plays_by_session** - store song play activities by session

|COLUMN  	    |TYPE  	        | NOTE   	            |
|-------------- |---------------| ----------------------|
|sessionId      |INT            | Primary Key           |
|itemInSession  |INT            |                       |
|artist         |TEXT           |                       |
|song           |TEXT           |                       |
|length         |DECIMAL        |                       |



**song_plays_by_user** - store song play activities by user

|COLUMN  	    |TYPE  	        | NOTE   	    |
|-------------- |---------------| --------------|
|userId         |INT            | Primary Key   |
|sessionId      |INT            |               |
|itemInSession  |INT            |               |
|artist         |TEXT           |               |
|song           |TEXT           |               |
|firstName      |TEXT           |               |
|lastName       |TEXT           |               |

**users_by_song** - store user info by song title

|COLUMN  	    |TYPE  	        | NOTE   	           |
|-------------- |---------------| ---------------------|
|userId         |INT            | Primary Key          |
|song           |TEXT           |                      |
|firstName      |TEXT           |                      |
|lastName       |TEXT           |                      |



## Extract-Transform-Load (ETL) Pipeline
ETL pipeline is written in Python, which extract data from static text files, transform data to clean/proper data format, then load the data into related tables in the database.

The text files are in CSV format and contain data about songs, users, song play sessions/activities. The files are located in **"event_data"** directory.

## Main Files

**CassandraDataModeling.ipynb** - Jupyper notebook contains methods to extract data from CSV, create database, create tables, and insert data into database.

## How To Run

Th following must be installed and setup on local machine before running the scripts/files in this project:
* Appache Cassandra 
* Python 2.7+
* Python Packages - Jupyter Notebook, Pandas, Cassandra Driver

Run the following commands in terminal:

>jupyter notebook CassandraDataModeling.ipynb




