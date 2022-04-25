# Customer Segmentation with RFM Analysis: Project Overview
* The [data](https://www.kaggle.com/regivm/retailtransactiondata?select=Retail_Data_Transactions.csv) provides customer and date level transactions for few years. 
* From this, by using RFM analysis we can get the customer segmentation
* Along this project, use the common 2 clustering algorithm: Agglomerative and K-Means
* At the end, the result is customers can be segmented into 3 types: Gold, Silver, and Bronze

# Shortly About Agglomerative and K-Means
## Agglomerative
* Clusters 2 adjacent data
* Has `Dendogram` as the internal evaluation
* **Deterministic**
* The distance can be measured with: `Euclidean Distance`, `Manhattan Distance`, `Minkowski Distance`, and `Hamming Distance`

## K-Means
* Looking for stable centroid to cluster the data
* **Non-Deterministic**
* Has `inertia` as the internal evaluation or known as `Elbow Method`

# Data Preparation
**Convert the `trans_date` into Date Time format**
## Converts The `trans_date` into Date Time Format
* **As the `trans_date` not in the right data type as the datetime, we have to convert it for the next purpose, especially for the RFM's featuring process** by adding this code:
`data["trans_date"] = pd.to_datetime(data["trans_date"])`

## Create **RFM** Features *(Receny, Frequency, and Monetary)*
### Recency
* This feature to see **how many days ago** the customers did their last transacation
* In this step, use the `trans_date` that have been converted into date time format before
* Find the last transaction with `max()` function to set the last date
* Then, by subtracting that `last date` with `trans_date`, we get the recency days

### Frequency
* This feature to see **how often the customers did the transactions**
* Can be obtained by grouping the data by their unique ID, then count the transaction date

### Monetary
* This feature to see **how many money value customers spend for all their transactions**
* Can be obtained y grouping the data by their unique ID, then count the transaction amount

# Result
Using `K-Means` and `Agglomerative` have the same result, 3 cluster.<br>
![alt text](https://github.com/primabk/Customer_Segmentation_with_RFM/blob/main/Segmentation%20with%20K-Means.png)

# Summary
1. With `K-Means` we get the optimal number of clusters are 3, and means to be there will be 3 segmentations from the data. I called this segementation as below:
    * **Bronze for lower segmentation (clluster 0)**<br>
        High recency, low frquency, high monetary
    * **Silver for middle segmentation (clluster 1)**<br>
        low recency, low frequency, high monetary
    * **Gold for higher segmentation (clluster 2)**<br>
        low recency, low frequency, higher monetary
2. Actions may be taken:
    * **Bronze**<br>
        * take a look if there are any issues around the product/service<br>
        engage them with related promotion cupon based on the previous transaction<br>
    * **Silver**<br>
        * give them more related promotion cupon to improve their transactions amount so eventually they become gold customers<br>
    * **Gold**<br>
        * give them any rewards as their loyalty to deal their transactions on the service<br>
