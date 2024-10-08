# Capstone
A hands-on project to predicting whether a tumor is Malignant or Benign. I compare the performance of the following classifiers: k-nearest neighbors, logistic regression, decision trees, and support vector machines. I also explore potential Clustering techniques. This is the Capstone project for the UC Berkeley AI/ML Professional Certificate.

Detailed Analysis can be found in the Jupyter notebook

## Data
The data is sourced from  kaggle: https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data

The Zip file is linked in the "Data" folder of this project

The classification goal is to predict whether a tumor is Malignant from a series of numeric measurements.

## Processing
The Target variable was mapped such that "Malignant" = 1, and "Benign" = 0

Standard scalar was applied to all numeric features. 

I used a test/train split for an initial investigation, and then 5-fold Cross Validation for tuning the hyper-parameters of the models. 

I used both Gaussian Mixture Modelling and DBSCAN to add clustering to the dataset.

I also explored Polynomial Feature combinations to give the model more expressive power. The summary is that polynomial combination of degree 2 outperformed the raw data, and polynomial combinations of degree 3 showed some signs of over-fitting, particularly in the D-tree model. 


## Evaluation

Recall (Sensitivity): This metric measures how well our model identifies actual cases of malignant tumors. High recall means that our model successfully detects most of the true malignant cases. If recall is low, it indicates that our model is making Type II errors — misclassifying malignant tumors as benign. This is a significant risk, as missing a true case of cancer can lead to delayed treatment and severe health consequences for the patient.

Precision: This metric focuses on how accurate our model's positive predictions are. It tells us the proportion of cases predicted as malignant that are actually malignant. While precision is important, the consequence of a false positive (Type I error) is usually further testing, which, although inconvenient and costly, is less harmful than failing to detect a malignant tumor.

In medical diagnostics, recall is the priority. Minimizing Type II errors is critical because the cost of missing a malignant tumor is much higher than the cost of a false alarm. A model with high recall ensures that nearly all true cases are flagged for further investigation, reducing the risk of undiagnosed or untreated cancer. Therefore, for our diagnostic model, it is strategically more valuable to optimize for recall, even at the expense of some precision, to ensure that we catch as many true malignant cases as possible.

## Algorithms
This project considers 4 algorithms:
- K-nearest neighbors
- Logistic regression
- Decision trees
- Support vector machines (SMV)

## Tuning

After completing the initial analysis to baseline model performance, I ran a GridSearch to further refine these models and find the optimal hyper parameters. The details of the optimal weights are available in the Notebook, but here are the highlights: 

The best performing Combinations of Features was Degree 2 PolyFeatures without including Clustering.This organization produced the following recall

- SVM - Mean Recall from 5-Fold CV: 0.9623
- Random Forest - Mean Recall from 5-Fold CV: 0.9625
- Logistic Regression - Mean Recall from 5-Fold CV: 0.9575
- KNeighborsClassifier - Mean Recall from 5-Fold CV: 0.9386

SVM outperformed the other best approaches by having a higher accuracy ( Lower False Positive rate) which is a secondary metric to compare these classifiers.

## Confusion Matrices

As mentioned above, we are primarily concerned not with overall accuracy but with Minimizing the False Negative detections. In the Confusion Matrices below, "FN" is in the bottom left corner of each plot, showing the number of instances that were Malignant but mis-classified as Benign.

Many more detailed Confusion Matrices are availble in the analysis Notebook, here we only need consider best performing model: 

![Confusion Matrix](Images/Confusion_matrices.png)

## Feature Importance
Although the strictly best model (SMV) does not have an easy way to view feature importance. LogisticRegression performed nearly as well on Recall (our top metric) and comparably on accuracy, with the significant added benefit of being able to interpret top features. This model demonstrates that the column texture_worst is the most important individual measurement, appearing both by itself and in combination with many other features. 

Here is a chart
![Feature Importance](Images/LogReg_feature_importance.png)

The RandomForest model identified different top features, which are visible below
![Feature Importance](Images/Dtree_Features.png)

RandomForest Identifies a more diverse set of points, all linear combinations. 

## Conclusion
- The best trade off in Model Performance was the Degree = 2 PolynomialFeatures without clustering labels applied. This model had a Mean Recall from 5-Fold CV of 0.9623. This number would likely need to be improved in order to deploy this model in a real-world medical context.
  
- Logistic Regression and RandromForest performed just as well in Recall department, but slightly worse in accuracy. These models are much easier to interpret, giving us legible feature scores. It's very clear from the top 10 feature values for the Logistic model  that texture_worst is the most important singular feature. If interperitability were a key goal, Logistic Regression Model Or RandomForest may be superior choice.
  

## Possible Continuations
- I was surprised and disappointed that I was unable to use clustering to improve the model performance. Theoretically this should be possible. Additional experimentation with hyper parameters, as well as potentially reducing the dimensionality could yield valuable results 
- The biggest flaw in this dataset was simply its size. With targets of recall so high for the realworld application, It's hard to imaging exceeding 99% accuracy without a larger dataset.
- Ensemble Techniques like XGBoost, Gradient Boosting Machines, or Random Forest might help with further reducing False Negatives
- Expanding the ParamGrid to search a broader space for potentially more optimal hyper-perameters.
- Additional work to reduce or remove some features could create an opportunity to reduce the cost or time of testing required to detect cancer. At this point, my model is not powerful enough to provide such insights. 

