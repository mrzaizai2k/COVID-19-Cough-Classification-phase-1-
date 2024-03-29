# COVID-19-Cough-Classification-phase-1
Check out my 2 YOUTUBE channels for more:
1. [Mrzaizai2k - AI](https://www.youtube.com/channel/UCFGCVG0P2eLS5jkDaE0vSfA) (NEW)
2. [Mrzaizai2k](https://www.youtube.com/channel/UCCq3lQ1W437euT9eq2_26HQ) (old)

This project was created to distinguish between covid and non-covid patients based on cough sound. This is a non-invasive, low-cost, and simple procedure, we may use it as a first filter before testing with PCR or other methods. In phase 1, I attempted to understand the challenges with this method, the dataset, how to deal with audio files, and for the first time, integrate SMOTE and K-fold cross validation. 

I'm sorry, but I don't have a '.py' file for you this time. But, as always, you may test on my Kaggle notebook by clicking [**HERE**](https://www.kaggle.com/bomaich/covid-19-cough-classification).

To make amends, I'll go over what I did on this project in further detail:

## Table of contents
* [1. Dataset](#1-Dataset)
* [2. Primary features](#2-Primary-features)
* [3. Scaling data](#3-Scaling-data)
* [4. Imbalanced data](#4-Imbalanced-data)
* [5. Model](#5-Model)
* [6. K - fold cross validation](#6-K-fold-cross-validation)
* [7. Result](#7-Result)

## 1. Dataset
The dataset I used here is from AICovidVN115m contest. Which includes 669 positive cases (16.45% of total) and 3399 negative cases. But I didn't extract the features 
from `.wav` file because it's not really necessary now. I tool the raw feature which had been extracted from this [repo](https://github.com/dee-ex/EE3063-SEM202-FINAL-PROJECT/tree/main/features/raw)

## 2. Primary features
The feature extracted in this project were MFCCs, Mel frequency spectrogram, chroma and those are mean value `np.mean`. 

## 3. Scaling data
>"Just to give you an example — if you have multiple independent variables like age, salary, and height; With their range as (18–100 Years), 
(25,000–75,000 Euros), and (1–2 Meters) respectively, feature scaling would help them all to be in the same range, 
for example- centered around 0 or in the range (0,1) depending on the scaling technique."

Reference: https://www.atoti.io/when-to-perform-a-feature-scaling/

## 4. Imbalanced data

As you can see, our project is imbalanced positive: 669 (16.45% of total), negative cases: 3399 There are a alot of proposed methods to solve this like: 
* Over sampling
* Undersampling
* Hybrid over and under sampling
* Gain more data
* Data augmentation (I will use it for my next Covid classification phase 2)
   * Time stretch
   * Pitch shift
   * GAIN
   * Background noise
and so on...
     
Reference: https://phamdinhkhanh.github.io/2020/02/17/ImbalancedData.html#45-thu-th%E1%BA%ADp-th%C3%AAm-quan-s%C3%A1t

In this project. I'll try resolving the imbalanced data by oversampling with SMOTE. It's a oversampling method. For me the result is not really good because they change the 
features and we don't know how they change its and if the new features were true in real life. I guess in phase 2 I will try on Gain and background noise to oversample the dataset

However, SMOTE help a lot on the training time with early stopping

Reference: https://machinelearningmastery.com/smote-oversampling-for-imbalanced-classification/

## 5. Model
I use a simple ANN model with drop out layers (0.5) to avoid overfitting. The model here is quite simple. I prefer using CRNN + attention and a more complicated model for
2D dataset instead of 1D dataset like this. You know, it's just **PHASE 1!**

## 6. K fold cross validation

Here I use K-fold (Stratified k fold) with the oversampled data

After all, I think K-fold is just a method to generally assessed how good or bad the model is. Help us tune the hyperparameters better

Reference:

https://viblo.asia/p/lam-chu-stacking-ensemble-learning-Az45b0A6ZxY

https://www.machinecurve.com/index.php/2020/02/18/how-to-use-k-fold-cross-validation-with-keras/

https://github.com/SadmanSakib93/Stratified-k-fold-cross-validation-Image-classification-keras/blob/master/stratified_K_fold_CV.ipynb

https://miai.vn/2021/01/18/k-fold-cross-validation-tuyet-chieu-train-khi-it-du-lieu/

## 7. Result 
**SORRY FOR THE PICTURE RESOLUTION** You can visit [**my Kaggle Notebook**](https://www.kaggle.com/bomaich/covid-19-cough-classification) to see it clear

**Original data**

|          | precision |    recall|  f1-score|   support|
|:--------:|:---------:|:---------:|:-------:|:-------:|
|Negative |      0.94 |     0.94  |    0.94   |    680 |
|Positive |     0.70 |     0.68  |    0.69    |   134 |
|accuracy |          |           |    0.90    | 814 |

<p align="center"><img src="result/Original_data.PNG" width="600"></p>
<p align="center"><i>Figure 1. Result with original data </i></p>

<p align="center"><img src="result/origindata_AUC.PNG" width="500"></p>
<p align="center"><i>Figure 2. AUC = 91% with original data </i></p>

**Oversampling data with SMOTE** 

|         | precision |    recall|  f1-score|   support|
|:-------:|:---------:|:---------:|:-------:|:-------:|
|Negative |      0.94 |     0.97  |    0.96   |    680 |
|Positive |     0.83 |     0.70  |    0.76    |   134  |
|accuracy |          |           |    0.93    | 814    |

<p align="center"><img src="result/oversampling.PNG" width="600"></p>
<p align="center"><i>Figure 3. Result with SMOTE </i></p>


<p align="center"><img src="result/oversamp_AUC.PNG" width="500"></p>
<p align="center"><i>Figure 4. AUC = 93% with SMOTE </i></p>

**Oversampling data and k-fold cross validation**

|         | precision |    recall|  f1-score|   support|
|:-------:|:---------:|:---------:|:-------:|:-------:|
|Negative |      0.97 |     0.96  |    0.96   |    680 |
|Positive |     0.81 |     0.84  |    0.82    |   134  |
|accuracy |          |           |    0.94    | 814    |

<p align="center"><img src="result/over_kfold.PNG" width="600"></p>
<p align="center"><i>Figure 5. Result with SMOTE and K_fold cross validation</i></p>
    
<p align="center"><img src="result/oversamp_kfold_AUC.PNG" width="500"></p>
<p align="center"><i>Figure 6. AUC = 95% with SMOTE and K_fold cross validation</i></p>

