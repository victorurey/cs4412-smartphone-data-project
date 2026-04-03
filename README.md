# Pattern Discovery in Smartphone Hardware Specifications and Design
This document aims to investigate patterns between smartphone hardware and common design decisions made by brands. It explores hardware specifications and recurring design patterns to reveal hidden patterns in smartphones today. A smartphone specification dataset is used to: (1) discover which combinations of hardware features are most associated with high-end devices and how these combinations differ from low-end devices, and (2) which hardware components frequently appear among smartphone models and how do these groupings reflect common patterns in smartphone design . Patterns are found using a combination of clustering techniques and association rule mining to reveal common hardware combinations across smartphone models.

# Dataset Documentation
* Kaggle - Smartphone Specifications Dataset - [View](https://www.kaggle.com/datasets/devgondaliya007/smartphone-specifications-dataset)

Size: 986 rows, 27 columns
File size: 170.32kB

This data set provides a comprehensive view of smartphone models and their specifications on the market today. It includes nearly 1000 different smartphone models and is useful for studying patterns between hardware specifications, pricing, and consumer buying trends. This data was collected across multiple mobile comparison and e-commerce websites to provide a wide array of phone models and their pricing.

Of these attributes, this list of variables were selected for mining: RAM (gb), Battery Capacity (mAh), Rear Camera Resolution (mp), Screen Size (in), Screen Resolution, NFC, and Rear Camera Count.

These values are normalized and standardized before being used in EDA or Clustering techniques. Values like RAM, Storage, Battery Capacity, and Camera Resolution were log transformed to reduce exponential values and their affect on the clustering. 

# Discovery Questions
My two discovery questions are as follows:
- **Which combinations of smartphone hardware features are most associated with high-end devices, and how consistently do these hardware groupings distinguish them from lower-end models?**

- **What combinations of hardware features frequently appear together across smartphone models, and how do these groupings reflect common design patterns?**


# Preprocessing 
## Missing Values
Instead of dropping all missing entries, I removed only rows missing one of the five core variables—RAM, Battery Capacity, Rear Camera Resolution, Screen Size, or Price—retaining 97.5% of the dataset for analysis.

## Outliers
Although some Price, RAM, and Battery Capacity values appeared as outliers, they corresponded to valid high-end devices and were retained to preserve the full range of smartphone specifications.



# Clustering Implementation
All three techniques used the dominant four features: RAM, Battery Capacity, Rear Camera Resolution, Storage. Z-score standardization was applied to normalize features with drastically different scales (e.g. battery-mah and screen-size). In addition, log transformations were applied to all values since one or two flagship devices had large values in some of these categories.

## K-Means
The elbow method along with silhouette scores were used to determine a k value of 2. These clusters, however, were incredibly loosely defined and all silhouette scores were essentially 0.
- Cluster 0 (High-End Devices): represents phones with higher RAM values, high storage, and better battery lives.
- Cluster 1 (Mid-Tier and Budget Devices): this cluster showed all other devices containing weaker cameras, and lower RAM and storage combinations.

## DBSCAN
I used a k-distance plot for nearest neighbors to pick a proper value for eps. This plot found that eps values had a large skew on how the algorithm would cluster the data. Small values (0.3-0.7) resulted in more than 20 clusters, medium values (0.9-1.1) resulted in around 10 clusters, and large values (1.2 or greater) resulted in a single cluster. This suggests that variances in these data variables were too small to produce distinct clustering at this scale.
- Cluster 0 (High-End Devices): represents phones with higher RAM values, high storage, and better battery lives. This cluster had the highest values across all features.
- Cluster 1 (Mid-Tier Devices): this cluster had medium values in RAM and storage, good battery, and medium-level cameras.
- Cluster 2 (High Performance-Focused Devices): this cluster showed a mix of high RAM and storage but low camera specifications. This likely represents those high-end devices that are focused on providing optimal performance and have no need to improve upon camera specifications.

## Hierarchal
I used Ward's method to calculate a linkage matrix to minimize variance within clusters. This is shown in the dendrogram plotted with the top 20 levels which shows how clustering was divided.
- Cluster 0 (Mid to High-end Devices): This cluster contained the highest values across all features, grouping all higher-end devices into this category.
- Cluster 1 (Budget Devices): This cluster had lower values in battery and camera specifications representing most budget and mid-range devices.
- Cluster 2 (Flagship Devices): this cluster contained only the best devices from the list, those with highest camera and battery life. This cluster was reserved for the best values in each variable.


# Association Rules Implementation
I used association rule mining to discover differences between high, mid, and low-end devices and the hardware components that make them out. It aims to define which combinations of hardware specs are common and how these combinations reflect design patterns across brands. Both Apriori and FP-Growth use following variables divided into 3 categories each:
- RAM (low, mid, high)
- Storage (low, mid, high)
- Battery (low, mid, high)
- Camera (low, mid, high)
- Screen Size (low, mid, high)

## Apriori
- Low end devices typically had low RAM, battery, and smaller screens
- Strong associations for low-end devices, lift above 2.1
- Mid-level devices have strong combinations of mid-range hardware
- High-end devices show weak correlations between components, less patterns in high-end hardware

## FP-Growth
- Similar in low-end, mid-level, and high-end aspects to Apriori
- Unique mid-tier pattern revealed that some devices upgrade their camera specifications while leaving RAM/storage values the same
- Again, showed that high-end devices seem to be more selective about hardware features and don't show recurrent combinations like low and mid-tiers of devices

# Conclusion
Of the three clustering methods, the hierarchical technique was the most useful in revealing tiers of devices based on features like RAM, battery, and camera quality. This separated the dataset into 3 main clusters, one for low RAM and smaller batteries, and other had greater RAM and stronger camera qualities. However, none of the forms of clustering were not clear-cut and a lot of the clustering techniques produced a single, uninformative cluster after processing the data. On the other hand, association rule mining provided much better results by revealing the combinations of hardware that contributed to these patterns in smartphone design. It showed how mid-range devices sometimes upgrade to better cameras without improving on RAM or storage specifications. 

Association rule mining through Apriori and FP-Growth were especially useful in revealing reccuring combinations of hardware features in smartphone design patterns. The strongest and most consistent combinations were in low-end devices where the highest confidence and lift values were found. These devices often had low storage, low RAM, and very rarely upgrades to medium sized screens. Most interestingly, the mid-tier results showed that there is a common pattern of upgrading camera specifications but leaving RAM and storage constant. These compromises in phone hardware are what differentiates brands and its cool to see those results take place before the high-end devices. 

Project by Victor Urey
