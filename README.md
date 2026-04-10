# Comparison-of-Transfer-Learning-Models-for-Dog-Breed-Classification

This repository presents an **experimental comparison of transfer learning approaches for dog breed classification**. The project evaluates two different strategies built on top of pretrained convolutional neural networks:

1. **NASNet + Multilayer Perceptron (MLP)**
2. **Xception + Ensemble VotingClassifier**

Both approaches rely on **transfer learning**, where pretrained CNN models are used as **feature extractors**, reducing training cost while leveraging representations learned from large datasets such as ImageNet. The extracted features are then used by different classifiers to perform the final breed prediction.

The models are evaluated using **accuracy, precision, recall, and F1-score**, and the results are visualized through comparative plots.

---

# Project Architecture

The project is organized into several components, each responsible for a specific stage of the machine learning pipeline:

```

Dataset Collection
│
▼
Bing Image Downloader
│
▼
Image Dataset
│
▼
Feature Extraction (Transfer Learning)
├── NASNet
└── Xception
│
▼
Classifier Training
├── NASNet Features → MLP
└── Xception Features → VotingClassifier
│
▼
Evaluation Metrics
│
▼
Visualization and Results Comparison

```

---

# Repository Structure

```

.
├── images/
├── model_metrics/
├── Bing_Images
├── NASnet_VGG
├── Xception_VGG
├── Results

```

### `images/`
Contains example images, figures, and visualizations used in documentation or reports.

### `model_metrics/`
Stores the **evaluation metrics for each model configuration** in JSON format.  
These files are later loaded to generate performance comparisons and plots.

### `Bing_Images/`
This module contains the **image collection pipeline** used to download dog breed images directly from **Bing Image Search**.  
It automates dataset generation using keyword-based queries.

Responsibilities:
- Query Bing image search
- Download images for each dog breed
- Organize images into dataset folders

---

### `NASnet_VGG/`
Implements the **NASNet-based transfer learning pipeline**.

Workflow:
1. Images are passed through **NASNet pretrained on ImageNet**
2. The CNN is used as a **feature extractor (frozen layers)**
3. Extracted features are flattened
4. A **Multilayer Perceptron (MLP)** classifier is trained on the features

Pipeline:

```

Images
↓
NASNet Feature Extractor
↓
Flattened Feature Vector
↓
MLP Classifier
↓
Dog Breed Prediction

```

---

### `Xception_VGG/`
Implements the **Xception-based ensemble approach**.

Workflow:
1. Images are processed using **Xception pretrained weights**
2. CNN features are extracted and flattened
3. An **ensemble VotingClassifier** combines multiple classifiers

Typical ensemble members include:
- Logistic Regression
- Random Forest
- K-Nearest Neighbors

Pipeline:

```

Images
↓
Xception Feature Extractor
↓
Flattened Feature Vector
↓
VotingClassifier (Ensemble)
↓
Dog Breed Prediction

```

The ensemble combines predictions using **hard voting**, where the final prediction corresponds to the class predicted by the majority of models.

---

### `Results/`
Contains scripts and outputs used to **compare model performance**.

This module:
- Loads stored metrics from the `model_metrics` folder
- Generates visual comparisons such as:
  - Bar plots of metrics
  - Radar charts for model comparison
  - Overall performance summaries

These visualizations help analyze **which transfer learning strategy performs better**.

---

# Evaluation Metrics

The models are evaluated using standard classification metrics:

- **Accuracy** – overall percentage of correct predictions
- **Precision** – proportion of correct positive predictions
- **Recall** – proportion of actual positives correctly identified
- **F1-score** – harmonic mean of precision and recall

All metrics are stored in JSON format and later used for visualization.

---

# Key Concepts Used in the Project

- **Transfer Learning**
- **Feature Extraction with CNNs**
- **Ensemble Learning**
- **Multilayer Perceptrons**
- **Model Evaluation and Visualization**

---

# Summary

This project explores how **different classifiers perform when combined with transfer learning feature extractors** for image classification. By comparing **NASNet + MLP** with **Xception + VotingClassifier**, the repository demonstrates how ensemble learning and pretrained CNN features can improve classification performance while reducing computational costs compared to training deep networks from scratch.
```
