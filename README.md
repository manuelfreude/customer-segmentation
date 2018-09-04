# Customer segmentation along multiple dimensions
## Food wholesaler customer segmentation using pca and k-means
Source: Udacity Machine Learning Engineer Nanodegree

## Python project summary

- Explored data with visualizations and statistics, see distribution heatmap of 3 samples below
- Conducted feature engineering incl. log-transformation and pca
- Calculated customer segments with k-means and evaluated best cluster number with silhouette score

### Sample distribution heatmap, pca dimensions and customer segments visualizations

![Sample distribution](https://github.com/manuelfreude/customer-segmentation/blob/master/sample_distribution.png)

![PCA dimensions](https://github.com/manuelfreude/customer-segmentation/blob/master/pca_dimensions.png)

Following features are relevant for the first four components:
- Component 1: high in fresh and frozen food, but low levels of milk, groceries and detergents
- Component 2: especially low in fresh, frozen and delicatessen
- Component 3: high in delicatessen, but low in fresh food
- Component 4: high in frozen food, detergents paper, but low in fresh and especially not delicatessen

![Customer segments](https://github.com/manuelfreude/customer-segmentation/blob/master/customer_segments.png)

The distribution is making a clear cut between green and red points, a few green points are in the mainly red area and vice versa, which will be reality in many real-life datasets. The main separator is the pca's dimension 1. Retailers have a low score here, hotels/restaurants/cafes have a high score. This is a great customer segmentation result considering limited knowledge about the data and the business upfront.


## Getting started
In this project, I analyzed a dataset containing data on various customers' annual spending amounts (reported in monetary units) of diverse product categories for internal structure. One goal of this project is to best describe the variation in the different types of customers that a wholesale distributor interacts with. Doing so would equip the distributor with insight into how to best structure their delivery service to meet the needs of each customer.

The dataset for this project can be found on the UCI Machine Learning Repository. For the purposes of this project, the features 'Channel' and 'Region' will be excluded in the analysis — with focus instead on the six product categories recorded for customers.

## Data exploration
The data will be explored through visualizations and code to understand how each feature is related to the others. I will observe a statistical description of the dataset, consider the relevance of each feature, and select a few sample data points from the dataset which I will track through the course of this project.

### Sample selection
To get a better understanding of the customers and how their data will transform through the analysis, it is best to select a few sample data points and explore them in more detail. In the respective code block, three indices will be added that represent three customers to track. It is suggested to try different sets of samples until you obtain customers that vary significantly from one another.

### Feature relevance
One interesting thought to consider is if one (or more) of the six product categories is actually relevant for understanding customer purchasing. That is to say, is it possible to determine whether customers purchasing some amount of one category of products will necessarily purchase some proportional amount of another category of products? We can make this determination quite easily by training a supervised regression learner on a subset of the data with one feature removed, and then score how well that model can predict the removed feature.

### Visualizing feature distributions
To get a better understanding of the dataset, we can construct a scatter matrix of each of the six product features present in the data. If a feature is relevant for identifying a specific customer, then the scatter matrix may not show any correlation between that feature and the others. Conversely, if a feature is not relevant for identifying a specific customer, the scatter matrix might show a correlation between that feature and another feature in the data.


## Data preprocessing
In this section, I will preprocess the data to create a better representation of customers by performing a scaling on the data and detecting (and optionally removing) outliers. Preprocessing data is often times a critical step in assuring that results I obtain from my analysis are significant and meaningful.

### Feature scaling
If data is not normally distributed, especially if the mean and median vary significantly (indicating a large skew), it is most often appropriate to apply a non-linear scaling — particularly for financial data. One way to achieve this scaling is by using a Box-Cox test, which calculates the best power transformation of the data that reduces skewness. A simpler approach which can work in most cases would be applying the natural logarithm.

### Outlier detection
Detecting outliers in the data is extremely important in the data preprocessing step of any analysis. The presence of outliers can often skew results which take into consideration these data points. There are many "rules of thumb" for what constitutes an outlier in a dataset. Here, we will use Tukey's Method for identfying outliers: An outlier step is calculated as 1.5 times the interquartile range (IQR). A data point with a feature that is beyond an outlier step outside of the IQR for that feature is considered abnormal.

### Dimensionality reduction
When using principal component analysis, one of the main goals is to reduce the dimensionality of the data — in effect, reducing the complexity of the problem. Dimensionality reduction comes at a cost: Fewer dimensions used implies less of the total variance in the data is being explained. Because of this, the cumulative explained variance ratio is extremely important for knowing how many dimensions are necessary for the problem. Additionally, if a signifiant amount of variance is explained by only two or three dimensions, the reduced data can be visualized afterwards.

## Clustering

In this section, I will choose to use either a K-Means clustering algorithm or a Gaussian Mixture Model clustering algorithm to identify the various customer segments hidden in the data. I will then recover specific data points from the clusters to understand their significance by transforming them back into their original dimension and scale.

### Creating clusters
Depending on the problem, the number of clusters that I expect to be in the data may already be known. When the number of clusters is not known a priori, there is no guarantee that a given number of clusters best segments the data, since it is unclear what structure exists in the data — if any. However, we can quantify the "goodness" of a clustering by calculating each data point's silhouette coefficient. The silhouette coefficient for a data point measures how similar it is to its assigned cluster from -1 (dissimilar) to 1 (similar). Calculating the mean silhouette coefficient provides for a simple scoring method of a given clustering.

### Cluster visualization
Once I've chosen the optimal number of clusters for your clustering algorithm using the scoring metric above, you can now visualize the results by executing the code block. The final visualization provided should, however, correspond with the optimal number of clusters.

## Conclusion
In this final section, I will investigate ways that you can make use of the clustered data. First, I will consider how the different groups of customers, the customer segments, may be affected differently by a specific delivery scheme. Next, I will consider how giving a label to each customer (which segment that customer belongs to) can provide for additional features about the customer data. Finally, I will compare the customer segments to a hidden variable present in the data, to see whether the clustering identified certain relationships.
