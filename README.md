# 🧠 Neural Network Stock Prediction Project

## 🚀 Overview

Welcome to the **Neural Network Stock Prediction** project! This project explores the predictive power of neural networks for predicting stock market returns, comparing it with logistic regression, and understanding the impact of outliers on model performance.

[![GitHub Repo](https://img.shields.io/badge/Visit-GitHub_Repo-181717?style=for-the-badge&logo=github)](https://github.com/devarchanadev/Neural-Network-Modeling) 
[![Dataset Source](https://img.shields.io/badge/Download-Dataset_Source-007EC6?style=for-the-badge&logo=r)](https://cran.r-project.org/web/packages/ISLR2/index.html)

## 🎯 Table of Contents
- [Project Summary](#-project-summary)
- [Business Impact](#-business-impact)
- [Insights & Recommendations](#-insights--recommendations)
- [Tools & Libraries](#-tools--libraries)
- [Data Preparation](#-data-preparation)
- [Modeling & Analysis](#-modeling--analysis)
- [Impact of Outliers](#-impact-of-outliers)
- [Results & Recommendations](#-results--recommendations)
- [Conclusion](#-conclusion)
- [Key Takeaways](#-key-takeaways)

## 📋 Project Summary

This project utilizes the `Weekly` dataset from the `ISLR2` package to predict stock return directions using a **neural network** model. The **logistic regression** model is also employed for comparison. The primary goal is to identify the best-performing model in terms of accuracy and interpretability. Additionally, the project examines how outliers influence the neural network's performance.

## 💼 Business Impact

Predicting stock market returns accurately is crucial for financial institutions, investors, and portfolio managers. This project demonstrates how different modeling approaches can be leveraged to make informed decisions, potentially leading to better investment strategies and financial gains.

| **Model**          | **Test Error**  | **Interpretability** | **Recommendation**       |
|--------------------|-----------------|----------------------|--------------------------|
| **Neural Network** | 46.83%          | Moderate              | Use for complex patterns |
| **Logistic Regression** | 40.77%     | High                  | Prefer for clear insights|

## 💡 Insights & Recommendations

- **Why Neural Networks?**  
  Neural networks can capture complex patterns and interactions between variables that simpler models might miss. However, they require careful tuning and are less interpretable.

- **Why Logistic Regression?**  
  Logistic regression is a robust, interpretable model, making it ideal for scenarios where model transparency is essential.

- **Outlier Impact**  
  Outliers can significantly distort neural network predictions. Applying shrinkage techniques can mitigate these effects and improve model generalization.

## 🛠️ Tools & Libraries

This project leverages the following tools and libraries:

- **R Programming Language** 🟦
- `neuralnet` package
- `ISLR2` package
- `ggplot2` for visualizations

```r
# Installing necessary packages
install.packages("neuralnet")
install.packages("ISLR2")
```

## 🧹 Data Preparation

The dataset was preprocessed by converting the `Direction` variable into a binary outcome (`Up = 1`, `Down = 0`). The data was then split into a training set (2/3) and a test set (1/3).

```r
# Data preparation
dats <- Weekly
dats$Direction <- ifelse(dats$Direction == "Up", 1, 0)

set.seed(123)
indis <- sample(1:nrow(dats), 2/3 * nrow(dats), replace = FALSE)
train <- dats[indis, ]
test <- dats[-indis, ]
```

## 📊 Modeling & Analysis

Models were fitted using different numbers of neurons (1 to 4) in the hidden layer. The neural network's performance was compared with logistic regression:

### 🔄 Neural Network
- Test errors ranged from **44.35% to 50.41%** depending on the number of neurons.

<img width="464" alt="Screenshot 2024-08-30 132333" src="https://github.com/user-attachments/assets/b289bc99-5958-44da-b817-72f40f3bb79d">
<img width="496" alt="Screenshot 2024-08-30 132307" src="https://github.com/user-attachments/assets/e3dfc717-de9f-4c0e-9769-a5c064968610">
<img width="474" alt="Screenshot 2024-08-30 132213" src="https://github.com/user-attachments/assets/6f44d599-460f-4ae5-926a-82b5829ecea1">
<img width="487" alt="Screenshot 2024-08-30 132102" src="https://github.com/user-attachments/assets/cd66a38a-da4c-44eb-8206-ef85bb43b176">


### 🔍 Logistic Regression
- Achieved a test error of **40.77%**, outperforming the neural network.

## ⚠️ Impact of Outliers
An outlier was introduced to evaluate its effect on model performance. Shrinkage techniques were applied to mitigate the outlier's impact, resulting in improved generalization.

```r
# Introducing an outlier
train$Lag1[sample(1:nrow(train), 1)] <- 90  # Extreme value

# Fitting the neural network with the outlier
nn_outlier <- neuralnet(Direction ~ Lag1 + Lag2 + Lag3 + Lag4 + Lag5 + Volume, data = train, hidden = 4, stepmax = 1e9)
```
## 📈 Results & Recommendations

### 🔄 Neural Network
- **Suitable for capturing complex relationships** but sensitive to outliers.

### 🔍 Logistic Regression
- **Recommended** for scenarios requiring high interpretability and lower error rates.

## 🏁 Conclusion
This project highlights the strengths and limitations of neural networks in financial modeling. While neural networks offer potential advantages in capturing complex patterns, logistic regression remains a more reliable and interpretable model in this scenario.

## 🎓 Key Takeaways

### 🎯 Model Selection Matters
- Choose models based on the specific needs of the task—**complexity vs. interpretability**.

### ⚠️ Handle Outliers with Care
- Outliers can significantly affect model performance; techniques like **shrinkage** can help.

### 🛠️ Understand Your Tools
- As a data scientist, knowing when to apply neural networks versus logistic regression is crucial for effective model deployment.
