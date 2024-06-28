# 1. Introduction
Movie rental Data Analysis.<br />
Answer business intelligence (BI) questions by cleaning and querying Data sets with PreSQL, creating a data dictionary and finally present findings.


# 2. Business understanding
Rockbuster Stealth LLC is a movie rental company that used to have stores around the
world. Facing stiff competition from streaming services such as Netflix and Amazon Prime,
the Rockbuster Stealth management team is planning to use its existing movie licenses to
launch an online video rental service in order to stay competitive.

## Key questions and objectives
The Rockbuster Stealth Management Board has asked a series of business questions and
they expect data-driven answers which they can use for their 2020 company strategy. Here are
the main questions they’d l ike to answer:

Which movies contributed the most/least to revenue gain?
* What was the average rental duration for all videos
* Which countries are Rockbuster customers based in?
* Where are customers with a high lifetime value based?
* Do sales figures vary between geographic regions?

# 3. Data understanding

## Data set
The rational database used for this projects contains 15 tables which are connected to eachother over a private key and/or foreign key.
This data set contains information about Rockbuster' film inventory, customers, payments and more.
[Rockbuster data set](</dvdrental.zip>)

## Data structure
The data structure at hand is setup as a snowflake schema. There is one fact table "payment" which has many dimension tables like "rental", "store", "customer" and "staff".
These dimension tables are connected to sub dimension tables like "film_actor","film_category", "category" and so on.
For a more detailed perspective please see below the ERD (Entity Relationship Diagram) which was extracted with Postgres pgAdmin.
![Rockbuster ERD](</02 Data/ERD Rockbuster.png>)

With the data dictionary all data types, tables and their relationship to eachother can be identified. [Rockbuster data dictionary](</05 Sent to client/Rockbuster Data Dictionary.pdf>)

## Tools
For this project the following tools were used
* PostgreSQL
* Tableau

# 4. Data preperation
To prepare the data properly for visualization we need to follow the following steps: Extract, transform, load into new database (in this case it will be to export the data into csv for visualization purposes)

First extract some key data for the final presentation to give the audience a feel of the data set and what it holds.
Extract the following:
* Count of all available movies
* MIN, MAX and AVERAGE of the following:</br >
&emsp;&emsp;- year of release</br >
&emsp;&emsp;- Rental duration</br >
&emsp;&emsp;- Rental rate</br >
&emsp;&emsp;- Movie length in minutes</br >
&emsp;&emsp;- replacement costs</br >
```SQL
--query MIN,MAX, AVG and count of movies
SELECT
	COUNT(film_id) AS count_of_movies,
	MAX(film_id) AS highest_film_id,
	
	MIN(release_year) AS MIN_release_year,
	MAX(release_year) AS MAX_release_year,
	AVG(release_year) AS AVG_release_year,
	
	MIN(rental_duration) AS MIN_rental_duration,
	MAX(rental_duration) AS MAX_rental_duration,
	AVG(rental_duration) AS AVG_rental_duration,
	
	MIN(rental_rate) AS MIN_rental_rate,
	MAX(rental_rate) AS MAX_rental_rate,
	AVG(rental_rate) AS AVG_rental_rate,
	
	MIN(length) AS MIN_length,
	MAX(length) AS MAX_length,
	AVG(length) AS AVG_length,
	
	MIN(replacement_cost) AS MIN_replacement_cost,
	MAX(replacement_cost) AS MAX_replacement_cost,
	AVG(replacement_cost) AS AVG_replacement_cost
	
FROM film
```

Extract data about the movies which produce the most revenue
```SQL
--extract movies with the most revenue by join rental, inventory and film and sum the amount
SELECT title,
       SUM(amount) AS total_payment
FROM payment A
INNER JOIN rental B ON A.rental_id = B.rental_id
INNER JOIN inventory C ON B.inventory_id = C.inventory_id
INNER JOIN film D ON C.film_id = D.film_id

GROUP BY title
ORDER BY total_payment DESC
```

Extract data about which countries the most customers come from
```SQL
--Extract data from which country most customer come from
SELECT 	D.country,	
		COUNT(customer_id) as customer_countries
FROM customer A	
INNER JOIN address B ON A.address_id = B.address_id	
INNER JOIN city C ON B.city_id = C.city_id	
INNER JOIN country D ON C.country_id = D.country_id	
	
GROUP BY country	
ORDER BY customer_countries DESC
```	

Where are customers with a high value based.
```SQL
--Customers with a high value from which country
SELECT country,
       COUNT(A.customer_id) AS customer_count,
       SUM(amount) AS total_payment
FROM payment A
INNER JOIN customer B ON A.customer_id = B.customer_id
INNER JOIN address C ON B.address_id = C.address_id
INNER JOIN city D ON C.city_id = D.city_id
INNER JOIN country E ON D.country_ID = E.country_ID

GROUP BY country
ORDER BY total_payment DESC
```


## Final presentation
Final presentation please see here [Rockbuster Data Analysis](</Rockbuster Data Analysis.pdf>)<br />
Visualizations made with Tableau please see here [Tableau visualisations](https://public.tableau.com/app/profile/constantin.melachrinos/viz/Rockbuster_17157995150910/Customerscountry?publish=yes)

