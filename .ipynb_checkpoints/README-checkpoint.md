# MNLP-project-1

# A wikidata item classification

Entity classification system that can discriminate wikidataitems into three categories: cultural agnostic, cultural representative, and cultural exclusive, based on the information from the Wikipedia and Wikidata pages of the entity

Definition of classes : 

Cultural Agnostic Item: the item is commonly known/used worldwide and no culture claims the item
Cultural Representative Item: the item is originated in a culture and/or claimed by a culture as their own, but other cultures know/use it or have similar items
Cultural Exclusive Item: the item is known/used only in a specific culture and it is claimed by that culture

2 models are developped : A non transformer approach, and a transformer based approach.

First part : Data collection
You will find in all the notebooks starting by 01_, the code to extract features, based on wikipedia and wikidata pages, for an item

Second part : Cleaning
The notebook 02_Cleaning_dataset provide functions and applications of thoses function to prepare the dataset for the modeling part. For example : fill in, cleaning, drop, convert a variable into dummy variables, correct the labels... Every choice of cleaning is justified in the notebook, thanks to the train set, and then applied to the validation set.


Third part : Visualisation
This notebook helps us visualizing the training and validation dataset. It helps us justify the use of the features we extracted, and highlight the contribution to the classification of these features. We mainly find histograms of each features, with the repartition of the class labels depending on the value of the feature. The fact that the plots are done for both train and validation set, helps us to show that our dataset might be unbalanced. At the end of the notebook, we can also find the heatmap for all the features

Fourth part : Modeling
This part is divided into 2 subparts. The first part is dedicated to the non-Tranformers approach :

First we build weak models, were each output will become the input of the ensemble model (see in second part)

- 04_Modeling_CNN : Train a CNN based on the photos available on the wikipedia pages. Choose between training on a dataset where we drop missing values, of training on filled in by white pages data

- 04_Modeling_description : Based on the text description of the item, we apply embedding and many methods for classification

- 04_Modeling_features : based on the features we extracted on wikidata, we apply ML methods to classify

Thoses three weaks models are train to predict the class of each item.

Second, we extract the logits of each weak output, and give it as input in another classification model, that we call ensemble model. We find this work in the following notebook : 04_Modeling_ensemble

Second part : The Transformers part

We apply different transformers models to differents text input. We mainly try to give as input the name, description, and 1000 first characters of the wikipedia page for each item, to models like BERT, DistillBERT, RoBERTa, DeBERTa, GPT-2.


Fifth part : Prediction

The notebook 05_Predictions take as input a dataset, composed of item (wikidata link), name, description, category and subcategory, and then output a csv file with predicted associated labels.


