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
* MIN, MAX and AVERAGE of the following
&emsp;&emsp;- year of release
&emsp;&emsp;- Rental duration
&emsp;&emsp;- Rental rate
&emsp;&emsp;- Movie length in minutes
&emsp;&emsp;- replacement costs


## Final presentation
Final presentation please see here [Rockbuster Data Analysis](</Rockbuster Data Analysis.pdf>)<br />
Visualizations made with Tableau please see here [Tableau visualisations](https://public.tableau.com/app/profile/constantin.melachrinos/viz/Rockbuster_17157995150910/Customerscountry?publish=yes)

