# Product Pricing for Profit Maximization

---

## Introduction

One of the secrets to business success is pricing your products properly. Price your products correctly and that can enhance how much you sell, creating the foundation for a business that will prosper (Masserman, 2021).

This project seeks to provide new business owners a starting point at which to price their products based on the current market. In other words, if I were to open a new business and sell a product that is already existing in the market, is there an ideal price range for me to sell the product at for it to be a profitable transaction? 

Dataset used in this project is the "Global Superstore" data which comprise transactions of more than 10,000 products with a clientele coming from 147 different countries, during the period 2012 to 2015.

The project can be organised in two stages: 

<u>*Stage 1 - Clustering*</u>
 
For each product category, I apply unsupervised learning algorithms, `Kmeans`, `DBSCAN`, and `Agglomerative Clustering` to identify clusters of price ranges. Evaluation metric to decide on the optimal number of cluster is the silhouette score, which is the average distance between clusters. A silhouette score ranges from -1 to +1 and a higher score indicates better separation between the clusters.

<u>*Stage 2 - Regression*</u>

Once clusters are set, I perform multivariate regression analysis using `ElasticNetCV`, `Random Forest Regressor`, `Support Vector Regressor` and `XGBoost Regressor` algorithms on each cluster, with profit being the target variable. From the line of best fit, get an accurate range of unit prices for that cluster, where transactions are profitable. 

---

## Framework

Data Cleaning and EDA > Clustering > Regression > Price point

## Folder Organisation

    |__ code
    |   |__ 01-data-cleaning-and-eda.ipynb   
    |   |__ 02-modelling-clustering.ipynb
    |   |__ 03-modelling-regression.ipynb
    |   |__ trx.html  
    |__ data
    |   |__ 1_raw
    |   |__ train.csv
    |   |__ test.csv
    |   |__ weather.csv
    |   |__ spray.csv
    |__ images
    |   |__ xxx.png
    |   |__ xxx.png
    |__ presentation_slides
    |   |__ pricing-products-capstone.pdf
    |__ README.md

## Analysis and Findings

EDA
- growing affluence over the years.

Clustering
- characteristics of different clusters 

Conclusion : sell product at this price range for profitable transaction

Regression 






## Conclusion and Recommendation



## Limitations and Challenges
- as much as art as it is science. (Masserman, 2021)
- must also take into consideration factors affecting purchase behaviour like affluence (propensity to spend like age, housing.), which we lack the data for. 

## Further Development


## References

"How to Price Your Products" (Masserman, 2021)
https://www.inc.com/guides/price-your-products.html


----

# Data Dictionary

Below the description of Superstore data. This dataset comprise all transactions 

| Features | Data Type | Description |
| :-------: | :--: | :---- |
| Row ID | int | unique identifier for each item purchased |
| Order ID | str | unique identifier for orders placed by a consumer |
| Order Date | datetime | date order was made or transaction date |
| Ship Date | datetime | date order was shipped |
| Ship Mode  | str | categorical variable of shipment class (ie. first class, second class, standard class or same day) |
| Customer ID | str | unique identifier assigned to customer based on orders|             
| Customer Name  | str | name of consumer |       
| Segment  | str  | type of purchase (ie. consumer, corporate or home office) |
| Postal Code | float | zip code based on location of purchase |
| City | str | city where purchase was made |                 
| State | str| state where purchase was made |                     
| Country | str | country where purchase was made |                  
| Region  | str | region where purchase was made |                
| Market | str | market where purchase was made |                 
| Product ID  | str  |  unique identifier for type of product |          
| Category | str  | category for product purchased |              
| Sub-Category | str   | sub-category for product purchased |            
| Product Name  | str  | product name for product purchased |           
| Sales | float | total sales for the transaction |
| Quantity  | int | quantity ordered for transaction |
| Discount | float | percentage discount used for transaction |
| Profit  | float | sales less discount and cost of transaction |
| Shipping Cost | float | shipping cost for the transaction |
| Order Priority | str | categorical vairable indicating high, medium, low or critical priority for the transaction |      

