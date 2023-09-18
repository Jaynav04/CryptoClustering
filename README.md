# CryptoClustering
Using Unsupervised Machine Learning to predict if cryptocurrencies are affected by 24-hour or 7-day price changes.

## Tools & Modules Used
1. Python
   - Pandas
   - sklearn
2. Jupyter Notebook


## Steps Taken to Complete
The following steps are broken down by the following points
- Preparing the Data
- Finding the Best Value for k Using the Original Scaled DataFrame
- Creating Clusters with K-means Using the Original Scaled Data
- Optimizing Clusters with Principal Component Analysis (PCA)
- Finding the Best Value for k Using the PCA Data
- Creating Clusters with K-means Using the PCA Data

### Preparing the Data
* Using the StandardScaler() module from scikit-learn I normalize the data from the CSV file.
* Created a DataFrame with the scaled data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
* The first five rows of the scaled DataFrame appear as follows:
  ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/e1d25e20-6bcc-4a42-b1ac-f413d637b98b)

### Finding the Best Value for k Using the Original Scaled DataFrame
Using the elbow method I find the best value for k using the following steps:
* Created a list with the number of k values from 1 to 11.
* Created an empty list to store the inertia values.
* Created a for loop to compute the inertia with each possible value of k.
* Created a dictionary with the data to plot the elbow curve.
* Plotted a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.
  ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/da6f9279-4679-4630-b861-b5bc97dd060a)

*  question: What is the best value for k?:
   *  After comparing both the elbow curve and the numerical values in the dataframe representing the elbow curves, it appears that a cluster size of 4 is likely the most suitable choice.

### Creating Clusters with K-means Using the Original Scaled Data
Used the following steps to cluster the cryptocurrencies for the best value for k on the original scaled data:
* Initialized the K-means model with the best value for k.
* Fit the K-means model using the original scaled DataFrame.
* Predicted the clusters to group the cryptocurrencies using the original scaled DataFrame.
* Created a copy of the original data and added a new column with the predicted clusters.
* Created a scatter plot using hvPlot as follows:
  * Set the x-axis as "PCA1" and the y-axis as "PCA2".
  * Colored the graph points with the labels found using K-means.
  * Added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.
    ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/3546a04b-4b71-4c04-aa9c-2789f89fde78)

### Optimizing Clusters with Principal Component Analysis (PCA)
* Using the original scaled DataFrame, I performed PCA and reduced the features to three principal components.

* Retrieved the explained variance ratio to determine how much information can be attributed to each principal component

* question :What is the total explained variance of the three principal components?
   * The cumulative explained variance for the reduced 3 columns amounts to approximately 0.895, indicating an accuracy rating of around 90% for the PCA-transformed data.
  
* Created a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.

* The first five rows of the PCA DataFrame appear as follows:
  ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/bb12b144-dbd2-48aa-8de5-4b14dc332879)

### Finding the Best Value for k Using the PCA Data
Using the elbow method on the PCA data I find the best value for k using the following steps:

* Created a list with the number of k-values from 1 to 11.
* Created an empty list to store the inertia values.
* Created a for loop to compute the inertia with each possible value of k.
* Created a dictionary with the data to plot the Elbow curve.
* Plotted a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.
  ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/ade7d1cc-1bdb-4edf-9d32-f05472c0ef4a)

* question: What is the best value for k when using the PCA data?
   * Judging from the elbow plot of the PCA-transformed data, it appears that a cluster count of 4 would be a suitable choice.
  
* question: Does it differ from the best k value found using the original data?
   * In fact, there is no difference, as we both have a total of 4 clusters

### Creating Clusters with K-means Using the PCA Data
Used the following steps to cluster the cryptocurrencies for the best value for k on the PCA data:

* Initialized the K-means model with the best value for k.
* Fit the K-means model using the PCA data.
* Predicted the clusters to group the cryptocurrencies using the PCA data.
* Created a copy of the DataFrame with the PCA data and added a new column to store the predicted clusters.
* Created a scatter plot using hvPlot as follows:
  * Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
  * Colored the graph points with the labels found using K-means.
  * Added the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.
    ![image](https://github.com/Jaynav04/CryptoClustering/assets/130405173/c132ebf4-50f8-4c48-81cd-530be54519c3)

* question: What is the impact of using fewer features to cluster the data using K-Means?
   * Using fewer features to analyze clusters can have many impacts.
        - The main advantages are 
        1. the increase of computational speed to analyze my original data. 
        2. is more visually appealing as the features of dimensiality are reduced
        - Disadvantages 
        1. Can be inaccurate so there is always a potential for loss of information
        2. Its difficult to understand what columns are data are useful or not and if you use the summarization of all columns there could be some soret             of biased clustering.
