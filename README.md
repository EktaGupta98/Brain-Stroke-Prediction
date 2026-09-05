# 🧠 Stroke Prediction System

A machine learning-based web application that predicts the likelihood of stroke using demographic and health-related factors such as age, hypertension, heart disease, BMI, glucose level, smoking status, and work type.

The project focuses on handling the highly imbalanced stroke dataset and improving the detection of actual stroke cases using SMOTE, model comparison, recall-based evaluation, and probability threshold tuning.

---

## 🚀 Features

- Predicts stroke likelihood from user health and demographic information
- Handles highly imbalanced target classes using **SMOTE**
- Performs exploratory data analysis (EDA)
- Uses categorical encoding and numerical feature preprocessing
- Compares multiple machine learning models
- Evaluates models using **Precision, Recall, F1-score, Accuracy, ROC-AUC and PR-AUC**
- Tunes the classification probability threshold
- Provides prediction probability along with the final prediction
- Interactive web interface using **Flask**

---

## 📊 Dataset

The dataset contains demographic and health-related information of individuals.

### Features

| Feature | Description |
|---|---|
| `gender` | Gender of the individual |
| `age` | Age of the individual |
| `hypertension` | Whether the individual has hypertension |
| `heart_disease` | Whether the individual has heart disease |
| `ever_married` | Whether the individual has ever been married |
| `work_type` | Type of employment |
| `Residence_type` | Urban or Rural residence |
| `avg_glucose_level` | Average glucose level |
| `bmi` | Body Mass Index |
| `smoking_status` | Smoking category |
| `stroke` | Target variable: 0 = No Stroke, 1 = Stroke |

The dataset contains approximately **15,000 training records** and is highly imbalanced, with stroke cases representing only around **4.13%** of the training data.

---

## 🔍 Exploratory Data Analysis

Before training the models, I performed Exploratory Data Analysis to understand the dataset and identify important patterns.

### Univariate Analysis

I analyzed individual features such as:

- Age distribution
- BMI distribution
- Average glucose level
- Gender distribution
- Smoking status
- Work type
- Hypertension
- Heart disease
- Stroke class distribution

One of the most important findings was the severe class imbalance between stroke and non-stroke cases.

### Bivariate Analysis

I also analyzed the relationship between individual features and stroke.

Some important observations were:

- Stroke cases were more concentrated among older individuals.
- Individuals with hypertension showed a higher presence of stroke cases.
- Heart disease was associated with a higher occurrence of stroke.
- Higher glucose levels were observed among many stroke cases.
- Other demographic and lifestyle features also showed differences between the two classes.

These observations helped in understanding which features could contribute to the prediction task.

---

## ⚙️ Data Preprocessing & Feature Engineering

The following preprocessing steps were performed:

- Removed the `id` column because it does not provide useful predictive information.
- Cleaned the `age` feature.
- Checked and handled missing values.
- Encoded categorical variables using **One-Hot Encoding**.
- Scaled numerical features where required.
- Split the data into training and validation sets using **stratified splitting**.
- Applied preprocessing only after splitting the dataset to avoid data leakage.

---

## 🤖 Machine Learning Models

I experimented with four different machine learning algorithms:

1. **Logistic Regression**
2. **Random Forest**
3. **XGBoost**
4. **LightGBM**

These models were selected to compare a simple linear classification approach with different tree-based ensemble and boosting algorithms.

### Why these models?

- **Logistic Regression:** Provides a simple and interpretable baseline for binary classification.
- **Random Forest:** Handles non-linear relationships and combines multiple decision trees.
- **XGBoost:** A powerful gradient boosting algorithm commonly used for structured/tabular data.
- **LightGBM:** An efficient gradient boosting algorithm that performs well on large tabular datasets.

---

## ⚖️ Handling Class Imbalance with SMOTE

The dataset contains significantly fewer stroke cases than non-stroke cases.

Because of this imbalance, a model could achieve high accuracy simply by predicting most records as non-stroke.

To address this problem, I used **SMOTE (Synthetic Minority Over-sampling Technique)**.

SMOTE generates synthetic samples for the minority class instead of simply duplicating existing samples.

SMOTE was applied **only to the training data** to prevent data leakage into the validation set.

---

## 📈 Model Evaluation

Since the dataset is highly imbalanced, accuracy alone was not sufficient for evaluating the models.

I focused mainly on:

### Recall

Recall answers:

> "Out of all the people who actually had a stroke, how many did the model correctly identify?"

For this project, recall was important because false negatives are particularly important in a stroke screening scenario.

### Precision

Precision answers:

> "Out of all the people predicted as having a stroke, how many actually had a stroke?"

### F1-Score

F1-score provides a balance between precision and recall.

### Model Comparison

The main results after applying SMOTE were:

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Logistic Regression + SMOTE | 79.12% | 14.52% | **83.33%** | 24.74% |
| XGBoost + SMOTE | 88.66% | 19.05% | 53.97% | 28.16% |
| LightGBM + SMOTE | 93.27% | 25.31% | 32.54% | **28.47%** |
| Random Forest + SMOTE | 91.47% | 17.70% | 29.37% | 22.09% |

### Selected Model

I selected **Logistic Regression + SMOTE** because it achieved the highest recall among the tested models:

**Recall = 83.33%**

Since the primary objective was to identify as many actual stroke cases as possible, recall was given higher importance than accuracy.

---

## 🎯 Threshold Tuning

Normally, binary classification uses a probability threshold of **0.5**.

However, I experimented with different thresholds to understand the trade-off between precision and recall.

At a threshold of **0.5**:

- Precision: 14.52%
- Recall: 83.33%
- F1-Score: 24.74%

At a threshold of **0.7**:

- Precision: 20.63%
- Recall: 67.46%
- F1-Score: **31.60%**

I selected **0.7** because it provided a better balance between precision and recall and produced the highest F1-score among the tested thresholds.

The model therefore uses:


Probability >= 0.70 → Stroke Likely
Probability < 0.70  → Stroke Not Likely

## 👩‍💻 Author

**Ekta**

Computer Science & Artificial Intelligence

---

⭐ If you found this project useful, consider giving the repository a star!
