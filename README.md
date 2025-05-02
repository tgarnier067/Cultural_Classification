# MNLP Project 1  
## A Wikidata Item Classification

**Entity classification system** that can discriminate Wikidata items into three categories:  
- **Cultural Agnostic**  
- **Cultural Representative**  
- **Cultural Exclusive**  
Based on information extracted from the **Wikipedia and Wikidata pages** of the entity.

---

### Definition of Classes

- **Cultural Agnostic Item**:  
  The item is commonly known/used worldwide and no culture claims it.

- **Cultural Representative Item**:  
  The item originated in a culture and/or is claimed by a culture as their own, but other cultures know/use it or have similar items.

- **Cultural Exclusive Item**:  
  The item is known/used only in a specific culture and is claimed by that culture.

---

### Models Developed

Two models are developed:  
- A **non-transformer** approach  
- A **transformer-based** approach

---

## Project Structure

### 1️⃣ Data Collection

All notebooks starting with `01_` contain the code to extract features from **Wikipedia and Wikidata pages** for each item.

Input datasets : 
- [MNLP 2025 HW1] train set [PUBLIC] - train_cleaned.tsv

Output dataset : 
- dev_df_country.json
- dev_df_dates.json
- dev_df_descr_analyse.json
- dev_df_images.json
- dev_df_lang.json
- dev_with_text.json
- devset_subclass_instances.json
- train_df_country.json
- train_df_dates.json
- train_df_descr_analyse.json
- train_df_images.json
- train_df_lang.json
- train_with_text.json
- trainset_subclass_instances.json

---

### 2️⃣ Cleaning

Notebook: `02_Cleaning_dataset`  
- Provides functions and examples to prepare the dataset for NON-TRANSFORMERS modeling.  
- Tasks include: filling missing values, cleaning, dropping variables, converting a variable into dummy variables, correcting labels, etc.  
- Every cleaning choice is **justified in the notebook** using the training set, then applied to the validation set.

Input dataset : 
- dev_df_country.json
- dev_df_dates.json
- dev_df_descr_analyse.json
- dev_df_images.json
- dev_df_lang.json
- dev_with_text.json
- devset_subclass_instances.json
- train_df_country.json
- train_df_dates.json
- train_df_descr_analyse.json
- train_df_images.json
- train_df_lang.json
- train_with_text.json
- trainset_subclass_instances.json

Output dataset :
- dev_df_complete.json
- train_df_complete.json

---

### 3️⃣ Visualization

Notebook: `03_Visualization`  
- Helps visualize the training and validation datasets.  
- Demonstrates the usefulness of extracted features and highlights their contributions to classification.  
- Includes:
  - **Histograms** for each feature with class label distributions
  - **Train vs Validation comparisons** to show dataset balance
  - A **heatmap** of all features at the end

Input dataset :
- dev_df_complete.json
- train_df_complete.json

---

### 4️⃣ Modeling

#### ➤ Non-Transformer Approach

We build **three weak models**, where each output is later used as input for an ensemble model:

- `04_Modeling_CNN`  
  Trains a CNN on the images available on Wikipedia pages.  
  Option to train on a dataset with missing images dropped or filled with blank placeholders. Input dataset : train_df_images.json and dev_df_images.json

- `04_Modeling_description`  
  Uses item descriptions. Applies embedding and various classification techniques.

- `04_Modeling_features`  
  Uses extracted Wikidata features with traditional machine learning models.

All three weak models predict the item’s class.

Then, in `04_Modeling_ensemble`, we:
- Extract logits from each weak model’s output
- Feed them into an **ensemble model** for final classification

#### ➤ Transformer-Based Approach

We apply different Transformer models to various text inputs:
- Name
- Description
- First 1000 characters of the Wikipedia page

Models used include:
- **BERT**
- **DistilBERT**
- **RoBERTa**
- **DeBERTa**
- **GPT-2**

---

### 5️⃣ Prediction

Notebook: `05_Predictions`  
- Takes as input a dataset containing:
  - Wikidata link
  - Name
  - Description
  - Category
  - Subcategory  
- Outputs a CSV file with the **predicted labels**.
