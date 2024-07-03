# Red Wine Quality Analysis

Welcome to this Jupyter Notebook where we delve into the red wine quality analysis using statistical inference and regression modeling. In this exploration, we aim to uncover the factors that influence the perceived quality of red wines based on physicochemical properties.

## Goals

Our primary goal is to build an explanatory model for our dataset. By employing statistical methods and regression techniques, we seek to:
- Identify which physicochemical variables significantly influence wine quality.
- Interpret the impact of these variables on the perceived quality of red wines.
- Validate our findings through statistical analysis and model evaluation.

## Dataset

We obtained the dataset from [Kaggle](https://www.kaggle.com/datasets/uciml/red-wine-quality-cortez-et-al-2009/data), where it is openly available for research and educational purposes. The dataset consists of 1599 observations, each representing a unique red wine sample.

### Features

The dataset contains the following columns:

- `fixed acidity`: Tartaric acid content in wine. Tartaric acid itself has a sour taste, but wines with higher levels of tartaric acid tend to have a crisper and more refreshing acidity. This acidity is crucial for balancing the wine's flavors and providing structure. Typical value range is 4-6 g/l.

- `volatile acidity`: Acetic acid content in wine. Acetic acid imparts a sharp, vinegar-like sourness to wine when present in higher amounts. While a small amount of acetic acid can contribute to wine complexity, higher concentrations are generally undesirable and considered a flaw. Typical value range is 0.5-0.8 g/l. EU limit is 1.3 g/l.

- `citric acid`: Citric acid content in wine. When present in appropriate amounts, it contributes positively to the sensory characteristics and stability of wine. It adds a bright acidity that can enhance fruit flavors and freshness, contributing to a well-balanced and enjoyable wine experience. Typical value range is 0.2-0.5 g/l.

- `residual sugar`: Residual sugar content in wine. Residual sugar plays a significant role in shaping the taste, mouthfeel, and overall style of wine. Its presence can range from imperceptible in dry wines to pronounced in sweet wines. Typical value range depends on the dryness of the wine. Dry wines may have 0 g/l and sweet ones 25+ g/l.

- `chlorides`: Chloride content in wine. Chlorides in wine contribute to its taste complexity, sensory balance, and overall quality. While they typically contribute positively when present in appropriate amounts, monitoring and managing chloride levels are important to achieve desired flavor profiles and ensure wine quality. Typical value range is 0.02-0.3 g/l. Most places regulate at 0.5 g/l as a maximum allowed value.

- `free sulfur dioxide`: Free sulfur dioxide content in wine. Free sulfur dioxide is a critical component in winemaking for its preservative and protective qualities. When managed properly, it contributes positively to the wine's aroma, flavor preservation, and overall quality, ensuring that the wine reaches consumers in a stable and enjoyable condition.

- `total sulfur dioxide`: Total sulfur dioxide content in wine. While both free and total SO₂ measurements involve sulfur dioxide in wine, they serve different purposes in winemaking. Free SO₂ is the active preservative and antioxidant, while total SO₂ gives a complete assessment of all forms of SO₂ present, including those that are bound and not immediately active in preserving the wine. According to regulations in the EU, this value should not be over 350 g/l.

- `density`: Density of wine. Density measurements are used as quality indicators in wine production and analysis. They can help assess fermentation completeness, potential alcohol levels, and sometimes indicate the presence of residual sugars or other abnormalities.

- `pH`: pH value of wine. pH is a fundamental factor in wine chemistry that affects taste, microbial stability, color, and overall quality. Typical value range is 3.3-3.8.

- `sulphates`: Potassium sulphate content in wine. Potassium sulfate in wine primarily contributes potassium as a nutrient for yeast and potentially impacts pH and SO₂ levels.

- `alcohol`: Alcohol content of wine. Alcohol content is a critical component of wine that impacts its flavor, body, aging potential, and overall consumer experience.

- `quality`: Quality rating of the wine (score between 0 and 10).

Each row in the dataset represents a unique red wine sample with its corresponding physicochemical properties and quality rating.

## Data Cleaning and Preprocessing

### Handling Duplicates

Even though the dataset description mentions 1599 unique wine entries, there are 240 instances where the data is exactly the same (potentially differing only by brand, although this information is unavailable). Therefore, we are dropping these duplicate rows as they do not provide additional insights.

### Outlier Detection and Treatment

To identify outliers, we used two methods: Z-score and visual graphs. We found several outliers in both free sulfur dioxide and total sulfur dioxide. However, since the maximum value of these outliers is under 300 and the regulated maximum value is 350, we retained these data points.

### Standardization

Because we will try to perform regression, value ranges have a strong influence on our coefficient values. For example, fixed acidity will influence our model more than citric acid due to the huge gap in value ranges. For this reason, we standardized our dataset.

### Correlation Analysis

We considered a strong positive correlation when the value is >=0.67 and a strong negative correlation when the value is <-0.67. In our heatmap, we observed several strong correlations that guided our feature selection process.

### Multicollinearity Inspection

We used the variance inflation factor (VIF) to check for multicollinearity. Initially, some features had VIF values >5, indicating multicollinearity issues. After dropping less important features, our VIF values were all below 5.

## Model Building

We built our regression model using the significant features: volatile acidity, fixed acidity, and alcohol content. The high F-statistic combined with a minimal change in R-squared suggests that the removed predictors were not contributing meaningful explanatory power but were likely adding noise, reducing the model's overall statistical significance.

## Future Research

- Correct transformation of citric acid could lead to its inclusion into the model.
- Experimenting with different combinations of features could lead to better variability explanation.
- More in-depth EDA could help find other useful features.
- Using more sophisticated methods could help transform features to a true standard distribution, improving the model.
- Trying polynomial or other non-linear models could improve final results.

## Conclusion

In this analysis, we identified the key physicochemical properties that significantly influence the quality of red wine. Through extensive data cleaning, outlier treatment, and transformation, we ensured our data met the assumptions required for regression modeling. Our final model highlighted volatile acidity, fixed acidity, and alcohol content as the most impactful factors on wine quality. By focusing on these core features, we built a statistically robust model that provides clear insights into the attributes that enhance the sensory perception of red wine.