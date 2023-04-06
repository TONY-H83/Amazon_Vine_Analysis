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
