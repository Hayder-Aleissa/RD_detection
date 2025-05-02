
# Pneumonia Detection from Chest X-ray Images using Traditional Machine Learning

## Project Overview

This project explores the use of traditional machine learning techniques to classify chest X-ray images as either normal or showing signs of pneumonia. The objective is to evaluate whether handcrafted features and classical models can achieve results comparable to deep learning approaches, particularly in resource-constrained environments.

## Motivation

- **Medical Significance**: Pneumonia is a serious respiratory disease that can be detected through chest radiographs. Automated classification can improve diagnostic efficiency and reduce workload on radiologists.
- **Computational Efficiency**: Deep learning models are effective but computationally expensive. This project aims to identify lightweight machine learning alternatives.
- **Comparative Analysis**: The performance of traditional models is compared against a CNN baseline to assess their viability.

## Dataset

We used the publicly available [Chest X-ray Images (Pneumonia) dataset](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia). It contains labeled images in two classes:
- `NORMAL`: Healthy chest X-rays
- `PNEUMONIA`: X-rays showing infection

The dataset was split into training, validation, and testing sets with a 70:15:15 ratio.

## Methodology

### 1. Dataset Preparation

- All images were renamed consistently.
- Data was divided into `train`, `val`, and `test` subsets.
- A parallel structure was created to evaluate performance on both raw and preprocessed images.

### 2. Preprocessing

Each image in the "processed" subset underwent the following enhancement steps:
- Grayscale conversion
- Contrast enhancement using CLAHE
- Noise reduction with bilateral filtering
- Normalization using OpenCV’s `normalize`

### 3. Feature Extraction

A comprehensive set of radiological features was extracted, including:

- **Intensity Statistics**: Mean, standard deviation, skewness, kurtosis
- **Histogram Percentiles**: 25th, 50th, and 75th percentile intensities
- **Edge Features**: Canny edge statistics and density
- **Contour Descriptors**: Area, perimeter, and circularity
- **Texture Features**: GLCM (contrast, energy, correlation, etc.) and Local Binary Patterns (LBP)
- **Frequency Domain Features**: Derived from the magnitude spectrum of the FFT
- **Corner Detection**: Harris corner count
- **HOG Descriptors**: Truncated for computational efficiency

### 4. Class Balancing

To address the imbalance (more pneumonia cases), we used:
- Data augmentation on the minority class
- SMOTE (Synthetic Minority Over-sampling Technique)
- Class weighting in certain classifiers

### 5. Classification

Several machine learning models were trained and evaluated:
- Logistic Regression
- Logistic Regression + SMOTE
- Random Forest
- Multilayer Perceptron (MLP)

Each model was trained on both the full set of handcrafted features and on PCA-reduced features for dimensionality reduction.

### 6. Evaluation

Models were evaluated using:
- Accuracy
- Precision, Recall, F1-Score (for each class)
- AUC-ROC curves (when applicable)

### 7. Deep Learning Benchmark

A Convolutional Neural Network (CNN) was trained as a performance baseline and used to assess the relative performance of traditional models.

## Results and Analysis

- **Traditional ML vs Deep Learning**: The best traditional model (MLP with feature engineering) achieved an accuracy of 94.66%, while the CNN achieved 97.27%, a difference of just 2.61%.
- **Effect of Preprocessing**: Preprocessing significantly improved model performance. MLP benefited the most.
- **Effectiveness of Feature Engineering**: The handcrafted features successfully captured key diagnostic patterns in the X-ray images.
- **SMOTE Utility**: SMOTE improved logistic regression performance by approximately 1.3%.
- **Model Efficiency**: Simpler models like logistic regression still achieved high accuracy (>90%), making them practical in resource-constrained settings.
- **Feature Redundancy**: PCA revealed that most variance was captured in the first few components, and additional features did not always improve performance, highlighting potential redundancy.

## Conclusion

This study confirms that with strong feature engineering, traditional machine learning approaches can achieve competitive results in medical image classification. These methods can serve as effective, low-cost alternatives to deep learning models in clinical environments where computational resources are limited.
 

## Course Information

- **Course**: ICS 483 – Computer Vision  
- **Institution**: King Fahd University of Petroleum and Minerals  
- **Term**: Second Semester, 2024–2025 (242)

## Licensing
This repository is developed as part of the KFUPM ICS 483 course (semester 242) and is intended solely for educational purposes.
