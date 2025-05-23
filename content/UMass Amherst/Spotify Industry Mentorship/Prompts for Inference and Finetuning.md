---
title: Prompts for Inference and Finetuning
tags:
    - SQL-generation
    - prompts
    - fine-tuning
    - inference
created: 2025-05-11
---


### Inference Prompt

```
You are an expert SQL assistant. 
    Your task is to generate ONLY the final SQLite SQL query starting from SELECT that answers the given natural language question using the provided database schema and external knowledge. Do not include any explanations, comments, or markdown formatting.
    

<schema>:

CREATE TABLE `customers` (
  `CustomerID` integer NOT NULL
,  `Segment` text
,  `Currency` text
,  PRIMARY KEY (`CustomerID`)
,  UNIQUE (`CustomerID`)
)

CREATE TABLE `gasstations` (
  `GasStationID` integer NOT NULL
,  `ChainID` integer DEFAULT NULL
,  `Country` text
,  `Segment` text
,  PRIMARY KEY (`GasStationID`)
,  UNIQUE (`GasStationID`)
)

CREATE TABLE `products` (
  `ProductID` integer NOT NULL
,  `Description` text
,  PRIMARY KEY (`ProductID`)
,  UNIQUE (`ProductID`)
)

CREATE TABLE `transactions_1k` (
  `TransactionID` integer NOT NULL PRIMARY KEY AUTOINCREMENT
,  `Date` date DEFAULT NULL
,  `Time` text
,  `CustomerID` integer DEFAULT NULL
,  `CardID` integer DEFAULT NULL
,  `GasStationID` integer DEFAULT NULL
,  `ProductID` integer DEFAULT NULL
,  `Amount` integer DEFAULT NULL
,  `Price` double DEFAULT NULL
)

CREATE TABLE `yearmonth` (
  `CustomerID` integer NOT NULL
,  `Date` varchar(255) NOT NULL
,  `Consumption` double DEFAULT NULL
,  PRIMARY KEY (`Date`,`CustomerID`)
,  CONSTRAINT `yearmonth_ibfk_1` FOREIGN KEY (`CustomerID`) REFERENCES `customers` (`CustomerID`) ON DELETE CASCADE ON UPDATE CASCADE
)

[QUESTION]:
"What is the ratio of customers who pay in EUR against customers who pay in CZK?"


[EVIDENCE]:
ratio of customers who pay in EUR against customers who pay in CZK = count(Currency = 'EUR') / count(Currency = 'CZK').
[SQL]:



```

### Finetuning Prompt

```
You are an expert SQL assistant.\n\n    Your task is to generate ONLY the final SQLite SQL query starting from SELECT that answers the given natural language question using the provided database schema and external knowledge. Do not include any explanations, comments, or markdown formatting.\n\n    [SCHEMA]\n    DATABASE: movie_platform\n\nCREATE TABLE `lists` (\n  `user_id` integer,\n  `list_id` integer PRIMARY KEY,\n  `list_title` text,\n  `list_movie_number` integer,\n  `list_update_timestamp_utc` text,\n  `list_creation_timestamp_utc` text,\n  `list_followers` integer,\n  `list_url` text,\n  `list_comments` integer,\n  `list_description` text,\n  `list_cover_image_url` text,\n  `list_first_image_url` text,\n  `list_second_image_url` text,\n  `list_third_image_url` text\n)\n\nCREATE TABLE `movies` (\n  `movie_id` integer PRIMARY KEY,\n  `movie_title` text,\n  `movie_release_year` integer,\n  `movie_url` text,\n  `movie_title_language` text,\n  `movie_popularity` integer,\n  `movie_image_url` text,\n  `director_id` text,\n  `director_name` text,\n  `director_url` text\n)\n\nCREATE TABLE `ratings_users` (\n  `user_id` integer,\n  `rating_date_utc` text,\n  `user_trialist` integer,\n  `user_subscriber` integer,\n  `user_avatar_image_url` text,\n  `user_cover_image_url` text,\n  `user_eligible_for_trial` integer,\n  `user_has_payment_method` integer\n)\n\nCREATE TABLE `lists_users` (\n  `user_id` integer PRIMARY KEY,\n  `list_id` integer PRIMARY KEY,\n  `list_update_date_utc` text,\n  `list_creation_date_utc` text,\n  `user_trialist` integer,\n  `user_subscriber` integer,\n  `user_avatar_image_url` text,\n  `user_cover_image_url` text,\n  `user_eligible_for_trial` text,\n  `user_has_payment_method` text\n)\n\nCREATE TABLE `ratings` (\n  `movie_id` integer,\n  `rating_id` integer,\n  `rating_url` text,\n  `rating_score` integer,\n  `rating_timestamp_utc` text,\n  `critic` text,\n  `critic_likes` integer,\n  `critic_comments` integer,\n  `user_id` integer,\n  `user_trialist` integer,\n  `user_subscriber` integer,\n  `user_eligible_for_trial` integer,\n  `user_has_payment_method` integer\n)\n\n    [QUESTION]\n    Name movie titles released in year 1945. Sort the listing by the descending order of movie popularity.\n\n    [EVIDENCE]\n    released in the year 1945 refers to movie_release_year = 1945;\n\n    [SQL]
```