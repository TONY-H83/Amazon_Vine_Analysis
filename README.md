# Amazon_Vine_Analysis
---

### Overview

#### The analysis performed in this assignment was in ordet to determine any bias in the Amazon Vine reviews dataset. There are two different main categories of reviews, they are "Vine" (Paid) and "Non-Vine" (Unpaid). To perform this analysis, I used the ETL methodolgy using Google Colab, AWS, and pgAdmin. 
---

### Extract

#### To extract the data, I imported the dataset into a Google Colab notebook using `Spark`. After reading in the data, I created 4 different tables that would later be used for the trasnform step of the ETL process. 
---

### Transform

#### The 4 tables created were:
- `customers_df = df.groupby("customer_id").agg({"customer_id": 'count'}).withColumnRenamed("count(customer_id)", "customer_count")`
- `products_df = df.select(['product_id','product_title']).drop_duplicates()`
- `review_id_df = df.select(["review_id", "customer_id", "product_id", "product_parent", to_date("review_date", 'yyyy-MM-dd').alias("review_date")])`
- `vine_df = df.select(["review_id", "star_rating", "helpful_votes", "total_votes", "vine", "verified_purchase"])`
---

### Load

#### The load step from the ETL process was accomplished by creating an AWS relational database (RDS) and writing the 4 tables that I created in the transform step. The RDS was setup to use `postgres` and was then connected to my local pgAdmin program. The true analysis was done by creating a CSV export of the `vine_df_table`. 
---

## Analysis

#### There was another round of Extract and Transform performed in order really understand if there was any bias to the vine reviews. The first thing I did was to read in the `vine table` into a Jupyter Notebook file using Python and create a dataframe. 

- Create a DataFrame or table where there are 20 or more total votes
![](https://github.com/TONY-H83/Amazon_Vine_Analysis/blob/main/Images/Reviews%20greater%20than%2020.png)

- Filtered to create a DataFrame where the percentage of helpful_votes is equal to or greater than 50%
![](https://github.com/TONY-H83/Amazon_Vine_Analysis/blob/main/Images/Most%20helpful%20review%20filter.png)

- The data is filtered to create a DataFrame where there is a Vine review (Paid)
![](https://github.com/TONY-H83/Amazon_Vine_Analysis/blob/main/Images/Count%20of%20paid%20reviews.png)

- The data is filtered to create a DataFrame where there isn’t a Vine review (Unpaid)
![](https://github.com/TONY-H83/Amazon_Vine_Analysis/blob/main/Images/Count%20of%20unpaid%20reviews.png)

- The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews
![](https://github.com/TONY-H83/Amazon_Vine_Analysis/blob/main/Images/Screenshot%202023-04-05%20at%207.45.13%20PM.png)
---

### Summary

- 8332 Unpaid reviews (non-vine)
- 19 Paid reviews (vine)
- 9 Vine 5-star reviews
- 4783 Non-vine 5-star reviews
- 47% of the Vine reviews were 5-star reviews
- 57% of the Non-vine reviews were 5-star reviews

The analysis of the reviews would show that there does not seem to be a bias between Vine and Non-vine reviews. The percentage of 5-star reviews are within 10% of eachother regardless of the significant difference in the number of votes. Further analysis could be done to determine if the cost of being a Vine member is worth it. There seems to be a much better paricipation rate with non-paid users. Could the cost of the Vine membership be reduced? What number of Vine users are not casting votes?

