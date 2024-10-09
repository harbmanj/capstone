# Capstone
A hands-on project to comparing the performance of the following classifiers: k-nearest neighbors, logistic regression, decision trees, and support vector machines. This is the Capstone project for the UC Berkeley AI/ML Professional Certificate.

Detailed Analysis can be found in the Jupyter notebook

## Data
The data is sourced from  kaggle: https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data

The Zip file is linked in the "Data" folder of this project

The classification goal is to predict whether a tumor is Malignant from a series of measurements taken 

## Processing
The Target variable was mapped such that "Malignant" = 1, and "Benign" = 0

Standard scalar was applied to all numeric features. 

I used a test/train split for an initial investigation, and then 5-fold Cross Validation for tuning the hyper-parameters of the models. 

I used both Gaussian Mixture Modelling and DBSCAN to add clustering to the dataset.

I also explored Polynomial Feature combinations to give the model more expressive power. The summary is that polynomial combination of degree 2 outperformed the raw data, and polynomial combinations of degree 3 showed some signs of over-fiitting, particularly in the D-tree model. 


## Evaluation

Recall (Sensitivity): This metric measures how well our model identifies actual cases of malignant tumors. High recall means that our model successfully detects most of the true malignant cases. If recall is low, it indicates that our model is making Type II errors — misclassifying malignant tumors as benign. This is a significant risk, as missing a true case of cancer can lead to delayed treatment and severe health consequences for the patient.

Precision: This metric focuses on how accurate our model's positive predictions are. It tells us the proportion of cases predicted as malignant that are actually malignant. While precision is important, the consequence of a false positive (Type I error) is usually further testing, which, although inconvenient and costly, is less harmful than failing to detect a malignant tumor.

In medical diagnostics, recall is the priority. Minimizing Type II errors is critical because the cost of missing a malignant tumor is much higher than the cost of a false alarm. A model with high recall ensures that nearly all true cases are flagged for further investigation, reducing the risk of undiagnosed or untreated cancer. Therefore, for our diagnostic model, it is strategically more valuable to optimize for recall, even at the expense of some precision, to ensure that we catch as many true malignant cases as possible.

## Algorithms
This project reviews 4 algorithms:
- K-nearest neighbors
- Logistic regression
- Decision trees
- Support vector machines (SMV)

## Tuning

After completing the initial analysis to baseline model performance, I ran a GridSearch to further refine these models and find the optimal hyper parameters. The details of the optimal weights are available in the Notebook, but here are the highlights: 

- Best cross-validated accuracy for LogisticRegression: 0.9141
- Best cross-validated accuracy for SVC: 0.9104
- Best cross-validated accuracy for DecisionTreeClassifier: 0.9056
- Best cross-validated accuracy for KNeighborsClassifier: 0.9022

While all of the models improved, LogisticRegression overtook SVC for the top-spot.

## Confusion Matrixes

For this application, there is not a high cost for either flase positive or false negatives. However, it is still interesting to check the confusion matrices. It could be possible for two models with comparable accuracies to present very different error types. On marginal calls like this one (91.4% accuracy for LogisticRegression and 91.0% accuracy for SVC), business considerations might prefer one type of error over the other. For example, if we were concerned about maximing the productivity of our calls, we might be willing to take the trade of slightly lower overall accuracy for slightly higher precision. Conversely, if we had a limited list of potential customers to call, we might be more concerned about over-looking some "yes" responses and prefer higher recall. Here the Confusion Matrixes do not show much variation in error types
![Confusion Matrix](Images/DTree_Confusion.png)
![Confusion Matrix](Images/KN_Confusion.png)
![Confusion Matrix](Images/SVC_Confusion.png)
![Confusion Matrix](Images/LogReg_Confusion.png)

## Feature Importance
Interpretting the Feature Importance of the Logistic Regression model can be tricky. Here are the outputs for the top 10 most impactful features: 


Here is a chart
![Feature Importance](Images/LinReg_Feature_Importance.png)



## Conclusion

## Possible Continuations

