Analysis: The best performing Model was Logistic Regression, tuned with GridSearchCV scoring = 'recall' to prioritize minimizing false-negative detections The Selected Hyper-parameters were: {'classifier': LogisticRegression(max_iter=1000, random_state=42), 'classifier__C': 10, 'classifier__penalty': 'l2'}
Accuracy: 0.97
Classification Report:
              precision    recall  f1-score   support

           0       0.99      0.97      0.98        71
           1       0.95      0.98      0.97        43

    accuracy                           0.97       114
   macro avg       0.97      0.97      0.97       114
weighted avg       0.97      0.97      0.97       114

This only mis-classified one benign tumor as Malignant. 



