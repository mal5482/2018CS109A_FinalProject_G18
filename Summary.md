[Introduction](https://mal5482.github.io/ADNI-Alzheimer-Project/index)   |   [Literature Review](https://mal5482.github.io/ADNI-Alzheimer-Project/Review)   |   [EDA](https://mal5482.github.io/ADNI-Alzheimer-Project/EDA)   |   [Models](https://mal5482.github.io/ADNI-Alzheimer-Project/Models)   |   [**Results and Discussion**](https://mal5482.github.io/ADNI-Alzheimer-Project/Summary)   |   [Conclusion](https://mal5482.github.io/ADNI-Alzheimer-Project/Conclusion)   |   [Reference](https://mal5482.github.io/ADNI-Alzheimer-Project/Reference)

# Results and Discussion
---
## Contents
* [1. Summary](#summary)<br>
* [2. Results](#results)<br>
  * [1) Overall Performance of Models](#overall)<br>
  * [2) Performance of Models on Each Diagnosis Label](#each-label)<br>
* [3. Discussion](#discussion)<br> 
  * [1) Feature Importance](#feature-importance)<br>
  * [2) Influence of Imputation Methods](#imputation)<br>

---

## <a name="summary"></a> 1. Summary
<p> In our project, we first select potential predictors based on both literature review and EDA results. Then we built nine classification models to predict the baseline diagnosis status of an individual given his predictors patterns. For each model, we used three different imputation methods: directly drop missing, mean imputation, and regression imputation. We also tried two types of regularization, Ridge and Lasso. We selected our best prediction model based on the performance on test set.</p>

---

## <a name="results"></a> 2. Results

### <a name="overall"></a> 1) Overall Performance of Models

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

Overall, the models perform pretty well in classifying the three diagnosis status. Except for k-NN model, all other models manage to achieve a test accuracy higher than 87%, and six of them have test accuracy higher than 90%, two higher than 96%.

The model that performs best is the **random forest model** using regression imputation, max tree depth equals 4, and number of trees equals 35. It reaches a test accuracy of **96.40%**, even higher than its training accuracy.

The only other model that has a test accuracy over 96% is the **multinomial logistic regression** using drop missing imputation, and **lasso regularization**. This model set the coefficient of many predictors to zero and kept only 9 predictors. Actually, when using mean imputation and regression imputation, this model would drop one more predictor (RAVLT_learning_bl) and kept only 8 predictors.

### <a name="each-label"></a> 2) Performance of Models on Each Diagnosis Label

![Each label performance](/images/stable_each.png)

The performance of the models on **each label** is also very high, which indicates the reliability of our model.

Three of the models have worst performance in predicting CN, and five of them have worst performance in predicting AD among the three labels. This is somewhat reasonable as the number of instances of CN and AD are around a half to the number of instances of LMCI in the dataset. This may also suggest that distinguish AD from other two classes is more difficult than vise versa.

---

## <a name="discussion"></a> 3. Discussion

### <a name="feature-importance"></a> 1) Feature Importance

Multinomial logistic regression using lasso regularization, decision tree, and random forest reveal some infomation on the importance of our predictors in this classification process.

Multinomial logistic regression using lasso regularization and mean imputation/regression imputation kept 8 predictors in the model, which are: MMSE_bl, RAVLT_immediate_bl, RAVLT_perc_forgetting_bl, ADAS13_bl, CDRSB_bl, ABETA_bl_n, TAU_bl_n, Hippocampus_bl (no imputation model kept one more: RAVLT_learning_bl). Among them, the first five predictors are from neurocognitive/neuropsychological assessments; ABETA_bl_n and TAU_bl_n are from cerebrospinal fluid (CSF) biomarkers; Hippocampus_bl is from imaging data.

Single decision tree with max tree depth equals 2, 3, and 4 all kept **CDRSB_bl** as the top two nodes. **MMSE_bl** also showed up in two nodes in tree with deapth equals 3 and 4. Other three predictors showed up in the trees are TMT_PtB_Complete, MidTemp_bl, and ADAS13_bl. But they are only used once.

In random forest models, we can tell the feature importance more directly. **CDRSB_bl** has an importance bigger than 0.4 whatever imputation method and max tree depth we used. The other three important features are **MMSE_bl**, **RAVLT_immediate_bl**, and **ADAS13_bl**. **RAVLT_learning_bl** showed its importance but only in no imputation model, which corresponds to lasso regularization.

The results of these models consistently showed that **CDRSB_bl**, **MMSE_bl**, **RAVLT_immediate_bl**, and **ADAS13_bl** are predictors that play an important role in prediciting baseline diagnosis for our dataset. This also corresponds well with our finding in literature review. All these four predictors are from neurocognitive/neuropsychological assessments domain. They are tests assessing different facets of cognitive performance, including daily functional ability, severity of cognitive impairment, verbal learning and fluency, and memory.

**Our finding indicates that these tests are indeed very relevent and reliable in predicting AD. As these tests could be easily reached online or from physicians, compared to complicated examinations requiring medical instruments, this could be more helpful for individuals who want to apply early self-assessment at home.**

### <a name="imputation"></a> 2) Influence of Imputation Methods

In terms of prediction accuracy, we do not see a very strong influence of imputation methods overall. 

The largest different of accuracy between three imputation methods showed up in QDA and AdaBoost, as presented below. These two model also showed a greater discrepancy of training accuracy and test accuracy. For instance, regression imputation drives the training accuracy of AdaBoost up to 1, but the test accuracy remains 0.89. But for models that performs better, the difference between training and test accuracy are very small no matter what imputation methods we used.

![imputation](/images/imput_models.png)

Although in for some models, simply dropping missing values give us a higher test accuracy (e.g. LDA), we may still prefer mean or regression imputation. Missing values account for around 1/4 of the data in training set and 1/3 in test set, so dropping them would seriously decrease our power and may introduce overfitting problem.
