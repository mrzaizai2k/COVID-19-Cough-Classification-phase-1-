# COVID-19-Cough-Classification-phase-1

Sorry I have no `.py` file this time for you. But as usual I have my Kaggle notbook [**HERE**](https://www.kaggle.com/bomaich/covid-19-cough-classification) for you
guys to try on.

To Compensate for you, I will especially explain what I have done on this project:

## Table of contents
* [1. Dataset](#1-Dataset)
* [2. Primary features](#2-Primary-features)
* [3. Scaling data](#3-Scaling-data)
* [4. Imbalanced data](#4-Imbalanced-data)
* [5. Model](#5-Model)
* [6. K - fold cross validation](#6-K-fold-cross-validation)
* [7. Lời cảm ơn](#7-lời-cảm-ơn)
* [8. Bản quyền tập dữ liệu](#8-bản-quyền-tập-dữ-liệu)
* [9. Giấy phép](#9-giấy-phép)

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

However, SMote help a lot on the training time with early stopping

Reference: https://machinelearningmastery.com/smote-oversampling-for-imbalanced-classification/

## 5. Model
I use a simple ANN model with drop out layers (0.5) to avoid overfitting. The model here is quite simple. I prefer using CRNN + attention and a more complicated model for
2D dataset instead of 1D dataset like this. You know, it's just **phase 1!**

## 6. K fold cross validation

Here I use K-fold (Stratified k fold) with the oversampled data

After all, I think K-fold is just a method to generally assessed how good or bad the model is. Help us tune the hyperparameters better

Reference:

https://viblo.asia/p/lam-chu-stacking-ensemble-learning-Az45b0A6ZxY
https://www.machinecurve.com/index.php/2020/02/18/how-to-use-k-fold-cross-validation-with-keras/
https://github.com/SadmanSakib93/Stratified-k-fold-cross-validation-Image-classification-keras/blob/master/stratified_K_fold_CV.ipynb
https://miai.vn/2021/01/18/k-fold-cross-validation-tuyet-chieu-train-khi-it-du-lieu/





