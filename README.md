# Amazon Vine Analysis

## Project Overview

In this project, we used PySpark, AWS RDS, SQL, and pgAdmin to extract, transform and load Amazon review to analyze paid and unpaid reviews for various products. 

## Deliverable 1 

Initially, we created a new database with Amazon RDS and connected that to pgAdmin with an AWS server. Then, through pgAdmin, we queried the database and produced tables for customers, products, review IDs, and vine reviews. 

Then, through Google Colab, we created a new dataframe to match. 

![This is an image](https://github.com/sophiehearn/Amazon_Vine_Analysis2/blob/main/BookReviews.png?raw=true)

We grouped customers by customer ID, created a product table, created a review ID table, and finally created a table to track vine reviews. 

Below is a screenshot of the customer ID count table, as an example. 
![This is an image](https://github.com/sophiehearn/Amazon_Vine_Analysis2/blob/main/customer_id.png?raw=true)

Finally, we connected this table to pgAdmin to populate it with the data. 

## Deliverable 2

We were interested in understanding whether there was an impact on review ratings based on whether it was a paid or unpaid review. In this case, the "vine" reviews are paid, and ones that aren't vine are unpaid. 

Initially we sorted by "helpful" reviews, and reviews that had 20+ total votes. 

Then we filtered by vine (`vine == Y`) and non-vine (`vine == N`). 

Initially, I was analyzing a set of reviews which had no vine reviews (eBooks), so I redid the analysis with a set of reviews for apparel, which provide vine vs no-vine reviews.

Here is a snapshot of the relevant code used to calculate the percentage of 5 star reviews which were paid (vine) vs unpaid:

```
# 5 star paid reviews
five_star_paid = filtered_vine_df.filter(col("star_rating") == 5).count() 
five_star_paid_percent = five_star_paid/five_star_reviews*100
five_star_paid_percent
```

We were able to determine that the PAID reviews for apparel constituted .06% of 5 star reviews, but were less than .01% of total reviews. Thus, we can see that although paid reviews are a small portion of overal reviews, they were much more likely to be 5 stars.

## Summary

Ultimately, we learned that paid reviews are more likely to give the highest ratings (5 stars). Thus, we can hypothesize that there is a bias, but to understand the statistical significance of this potential bias, we would need to run a t-test and confirm our hypothesis.