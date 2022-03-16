# Amazon_Vine_Analysis

## Overview
Analyze Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

Choose one of these [datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt). Each one contains reviews of a specific product, from clothing apparel to wireless products. Use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Then use Pandas & a Jupyter Notebook to determine if there is any bias toward favorable reviews from Vine members in the dataset. 

## Steps
1. I started by choosing the [camera dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Camera_v1_00.tsv.gz) to work with. 
2. In Amazon Web Services' RDS, I created a database on  to host my big data file. 
3. In PG ADmin, I created a server and linked it to my AWS database. Then started a query to creat 4 empty tables (with just column headers) from the camera dataset. 
    <p align="center"><image src="images/empty_tables.JPG" width="500" height="500"></p>
4. Next, I used [Google CoLab to do some ETL](Amazon_Reviews_ETL.ipynb) on the camera data. First, I had to import Spark & Posgres and start a Spark session. Then, I read in the camera data and performed some ETL create the pgAdmin tables (with data:wink:). Next, I connected the  to my AWS dataframe to load the morphed data into my AWS dataframe, and connect with my pgAdmin tables. It took a while to load the tables!
5. I verified the data loaded into my pgAdmin tables by running `SELECT * FROM table_name` in a pgAdmin query. 
    <p align="center"><image src="images/filled_tables.JPG" width="500" height="750"></p>
6. I saved the vine_table.csv so that I could run some more [ETL using Pandas & Jupyter Notebook](Vine_Review_Analysis.ipynb) to compare the Vine member buyers & non-Vine member buyers. This comarison determined if there was any bias towards reviews based on membership.

## Results

| Vine Member? | Total Reviews | Total 5:star: Reviews | Percent 5:star: Reviews |
| :--- | --- | --- | --- |
| YES | 607 | 257 | 42.3 % |
| NO | 50522 | 25220 | 49.9 % |

 - How many Vine reviews and non-Vine reviews were there?  
    <p align="center"><image src="images/total_reviews.JPG" width="450" height="160"></p>
 - How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?  
    <p align="center"><image src="images/5_star.JPG" width="600" height="550"></p>
 - What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?  
    <p align="center"><image src="images/5_star_percent.JPG" width="530" height="160"></p>

## Summary
There doesn't seem to be bias at all because the people who have no financial motivation to make reviews gave less 5-star reviews than those who don't. Although, one can't help to think that a professional reviewer may be more critical than the average person and therefore less likely to give a 5-star. For further analysis, I would do a statistical test on the data to grade it's accuracy. I would also compare this same ETL for all the other stars and compare those, just like I did for the 5-star to see if the 42/49 pattern is similar across all stars. I am guessing the non-reviewers will have more 5 and 1 stars and the professional will have more in the 2-4 star categories. 
