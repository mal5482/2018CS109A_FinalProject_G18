[Introduction](https://mal5482.github.io/ADNI-Alzheimer-Project/index)   |   [Literature Review](https://mal5482.github.io/ADNI-Alzheimer-Project/Review)   |   [EDA](https://mal5482.github.io/ADNI-Alzheimer-Project/EDA)   |   [Models](https://mal5482.github.io/ADNI-Alzheimer-Project/Models)   |   [**Results and Discussion**](https://mal5482.github.io/ADNI-Alzheimer-Project/Summary)   |   [Conclusion](https://mal5482.github.io/ADNI-Alzheimer-Project/Conclusion)   |   [Reference](https://mal5482.github.io/ADNI-Alzheimer-Project/Reference)

# Results and Discussion
---
## Contents
* [1. Summary](#summary)<br>
* [2. Results](#results)<br>
* [3. Discussion](#discussion)<br> 

---

## <a name="summary"></a> 1. Summary
<p> In our project, we first select potential predictors based on both literature review and EDA results. Then we built nine classification models to predict the baseline diagnosis status of an individual given his predictors patterns. For each model, we used three different imputation methods: directly drop missing, mean imputation, and regression imputation. We also tried two types of regularization, Ridge and Lasso. We selected our best prediction model based on the performance on test set.</p>

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

<p>Overall, the models perform pretty well in classifying the three diagnosis status. Except for k-NN model, all other models manage to achieve a test accuracy higher than 0.87, and six of them have test accuracy higher than 0.90, two higher than 0.96.</p>
<p>The model that performs best is the **random forest model** using regression imputation, max tree depth equals 4, and number of trees equals 35. It reaches a test accuracy of 0.9640, even higher than its training accuracy.<br>
The only other model that has a test accuracy over 0.96 is the **multinomial logistic regression** using drop missing imputation, and **lasso regularization**. This model set the coefficient of many predictors to zero and kept only 9 predictors. Actually, when using mean imputation and regression imputation, this model would drop one more predictor (RAVLT_learning_bl) and kept only 8 predictors.</p>
<p>The performance of the models on each label is also very high, which indicates the reliability of our model. The test accuracy of predicting CN, AD and LMCI is 0.97, 0.95, 0.97 respectively.</p>
<p>

## <a name="discussion"></a> 3. Discussion
