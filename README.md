# GrandDebat
This repo contains my try on Le Grand Débat National dataset classification task.  

The data contains answeres people gave alongside with the person's meta information that was collected during the political-oriented poll. I thought it would be interesting to try to predict the location of the interviewed.  
The key idea was to use as simple methods as I can to generate different sets of features and target variables.  
Mehods that made it to the final cut **TF-IDF**, **Word2Vec**, **PCA**, **SVD**.  
Checking the features viability methods was best with **XGBoost** and **Multinomial Naive Bayes**.  

#### Some statistics
* 350k rows overall
* 0.5 not NaNs
* ~50 questions
* 10e6 answers
* ~7k zipcodes

## Feature extraction
There are two sets of features that I've extracted: *X_tfidf* and *X_w2vec_svd_30_components*.  
#### X_tfidf
I found to be helpful to just apply TF-IDF in a straightforward manner, which occurred to be the most suitable for region classification. My hypothesis is that it extracts region-specific words frequency information that corresponds to the political agenda of the current region.  
#### X_w2vec_svd_30_components
The way I used W2V is the following:
* Applying the pre-trained w2vec model to get an embedding of each individual word in an answer
* Take the average of all the word embeddings
* Apply dimensionality reduction on the final features to constrain the number of parameters from the original 300 to 30.

All the algorithms were applied to the *text** list, which contained an individual answer (about 3-150 symbols long) for each person on one particular question.  

## Target extraction
The target variables I obtiabed were: *y_authorZipCodes*, *y_authorZipCode_postal_regions*, *y_authorZipCode_geo_regions*, and *y_city_binary_sizes*.  
**y_authorZipCodes**: initial zipcodes of the interviewed (~7k classes)  
**y_authorZipCode_postal_regions**: first two digits of zipcode (~100 classes)  
**y_authorZipCode_geo_regions**: zipcodes classified in 14 geographical regions (Île de France, Nord-Pas-de-Calais Picardie, Alsace Champagne-Ardenne Lorraine, ...)  

## Conclusion
The best result was obtained with **X_tfidf + y_authorZipCode_geo_regions + 
Multinomial Naive Bayes":
```text
Model accuracy: 21.43%
Random accuracy: 7.14%
```
There are a lot more that can be done with this dataset, besides applying basic methods, but even the simplest statistic analysis of the text gives accuracy 3 times higher than random on 14 classes, which is not much, but I suppose that it does a better job than the man disconnected from politics can perform.  
You can make use of this notebook for basic loading and processing data.

`output` folder contains a link to the gdrive where you can download all the dumped X and y  
`pretrained_w2v` should be filled with the pre-trained w2vec model (link is in the folder)
`Data Preprocessing and Some NLP models applied.ipynb` is the main notebook file.
