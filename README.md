# 🧠 Wikidata Item Classification

**A machine learning system to classify Wikidata items** into culturally meaningful categories using features extracted from **Wikipedia and Wikidata**.

---

## 🗂️ Categories Defined

Each item is classified into **one of three cultural categories**:

| Category | Description |
|----------|-------------|
| 🟢 **Cultural Agnostic** | The item is commonly known or used worldwide. No culture specifically claims it. |
| 🟡 **Cultural Representative** | The item originates from or is claimed by a culture, but is also known/used across cultures or has similar counterparts. |
| 🔴 **Cultural Exclusive** | The item is only known or used within a specific culture and is strongly identified with it. |

---

## 🔍 Objective

This project aims to investigate cultural ownership and representation by automatically classifying Wikidata entities, based on features all inferred from Wikipedia and Wikidata.

---
## 📄 Paper

We encourage you to first read the paper we wrote as part of this project. You can find it in this GitHub repository under the filename `Cultural_Classification_report.pdf`

---

## 🧰 Models Overview

Two main approaches are implemented:

### 1. **Non-Transformer Models**

A modular pipeline with three distinct models:
- A **CNN model** for images found in Wikipedia pages
- A **text-based model** using item descriptions
- A **feature-based model** using structured Wikidata attributes

These are later **combined into an ensemble model** for final prediction.

### 2. **Transformer-Based Models**

Applied directly to raw text (item name, description, Wikipedia extract), using:
- **BERT**
- **DistilBERT**
- **RoBERTa**
- **DeBERTa**
- **GPT-2**

---

## 📁 Project Structure

### `01_*.ipynb` – **Data Collection**

- Extracts relevant data from Wikidata and Wikipedia (text, images, features).
- Raw data generation for each entity.

---

### `02_Cleaning_dataset.ipynb` – **Data Cleaning**

- Prepares dataset for non-transformer modeling.
- Covers missing value imputation, label correction, one-hot encoding, and more.
- Every cleaning step is **justified using training/validation metrics**.

---

### `03_Visualization.ipynb` – **Exploratory Analysis**

- Visual diagnostics of feature distributions and dataset balance.
- Includes:
  - Per-feature histograms with class overlays
  - Train vs. validation comparisons
  - Correlation heatmaps

---

### `04_Modeling_*` – **Model Training**

#### 🧱 Non-Transformer Models

- `04_Modeling_CNN`: Classifies based on item **images**
- `04_Modeling_description`: Uses **textual descriptions**
- `04_Modeling_features`: Leverages **Wikidata features**
- `04_Modeling_ensemble`: Combines the three outputs into an **ensemble classifier**

> CNN models handle missing images via either **blank placeholders** or **row exclusion**.

#### 🤖 Transformer-Based Models

- Fine-tunes popular transformer architectures on:
  - Name
  - Description
  - Wikipedia snippet (first 1000 characters)

---

### `05_Predictions.ipynb` – **Prediction & Export**

- Inputs a dataset with:
  - Wikidata URL
  - Name
  - Description
  - Category
  - Subcategory
- Outputs a CSV with **predicted cultural classification**

---

---

## 📊 Results

### A. Non-Transformer Models

#### 🧱 CNN Model (based on Wikipedia images)

| Method               | Accuracy | Recall | Precision | F1-Score |
|----------------------|----------|--------|-----------|----------|
| White Image Filling  | 51.33%   | 48.82% | 49.46%    | 46.84%   |
| Drop NaN             | 48.95%   | 46.17% | 50.07%    | 45.15%   |

#### 📝 Description-Based Models

| Method                     | Accuracy | Recall | Precision | F1-Score |
|----------------------------|----------|--------|-----------|----------|
| SpaCy + KNN                | 64.00%   | 64.71% | 63.75%    | 60.64%   |
| FastText + KNN             | 66.33%   | 67.01% | 66.73%    | 65.02%   |
| FastText + Neural Network  | 68.00%   | 68.00% | 68.13%    | 67.44%   |

#### 🔢 Feature-Based Models (using structured Wikidata attributes)

| Method              | Accuracy | Recall | Precision | F1-Score |
|---------------------|----------|--------|-----------|----------|
| Neural Network      | 75.67%   | 75.67% | 75.50%    | 75.06%   |
| Random Forest       | 74.67%   | 74.67% | 74.32%    | 74.39%   |
| XGBoost             | 74.33%   | 74.33% | 73.91%    | 74.03%   |
| Logistic Regression | 76.33%   | 76.33% | 76.44%    | 75.51%   |
| SVM                 | 73.00%   | 73.00% | 72.79%    | 72.00%   |

---

### 🤝 Ensemble Method (combining weak models)

| Method              | Accuracy | Recall | Precision | F1-Score |
|---------------------|----------|--------|-----------|----------|
| Neural Network      | 69.67%   | 69.67% | 71.26%    | 69.52%   |
| XGBoost             | 65.00%   | 65.00% | 66.92%    | 65.19%   |
| Logistic Regression | 63.33%   | 63.33% | 65.63%    | 63.80%   |
| SVM                 | 64.67%   | 64.67% | 66.82%    | 65.08%   |

---

### 🤖 Transformer Models

| Model       | Input Type                             | Accuracy | Recall | Precision | F1-Score |
|-------------|-----------------------------------------|----------|--------|-----------|----------|
| DistilBERT  | Description only                        | 69.33%   | 69.33% | 69.15%    | 68.90%   |
| DistilBERT  | Name + Description                      | 77.00%   | 77.00% | 76.63%    | 76.62%   |
| DistilBERT  | Name + Explicit Description             | 76.67%   | 76.67% | 76.48%    | 76.36%   |
| DistilBERT  | Name + Description + Wikipedia snippet  | 74.33%   | 74.33% | 74.28%    | 74.23%   |
| BERT        | Name + Description                      | 70.03%   | 70.03% | 68.60%    | 68.42%   |
| RoBERTa     | Name + Description                      | 68.69%   | 68.69% | 66.76%    | 66.78%   |
| DeBERTa     | Name + Description                      | 74.33%   | 74.33% | 73.84%    | 73.84%   |
| GPT-2       | Name + Description                      | 70.67%   | 70.67% | 71.14%    | 70.42%   |

---

### 🏆 Best Performing Models

- **Best Non-Transformer (Feature-Based)**: Logistic Regression with **76.33% accuracy**
- **Best Ensemble Model**: Neural Network with **69.67% accuracy**
- **Best Transformer**: DistilBERT (Name + Description) with **77.00% accuracy**

---
## 📬 Contact

For questions or collaboration opportunities, feel free to reach out:

- **Thomas Garnier** – [tgarnier067@gmail.com](mailto:tgarnier067@gmail.com)  
- **Thomas Chen** – [thomaschen178@gmail.com](mailto:thomaschen178@gmail.com)
- **Jedrzej Miczke** – [miczkejedrzej@gmail.com,](mailto:miczkejedrzej@gmail.com,)



