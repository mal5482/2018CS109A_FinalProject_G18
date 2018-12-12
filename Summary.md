[Introduction](https://mal5482.github.io/ADNI-Alzheimer-Project/index)   |   [Literature Review](https://mal5482.github.io/ADNI-Alzheimer-Project/Review)   |   [EDA](https://mal5482.github.io/ADNI-Alzheimer-Project/EDA)   |   [Models](https://mal5482.github.io/ADNI-Alzheimer-Project/Models)   |   [**Results and Discussion**](https://mal5482.github.io/ADNI-Alzheimer-Project/Summary)   |   [Conclusion](https://mal5482.github.io/ADNI-Alzheimer-Project/Conclusion)   |   [Reference](https://mal5482.github.io/ADNI-Alzheimer-Project/Reference)

# Results and Discussion
---
## Contents
* [1. Summary](#summary)<br>
* [2. Results](#results)<br>
* [3. Discussion](#discussion)<br> 
---

## <a name="summary"></a> 1. Summary
**<p>In our project, we first select potential predictors based on both literature review and EDA results. Then we built eight classification models to predict the baseline diagnosis status of an individual given his predictors patterns. For each model, we used three different imputation methods: directly drop missing, mean imputation, and regression imputation. We also tried two types of regularization, Ridge and Lasso. We selected our best prediction model based on the performance on test set.</p>**

## <a name="results"></a> 2. Results

```py
# create summary table
models_name = ['Multinomial Logistic Regression','LDA','QDA','k-NN','Decision Tree','Bagging','Random Forest','AdaBoost']
iterables = [models_name, labels]
mindex = pd.MultiIndex.from_product(iterables, names=['Models', 'Imputation Method'])
summary_df = pd.DataFrame(index=mindex)

train_accs = [logi_accs_train, lda_accs_train, qda_accs_train, knn_accs_train, 
                             dt_accs_train, bag_accs_train, rf_accs_train, ada_accs_train]
test_accs = [logi_accs_test, lda_accs_test, qda_accs_test, knn_accs_test, 
                             dt_accs_test, bag_accs_test, rf_accs_test, ada_accs_test]
train_acc_array = []
test_acc_array = []

for i in range(8):
    for j in range(3):
        train_acc_array.append(train_accs[i][j])
        test_acc_array.append(test_accs[i][j])

summary_df['Training Accuracy'] = train_acc_array
summary_df['Test Accuracy'] = test_acc_array

```
![summary table](/images/stable.png)


## <a name="discussion"></a> 3. Discussion
