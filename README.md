Data Preprocessing contains the following:  
Includes  
Reading data  
Preparing dataframe  
Getting raw X and y  
Processing y  
	y: Postal code regions  
		save  
	y: Geo regions  
		save  
	y: If city is big or not  
		save  
X from simple NLP models application  
	processed X: TF-IDF X processing  
		save  
	processed X: Word2Vec + PCA  
		Word2Vec  
		PCA  
		SVD
		save  
Model check  
	X = ...  
	y = ...  
	Bayes  
	XGboost  

This notebook is the result of some research conducted on how to preprocess data, form new labels and apply NLP models in the task of zipCode prediction on the GrandDébat dataset  
This notebook contains some instruments and parameters (like, for example, SVD compression degree) for you to be able to further get better results  
Ready-to-go results of the label extraction and NLP models application can be downloaded from the /output folder  
