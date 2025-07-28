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

We encourage you to first read the paper we wrote as part of this project. You can find it in this GitHub repository under the filename `.pdf`

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

