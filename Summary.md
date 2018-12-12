[Introduction](https://mal5482.github.io/ADNI-Alzheimer-Project/index)   |   [Literature Review](https://mal5482.github.io/ADNI-Alzheimer-Project/Review)   |   [EDA](https://mal5482.github.io/ADNI-Alzheimer-Project/EDA)   |   [Models](https://mal5482.github.io/ADNI-Alzheimer-Project/Models)   |   [**Summary**](https://mal5482.github.io/ADNI-Alzheimer-Project/Summary)   |   [Reference](https://mal5482.github.io/ADNI-Alzheimer-Project/Reference)

# Summary

**1. Results of previous classification models:**

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

|   Models    |   Imputation Method    |   Training Accuracy    |    Test Accuracy   |
|-------|-------|-------|----------|
|                                      |  Drop Missing    |       |       |
|  Multinomial Logistic Regression     |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  LDA                                 |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  QDA                                 |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  k-NN                                |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  Decision Tree                       |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  Bagging                             |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  Random Forest                       |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
|                                      |  Drop Missing    |       |       |
|  AdaBoost                            |  Mean Imputation   |       |       |
|                                      |  Regression Imputation     |       |       |
