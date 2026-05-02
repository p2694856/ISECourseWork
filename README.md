# Intelligent Software Engineering Tool Building Project (Bug Report Classification)

## Introduction

Bug Reports are crucial for the software development lifecycle. They help developers understand issues and prioritize problems, which improves development efficiency. This is why bug reports are considered the foundation of programming repair.

This project aims to build a tool that classifies bug reports as either performance-related (1) or non-performance-related (0). Performance-related bugs need to be fixed quickly because they can negatively impact speed and accuracy, worsening the user experience. Additionally, performance and non-performance bugs sometimes require different approaches to be resolved.

The tool utilizes a combination of feature extraction via TF-IDF and various established classification models to process and analyze data effectively.

Five datasets were provided for this report to allow for a comprehensive evaluation of the model: TensorFlow, PyTorch, Keras, MXNet, and Caffe. The data will be split 80-20 (training/testing), a standard industry practice. The goal is to improve upon at least one metric of a pre-existing model by researching and applying relevant techniques. This report will detail the chosen method, its setup, and a comparison with the baseline.

## Related Work

While there are multiple approaches to bug report classification, this project focuses on machine learning methods because they are currently the most widely used and efficient.

The baseline provided uses Naïve Bayes, a 'traditional' machine learning method. Other traditional methods include Support Vector Machines (SVM), Random Forest Decision Trees, and Logistic Regression. These are relatively easy to implement and can help determine bug severity and improve predictions.

Deep learning approaches, such as Convolutional Neural Networks and Recurrent Neural Networks, exist and tend to be more accurate. However, they are more complex and require large datasets for fine-tuning. Given the size of the provided datasets, deep learning methods were deemed too complex, time-consuming, and unnecessary for this project.

This project compares different traditional machine learning methods that utilize TF-IDF:

*   **Naïve Bayes:** A probabilistic classifier assuming feature independence. It is fast, efficient, and handles categorical data well, but relies heavily on the independence assumption and lacks flexibility.
*   **Random Forest Decision Tree:** Builds multiple decision trees and aggregates predictions through majority voting. It doesn't require linear relationships and works with both categorical and continuous data, but it's slower than other traditional methods and may require tuning.
*   **Support Vector Machines (SVM):** Finds the optimal hyperplane to separate classes. It's highly effective for high-dimensional data and flexible regarding linear vs. non-linear classification. However, it's computationally intensive (especially with large datasets) and struggles with noisy data.
*   **Logistic Regression:** A statistical model for binary classification. It's simple and efficient but mostly limited to linear classifications, struggling with complex, high-dimensional data.

## Solution, Comparison and Experimentation

To find the optimal solution, various machine learning methods were compared using the provided code as a base. Metrics were collected and visualized in a heatmap (Figure 1). Note that SVM was not implemented due to time constraints and the author's inexperience with the technique.

The heatmap (Figure 1) compares the models based on Accuracy, Precision, Recall, F1 score, and AUC.

### Processing Time

Processing time was considered as a factor. Naïve Bayes was observed to be the fastest method. Random Forest Decision Trees and Logistic Regression took significantly longer—at least three times the time required for Naïve Bayes.

### Results

The provided baseline, Gaussian Naive Bayes, was the worst performer in most metrics, except for Recall. While it outperformed other methods in Recall, the difference wasn't significant enough to justify its use, especially given its low AUC score. Therefore, all other tested methods outperformed the baseline.

A score of 70% was considered acceptable, and 85% was considered excellent, aligning with industry standards. While all methods showed good accuracy, the Random Forest Decision Tree stood out for its consistently good scores across all metrics, although its AUC was lower than the other two top performers.

Considering processing time, Multinomial Naive Bayes proved to be a strong contender. It was fast and, unlike Logistic Regression, maintained scores above 60% across the board, outperforming the Decision Tree in several areas.

### Conclusion on Methods

Both Random Forest Decision Tree and Multinomial Naive Bayes are viable methods for bug report classification. The choice depends on the specific priorities: Random Forest offers better overall performance, while Multinomial offers significantly faster processing times with acceptable performance.

## Setup

The code was built upon the provided baseline. All methods used the same TF-IDF natural language processing to ensure a fair comparison. The code was written in Python using the Kaggle IDE.

First, a dataset loader was created to average the datasets and save time (Figure 2). Then, the setup was applied to the Gaussian Naive Bayes baseline and subsequently replicated for the other methods.

The application of different methods relied on resources from GeeksforGeeks.org and Scikit-learn.org, adhering to best practices.

The code structure followed the baseline:

1.  Import required libraries
2.  Define text preprocessing methods
3.  Process a single dataset
4.  Load Datasets
5.  Output Results

The data was split 80/20 (training/test), and the process was iterated 10 times (as in the baseline) to reduce bias. Efficiency was calculated using Accuracy, Precision, Recall, F1 score, and AUC.

## Reflection

While the process was generally successful, some limitations exist. In an industry setting with larger datasets, deep learning methods would likely be more appropriate, despite the author's current lack of expertise in that area. The author relied on online resources to implement various methods rather than creating custom ones from scratch. The inability to implement SVM, which research suggests might be superior, is a significant limitation.

A key limitation of the code is the number of iterations; more iterations could further reduce bias. Additionally, future work should focus on identifying the most relevant metric specifically for bug report classification, rather than assessing all metrics equally, to improve the final solution.

## Artefact

The code repository is available at: https://github.com/p2694856/ISECourseWork

## Conclusion

The project identified two methods that outperform the provided Gaussian Naive Bayes baseline for bug report classification: Random Forest Decision Tree and Multinomial Naive Bayes.

The Random Forest Decision Tree provides well-rounded performance scores but is significantly slower. The Multinomial Naive Bayes model is much faster and achieves a better AUC score, with its other metrics remaining competitive. The final choice depends on whether the user prioritizes performance (Random Forest) or processing speed (Multinomial).
