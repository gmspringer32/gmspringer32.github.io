## Table of Contents

1. [SMOTE](#smote-for-when-you-have-oversampling-of-one-level-of-target-variable)
2. [ROC](#ROC-curve)

## SMOTE for when you have oversampling of one level of target variable

```python
from imblearn.over_sampling import SMOTE
from collections import Counter

counter = Counter(y_train)
print('Before resampling: ', counter)

smt = SMOTE(random_state=16)
X_train, y_train = smt.fit_resample(X_train, y_train)

counter = Counter(y_train)
print('After resampling: ', counter)
```

Before resampling:  Counter({0: 375, 1: 201})
After resampling:  Counter({1: 375, 0: 375})

This will help when you run into the problem of having an oversampling of one class that will make it so that if your model predicts all 1's then it will have 90% accuracy. This SMOTE package duplicates some of one category to even out the numbers.

## ROC curve

```python
def plot_roc_curves(X_test, models, model_names):
    plt.figure(figsize=(10,5))
    for i in range(len(models)):
        y_pred_proba = models[i].predict_proba(X_test)[::,1]
        fpr, tpr, _ = metrics.roc_curve(y_test,  y_pred_proba)
        auc = metrics.roc_auc_score(y_test, y_pred_proba)
        plt.plot(fpr,tpr,label=model_names[i]+", auc="+str(auc))
    # set the x and y axis labels
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.legend(loc=4)
    plt.show()



plot_roc_curves(X_test, [logreg, dmlp, mlp, knn, rf, xgb], 
                ['Logistic Regression', 'Default MLPClassifier', 'MLPClassifier(100,100, logistic)', 'KNeighborsClassifier', 'RandomForestClassifier', 'XGBClassifier'])
```

**How to interpret ROC curve:**

When doing classification, models will give a probability of being in each class. Then it will take a threshold (usually .5) and use the probability vs the threshold to classify. Then you take a bunch of thresholds and use that threshold against your probabilities and classify, then calculate the true positive rate and false positive rate for each threshold. 

However, this is only possible for certain models. In some models, the probability that is produced does not model the actual probability of being in a class. In rule-based models such as decision trees, it is a reflection of the distribution of classes at the leaf of the tree we reach when following the rules of the decision tree. So while the ROC curve still gives us a sense of the overall effectiveness of the model, the model does not make it's final choice of class based on the probability.


There are many ways to find the best threshold. One is to use the J-statistic or Youden's J statistic

J = Sensitivity + Specificity - 1

Sensitivity = TP / (TP + FN) = True Positive Rate (TPR) 

Specificity = TN / (TN + FP) = 1 - False Positive Rate (FPR) 

J = TPR - FPR

Youden's J statistic is the maximum value of J 

You can calculate the J-statistic for different thresholds and choose the one with the maximum value 

The threshold that maximizes J is the optimal threshold
