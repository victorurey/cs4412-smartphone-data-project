# Pattern Discovery in Smartphone Pricing and Hardware Specifications
This project aims to investigate patterns between smartphone hardware and their success on the global market. It explores pricing, hardware specification, and brand strategy to paint a broader picture of the current smartphone hardware market. A smartphone specification dataset is used to: (1) discover which combinations of hardware features are common across price tiers across leading brands, and (2) which hardware components frequently appear among the most popular phone models between brands. Patterns are found using a combination of clustering and association rules to reveal common hardware combinations across smartphones.

# Dataset Documentation
* Kaggle - Smartphone Specifications Dataset - [View](https://www.kaggle.com/datasets/devgondaliya007/smartphone-specifications-dataset)

Size: 986 rows, 27 columns
File size: 170.32kB

This data set provides a comprehensive view of smartphone models and their specifications on the market today. It includes nearly 1000 different smartphone models and is useful for studying patterns between hardware specifications, pricing, and consumer buying trends. This data was collected across multiple mobile comparison and e-commerce websites to provide a wide array of phone models and their pricing.

Of these attributes, five variables were selected for mining: 
- RAM (gb)
- Battery Capacity (mAh)
- Rear Camera Resolution (mp)
- Screen Size (in)
- Price at release

These values are normalized and standardized before being used in EDA or Clustering techniques.

# Discovery Questions
My two discovery questions are as follows:
- **What natural groupings of smartphones can be discovered based on the combinations of hardware specifications across different price tiers?**

- **What combinations of hardware features frequently appear across smartphone models from major brands?**


# Preprocessing 
## Missing Values
Instead of dropping all missing entries, I removed only rows missing one of the five core variables—RAM, Battery Capacity, Rear Camera Resolution, Screen Size, or Price—retaining 97.5% of the dataset for analysis.

## Outliers
Although some Price, RAM, and Battery Capacity values appeared as outliers, they corresponded to valid high-end devices and were retained to preserve the full range of smartphone specifications.

## Creating Tiers
Five key features—RAM, Battery Capacity, Rear Camera Resolution, Screen Size, and Price—were selected, and Price was used to categorize smartphones into low-, mid-, and high-tier devices for pattern discovery.


# Clustering Implementation
## K-Means
- Features were normalized using z-score standardization
- The elbow method was used to determine number of clusters, k = 6
## Cluster Interpretation
- Six clusters revealed natural groupings of smartphones
- Four clusters revealed solid tiers:
  - Older devices
  - Budget Oriented Devices
  - Mid Range Devices
  - High-end Flagship Devices
- Two clusters revealed potential data inconsistencies:
  - Unusually high prices
  - Large RAM values

# Key Takeaways
The EDA revealed sufficient variation in hardware specifications to support pattern discovery, identifying natural groupings of devices across pricing tiers using K-Means clustering. While some clusters may reflect outliers or data errors, the dataset provides a strong foundation for association rule mining in M3, especially once missing operating system values are populated.

Project by Victor Urey
