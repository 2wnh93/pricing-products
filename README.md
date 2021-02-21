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

Once clusters are set, I perform multivariate regression analysis using `ElasticNetCV`, `LassoCV`,`Random Forest Regressor`,`Support Vector Regressor` and `XGBoost Regressor` algorithms on each cluster, with profit being the target variable. To determine the line of best fit, I use R<sup>2</sup> score as the evaluation metric, where a higher R<sup>2</sup> score, closer to 1 is better. From the line of best fit, I then get a range of unit prices for that cluster, where transactions are profitable. 

---

## Framework

![](images/framework.png)


## Folder Organisation

    |__ code
    |   |__ 01-data-cleaning-and-eda.ipynb   
    |   |__ 02-modelling-clustering.ipynb
    |   |__ 03-modelling-regression.ipynb
    |   |__ trx-pandas-profiling-report.html  
    |__ data
    |   |__ superstore-trx.csv
    |   |__ phones_clean.csv
    |   |__ phones_clustered.csv
    |__ images
    |   |__ framework.png
    |   |__ seasonality.jpg
    |   |__ eda.jpg
    |   |__ discount.jpg
    |   |__ rfm.jpg
    |__ presentation_slides
    |   |__ pricing-products-capstone.pdf
    |__ README.md


## Analysis and Findings

#### [<ins>Data Cleaning and EDA</ins>](code/01-data-cleaning-and-eda.ipynb)

The dataset comprise >50,000 transactions with 51 features from retailers across the world, selling items typical of a superstore. These transactions comprise the following product categories: `Technology`, `Furniture` and `Office Supplies`. 

Data cleaning processes including removing features with substantial (>70%) missing values, and those that do not provide added value. For instance, `Product ID` is unique to every product, and would not help with clustering. 

Most retailers are subjected to the seasonality of sales, where sales usually peak during summer (middle of the calendar year) and year-end. 

![](images/seasonality.JPG)

*Figure 1: Number of transactions on a monthly, weekly, and yearly basis*

Overall volume of transactions increased over the years from 2012 to 2015, which suggests growing affluence globally. There is also clear seasonality in sales, where months with the highest volume of transactions in *June, September, November* and *December*. This is expected with Christmas season, and bonus payout towards the end of the year. 

![](images/eda.JPG)

*Figure 2: Profit, Sales and Shipping cost of transactions, by region and category of items*

From Figure 2 above, we can see that `Western Africa`, `Western Asia` and `Central Asia` are unprofitable regions. These regions generally have lower sales and shipping cost.

Also, shipping costs very closely resemble sales amount for the respective regions. This may imply that shipping costs are a strong contributor to more sales. 

![](images/discount.JPG)

*Figure 3: Discount of transactions, by region and category of items*

Here we also see that the unprofitable regions have higher discounts, than other regions. 

Based on observations above, I engineered features to identify heavily discounted regions (>0.3%), non-profitable regions, and region which purchase relatively higher quantity (>3).

Customer segmentation analysis should also consider `Recency`, `Frequency` and `Monetary Value` (RFM) analysis.RFM segmentation allows marketers to target specific clusters of customers by communicating in a way that is more relevant based on the particular customer's behaviour based on RFM of the customer. By doing so, the Company can generate much higher response rates, increased loyalty and customer lifetime value (Optimove, 2020).

I attempt to identify if there are any obvious clusters, by creating new features which represent the `Recency`, `Frequency` and `Monetary Value` of transactions by customers. 

Following through from above analysis, I would expect some significant differences among regions, or between profitable regions and unprofitable regions. However, there does not seem to be any significant variance for me to glean any insights from RFM (Figure 4).

![](images/rfm.JPG)

*Figure 4: Recency, Frequency and Monetary Value, by region and category of items*

Once all features are engineered, and data is clean, I used just the `Phones` subcategory transactions for further analysis. Outliers are removed and categorical variables are one hot encoded. 

#### [<ins>Clustering</ins>](code/02-modelling-clustering.ipynb)

Clustering algorithms like `KMeans` are distance-based algorithms so prior to running the model, I used a `MinMaxScaler` to scale the features, for a more accurate clustering result. 

To avoid any noise in the data that can affect clustering, I tried combinations of features, to eventually scale down to the more important ones for clustering. 

<u>KMeans</u>

For KMeans, I have to feed the number of clusters and assess the silhouette score subsequently. I applied a range of 2 to 10 clusters to determine which number of clusters is the best, using the elbow method, inconjunction with the silhouette score. 

![](images/elbow.JPG)

*Figure 5: Distortion score elbow across 2 to 10 clusters*

**Distortion score** is the sum of squared distances from each point to its assigned center (ie. sum of squared errors). The elbow method seeks to identify a point as number of clusters increase, where the distortion score start to flatten, forming the elbow. This is determined to be the ideal number of clusters for the data.

Figure 5 shows that 3 clusters is the ideal number of clusters. 

![](images/silhouette.JPG)

*Figure 6: Silhouette score of 2 to 4 clusters*




## Conclusion and Recommendation



## Limitations and Challenges
- as much as art as it is science. (Masserman, 2021)
- must also take into consideration factors affecting purchase behaviour like affluence (propensity to spend like age, housing.), which we lack the data for. 
- learning points: 
- munging data, shifting of objectives. 

## Further Development
Intended intention of this project was to use ecommerce retail transactions data, and perform customer segmentation, and infer consumer behaviour from there. 

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

