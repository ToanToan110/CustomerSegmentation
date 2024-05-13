# Introduce
Imagine we are the member of a Retail/Telcos company and we wants to fuel its growth by Data-driven approach. This Series has 6 part research about 6 core problem of business:
- Part 1: [Customer Segmentation](https://github.com/ToanToan110/CustomerSegmentation)
- Part 2: [Churn Prediction](https://github.com/ToanToan110/ChurnPrediction)
- Part 3: [Customer's Life Time Value](https://github.com/ToanToan110/CustomerLifeTimeValue)
- Part 4: [Sales Prediction](https://github.com/ToanToan110/SalesPrediction)
- Part 5: [Market ResponseModel](https://github.com/ToanToan110/MarketResponseModel)
- Part 6: [A/B Testing](https://github.com/ToanToan110/A-B-Testing)

# About this Project
Each customer has unique characteristics in terms of age, gender, income...
We can’t treat every customer the same way with the same content, same channel, same importance. They will find another option which understands them better.
So that, we need to conduct a technique of dividing customers into groups with distinct Each customer has characteristics to serve business purposes, analyze behavior, and understand customers.
Depending on the company's needs, there will be different segmentation methods, this notebook using RFM to segment.





## Prerequisites
Package: Pandas, Matplotlib, Numpy

Techniques: K-means

## Resources 
Dataset: This notebook use [Retail Dataset](https://www.kaggle.com/datasets/vijayuv/onlineretail) on Kaggle

References: 
- https://www.kaggle.com/code/adarshcgowda/new-rfmt-model-for-segmentation-1st-in-kaggle
- https://towardsdatascience.com/data-driven-growth-with-python-part-1-know-your-metrics-812781e66a5b



## Process to RFM data
### Overview dataset:

### R: The last purchase date of Customer
![Recency](https://github.com/ToanToan110/CustomerSegmentation/assets/64849001/c1e93048-5756-429c-98b5-07491d170db9)

Most customers made purchases within the last 10 days.
### F: Frequency of order of customer
![frequency](https://github.com/ToanToan110/CustomerSegmentation/assets/64849001/a68e0c7c-bdce-4c04-89dc-989e2d6bc426)

Most customers have a high purchasing frequency (less than 100 days/time).
### M: THe value (sales) that customer bring
![montaryvalue](https://github.com/ToanToan110/CustomerSegmentation/assets/64849001/5dc3034a-e463-4163-9256-25ee9792f035)

Most of customers spend 100-500$ for purchase

**Summary about this RFM data**:

Base on the RFM value, we can see this is data about a group of customers that are operating stably and regularly, with the majority concentrated in the low segments.

## Segment
### Find the method for segment
We will segment based on a customer's RFM metrics, and this is an unlabeled problem.
=> Apply unsupervised learning method.

We Apply Kmeans for this simple problem.

*But the question is "Is it reasonable to divide the customer group into how many segments?"*
In real problem, choosing the number of segment will depend on many factors such as business requirements, size of the data set,...

In this case, We use the Elbow method to answer that.

![kvalue](https://github.com/ToanToan110/CustomerSegmentation/assets/64849001/b25e5f9e-02c7-4ba2-8c4b-ce80f0650cf3)

The optimal K value is identified at the point where the graph bends like an elbow (this is show the best match value of sum square distance between data points).
We choose k = 3.

And we name these segment is High-value, middle and low-value

### Fit method
We apply Kmean model by this code:

```python
kmeans = KMeans(n_clusters=3, random_state= 0)
kmeans.fit(df)
cluster = kmeans.predict(df)
```
### Evaluate the Segmentation
There 12 high-value, 3260 middle-value and 1100 low-value customer.

![evaluate](https://github.com/ToanToan110/CustomerSegmentation/assets/64849001/413d1529-8a07-4e66-9ea3-49830f7c79d8)

We can see that there is an uneven distribution between clusters, but the common characteristics of the clusters are: the higher Revenue, lower DateRecency, lower frequency, the more value that customer brings.
