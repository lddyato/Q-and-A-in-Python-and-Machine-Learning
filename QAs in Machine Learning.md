# Q1: xgb.cv and GridSearchCV

<https://stackoverflow.com/questions/43542317/xgboost-early-stopping-cv-versus-gridsearchcv>

I have the same issue with XGboost ignoring num_boost_rounds (when early stopping is specified) and continuing to fit. I would wager that this is a bug.

As for the advantages of early stopping over GridSearchCV:

The advantage is that you don't have to try a series of values for num_boost_rounds, but you automatically stop at the best.

Early stopping is designed to find the optimum number of boosting iterations. If you specify a very large number for num_boost_round (i.e. 10000) and the best number of trees turns out to be 5261 it will stop at 5261+early_stopping_rounds, giving you a model that is pretty close to the optimum.

If you wanted to find the same optimum using GridSearchCV without early stopping rounds you would have to try many different values of num_boost_rounds (i.e. 100,200,300,...,5000,5100,5200,5300,...etc...). This would take a much longer time.

The property that early stopping is exploiting is that there is an optimal number of boosting steps after which the validation error while start to increase. So ....

why doesn't it work for your case?

impossible to say precisely without having the data, but it is probably because of a combination of the following:

num_boost_round is too small (and you run into the bug where xgboost resets and starts over, creating an neverending loop)
early_stopping_rounds is too large (maybe your data has a strongly oscillating convergence behavior. Try a smaller value and see whether the CV error is good enough)
something might be strange about your validation data
Why are you seeing different results between GridSearchCV and xgboost.cv?

Difficult to tell without having a fully working example, but have you checked all the default values for the variables that you only specify in one of the two interfaces (like 'reg_alpha':0, 'reg_lambda':1, 'objective': 'reg:linear', 'booster':'gblinear') and whether your definition of RMSE exactly matches xgboost's definition?

# Q2: xgb.train vs xgb.XGBClassifier()

#Q3: accuracy_score, recall_score, roc_curve, roc_auc_score, confusion_matrix
## accuracy_score
分类准确率分数是指所有分类正确的百分比。分类准确率这一衡量分类器的标准比较容易理解，但是它不能告诉你响应值的潜在分布，并且它也不能告诉你分类器犯错的类型。
形式：
`sklearn.metrics.accuracy_score(y_true, y_pred, normalize=True, sample_weight=None)`
normalize：默认值为True，返回正确分类的比例；如果为False，返回正确分类的样本数
```
>>>import numpy as np  
>>>from sklearn.metrics import accuracy_score  
>>>y_pred = [0, 2, 1, 3]  
>>>y_true = [0, 1, 2, 3]  
>>>accuracy_score(y_true, y_pred)  
0.5  
>>>accuracy_score(y_true, y_pred, normalize=False)  
2  
```
## recall_score
