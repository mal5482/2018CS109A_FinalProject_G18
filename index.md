[**Introduction**](https://mal5482.github.io/ADNI-Alzheimer-Project/index)   |   [Literature Review](https://mal5482.github.io/ADNI-Alzheimer-Project/Review)   |   [EDA](https://mal5482.github.io/ADNI-Alzheimer-Project/EDA)   |   [Models](https://mal5482.github.io/ADNI-Alzheimer-Project/Models)   |   [Results](https://mal5482.github.io/ADNI-Alzheimer-Project/Summary)   |   [Conclusion](https://mal5482.github.io/ADNI-Alzheimer-Project/Conclusion)   |   [Reference](https://mal5482.github.io/ADNI-Alzheimer-Project/Reference)

# Introduction
---

![picture](/images/Picture3.png)
## Introduction of Alzheimer's Disease
Alzheimer’s disease (AD) is an irreversible neurodegenerative disease that results in a loss of mental function caused by the deterioration of brain tissue. Symptoms includes problems with memory, thinking and behavior.

The number of Americans living with Alzheimer's is growing fast. An estimated 5.7 million Americans of all ages have Alzheimer's in 2018, and over 96% are people older than 65 years old and approximately 200,000 individuals under age 65 who have younger-onset Alzheimer's. Alzheimer’s Disease is the only top 10 cause of death in the United States that cannot be prevented, cured or even slowed.

**Mild cognitive impairment (MCI)**, a high-risk condition for dementia, is regarded as a transitional state between **cognitive normal (CN)** and **Alzheimer’s Disease (AD)**. MCI is also classified as **early MCI (EMCI)** and **late MCI (LMCI)**. 


## Introduction of Alzheimer's Disease Neuroimaigng Initiative (ADNI) 
![picture](/images/adni.png)
ADNI is a global research study that actively supports the investigation and development of treatments that slow or stop the progression of AD. The overall goal of ADNI is to validate biomarkers for use in Alzheimer’s disease clinical treatment trials.

In this multisite longitudinal study, researchers at 63 sites in the US and Canada track the progression of AD in the human brain with **clinical**, **imaging**, **genetic** and **biospecimen biomarkers** through the process of **normal aging/cognitively normal (CN)**, **early mild cognitive impairment (EMCI)**, and **late mild cognitive impairment (LMCI)** to **dementia or AD**. 

The aim of the Alzheimer’s Disease Neuroimaging Initiative (ADNI) study is to track the progression of the disease over different disease stages. The study has **three phases**: **ADNI 1** (five years), **ADNI GO** (two years), and **ADNI 2** (five years). ADNI 1 is the earlies phase.

**The study population of our project includes participants from ADNI 1 only since our outcome of interest is baseline diagnosis.**

## Motivation of Study 
**Early diagnosis** of **AD** or **MCI** is really important in the following aspects. 

First, it could revoke the attention of patients and their family so that additional levels of care and intervention could be given. 

Second, it could help  resource allocation and save time for specific and targeted treatment.

Third, it would provide more insights on the treatment of other diseases or combination treatment since most of the AD patients are older than 65 years old and it is very likely they are simultaneously suffering other diseases.

**Therefore, the aim of this project is to build predictive model for early diagnosis using a wide range of predictors including socio-demographic, clinical, genetic, imaging characteristics, and biospecimen biomarkers.**
![picture](/images/AD.png)

## Research Question:
**How to diagnosis status at an early stage?**<br>
To be specific: to solve above question as a classification problem of classifying disease status (**normal aging/cognitively normal (CN)**, **late mild cognitive impairment (LMCI)**, and **AD**) at an early stage using different classification methods combining predictors from different domain, and compare the performance of difference models to select the optimal prediction model. 
