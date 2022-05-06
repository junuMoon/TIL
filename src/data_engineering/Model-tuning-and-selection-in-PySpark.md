# Model tuning and selection in PySpark

- Logistic Regression: linear model for classification
- Hyperparameter: parameter to get a model with good parameter which gives a good prediction
- Cross Validation: a method for estimating the performance of a model on unseen data
- K-fold: split the data into k subsets
- `evals.BinaryClassifierEvaluator`: evaluate the model with given metric
- `tune.ParamGridBuilder`: build a grid of hyperparameters
    - `lr.elasticNetParam`: `0` for L2 penalty, `1` for L1 penalty
    - `lr.regParam`: `0` for no regularization, `1` for maximum regularization
- AUC: area under the ROC curve
    - ROC curve: a plot of the true positive rate against the false positive rate

```python
cv = tune.CrossValidator(estimator=lr,
               estimatorParamMaps=grid,
               evaluator=evaluator
               )

best_lr = lr.fit(training)

models = cv.fit(training)
best_lr = models.bestModel
test_results = best_lr.evaluate(test)
evaluator.evaluate(test_results)
```
