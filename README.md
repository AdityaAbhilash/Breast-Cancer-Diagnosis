# Breast-Cancer-Diagnosis

In this I have made a classification model using Machine Learning to detect brest cancer. 

In this model it will classify if the cancer is malignant or benign based on the features provided.

For this we have to do the following steps:

1.Analyse the given data

2.Choose a model 

3.Prepare the model 

4.Train the model






## Python libraries 

We have to import some of the common libraries that is importhat in doing the project .

```bash
  import pandas as pd
  import seaborn as sns
  import matplotlib.pyplot as plt
  from sklearn.model_selection import train_test_split
  import numpy as np
```

## Analyse the model

first we have to find the null values 
```bash
df.isna().sum()
```
and then delete the null values and the useless columns
```bash
df=df.dropna(axis=1)
df=df.drop(['id'],axis=1)
```

Then we have to find if the data is balance or imbalance
```bash
sns.countplot(x='diagnosis',data=df)
```
this code will give a bar graph of no of malignant and benign.We can see that the data is somewhat balance.





![](data:image/png;base64,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GcIBsYMbyujRo9XU1CRJGjVqVIinAdBeHA6HOnToEPQNTNy4iB3cUCIiInT48GH7zwDMEAgE5PP5JEm1tbVavny5GhoaNHbs2BBPhnBA7OCGEx8fH+oRALSxrVu3KiUlRZIUFxenW265Rf/93/+trKys0A6GsOCwLMsK9RAAAADthe/kAQAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAImaysLOXn50uSvve972np0qUhnedKHTt2TA6HQ/v27Qv1KAAugV8XASAsVFZWKjY2NtRjXBGv16vq6molJSWFehQAl0DsAAgLXbt2DfUIVywiIkIejyfUYwD4FryNBeCaOHPmjB544AF17txZKSkpWrx4cdDxb76NVVxcrIyMDMXGxsrr9WrmzJlqaGgIes5LL70kr9erTp066e6771ZxcbG+853v2McLCwvVr18/rV27Vt/73vfkcrl07733qr6+3l4TCAT061//WsnJyerYsaPuuOMOVVZW2sdra2t1//33q2vXroqJiVGvXr20atUqSRe+jXWptQBCh9gBcE08/PDDevfdd7Vp0yZt27ZNO3fuVFVVVYvrO3TooP/4j//QwYMHtWbNGu3YsUPz5s2zj+/atUszZszQb37zG+3bt08jR47U008/fcF5PvnkE73++ut666239NZbb6msrEzPPPOMfXzevHl69dVXtWbNGv35z39Wz549NWrUKH3xxReSpEcffVQffvihtmzZosOHD2vFihUtvm11JWsBXEMWALSz+vp6Kzo62iopKbH3nTp1yoqJibF+85vfWJZlWWlpadaSJUtaPMd//dd/WYmJifb2xIkTrbvuuitozf3332+5XC57+/HHH7c6depk+f1+e9/DDz9sDRgwwLIsy2poaLCioqKs9evX28ebmpqs1NRUa9GiRZZlWdbYsWOtX/7ylxed6ejRo5Yka+/evd+6FkDocGcHQLv75JNP1NTUpEGDBtn7EhISdPPNN7f4nHfffVcjR47Ud7/7XcXFxemBBx7QqVOndObMGUnSRx99pB/96EdBz/nmtvSPt8fi4uLs7ZSUFNXU1NhzNTc368c//rF9PCoqSj/60Y90+PBhSdKDDz6okpIS9evXT/PmzVNFRUWLM1/JWgDXDrEDoN1ZlnVF6z/99FP99Kc/VXp6ul599VVVVVXpD3/4gySpubnZPqfD4fjW14mKigradjgcOn/+fND6i53n6305OTn69NNPlZ+fr5MnT2r48OGaO3fuRee+krUArh1iB0C769mzp6KiorR79257X21trf76179edP2ePXt09uxZLV68WAMHDlTv3r118uTJoDW33HKLPvjggwued6VzRUdHq7y83N7X3NysPXv26Ac/+IG9r2vXrpoyZYrWrVunpUuX6sUXX2zxnFeyFsC1wVfPAbS7zp07Kzc3Vw8//LASExPldru1YMECdehw8f/e+v73v6+zZ89q2bJlGjt2rHbt2qUXXnghaE1eXp6GDBmi4uJijR07Vjt27NCWLVsuuEtzKbGxsXrwwQf18MMPKyEhQd27d9eiRYv05ZdfKjc3V5L02GOPKTMzU7fddpsCgYDeeuutoBD6Z1eyFsC1w50dANfEc889pyFDhmjcuHEaMWKE7rjjDmVmZl50bb9+/VRcXKxnn31W6enpWr9+vYqKioLW/PjHP9YLL7yg4uJi9e3bV1u3btVvf/tbdezY8YrmeuaZZ3TPPfdo0qRJ+uEPf6iPP/5Y77zzjrp06SJJio6OVkFBgfr06aMhQ4YoIiJCJSUlFz3XlawFcO04rCt9Mx0AwtS0adP0l7/8Re+//36oRwEQRngbC8B163e/+51Gjhyp2NhYbdmyRWvWrNHzzz8f6rEAhBnu7AC4bk2YMEE7d+5UfX29brrpJuXl5WnGjBmhHgtAmCF2AACA0fiAMgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBo/w8bOKKv1AaipQAAAABJRU5ErkJggg==)




```bash
df.diagnosis = [1 if each == "M" else 0 for each in df.diagnosis]
```

THIS WILL CONVERT ALL 'M' TO 1 AND 'B' to 0.
So, in our case Malignant is 1 and Benign is 0.

## Choosing a Model

```bash
sns.pairplot(df.iloc[:,1:10],hue='diagnosis')
```
This code shows us the dependence of first 10 features plot dependent pairwise. And from that plot we can see that Classification (logistic regression model) is best suited in this case as malignant and benign cases will easily be distinguish by finding a proper decision boundry.

## Preparing the Model

We can see that  the range of various features of data.csv is different . So to make the range common we can use the below function :

```bash
def zscore_normalize(X)
```
where X is the training features.


We can split the data in training and testing data by using the following code:

```bash
X_train,X_test,Y_train,Y_test=train_test_split(X,Y,test_size=0.2,random_state=0)
```
we will use regularization to reduce overfitting.


#### The model :
```bash
def sigmoid(z)
```
where is z=w.X + b where w and b are parameters.

#### The cost function:
```bash
def cost_regularization(X,Y,w,b,lamda=0)
```
X is  features and Y is target . lamda is regularization constant.


#### To find the gradient :
```bash
def gradient_regularization(X,Y,w,b,lamda=0)
```
#### To do the whole gradient descent operation:
```bash
def gradient_descent(X,Y,w_in,b_in,alpha,num_iters,lamda=0)
```
In this w_in and b_in are random initial value of w and b.
alpha is learning rate . num_iters is the no of times we want to run the model.

#### To plot how the cost decreases with iterations :
```bash
def plot_(J_history,index,lamda=0)
```
J_history is the cost history and index is the array of no of iterations.

#### Predict if the data is Bening or Malignant.
```bash
def predict(w,b,X)
```
if we give final w,b and the testing data,if the output is 1 it is malignant and if it is 0 then benign.

#### To apply the logistic regression

##### To apply the logistic regression after dividing the data into x_train and x_test:
```bash
logidtic_regression(x_train,y_train,x_test,y_test,alpha,num_iters,lamda)
```
It will return J_history,index,w_history,b_history,w,b

##### To apply the logistic regression on the entire data set 
```bash
logidtic_regression1(x_train,y_train,alpha,num_iters,lamda)
```
It will return J_history,index,w_history,b_history,w,b

## Training the Model

#### Training the x_train and finding the accuracy of x_train and x_test and ploting the cost vs iterations :

``` bash
l=0.3
J_history,index,w_history,b_history,w,b=logidtic_regression(X_train,Y_train,X_test,Y_test,alpha=1,num_iters=5001,lamda=l)
plot_(J_history,index,l)
```
train accuracy : 99.12087912087912 %

test accuracy : 96.49122807017544 %

We now have w and b as final paremeters and we have to pass the test case in the function "zscore_normalize(X)" and then we can use the "predict" function  if we want to know if the cancer is malignant or benign (If we have all the features values of a new  patient).


#### Traing the whole model and ploting the cost vs iterations:

```bash
l=0.3
J_history_2,index_2,w_history_2,b_history_2,w_2,b_2=logidtic_regression1(X,Y,alpha=1,num_iters=5001,lamda=l)
plot_(J_history_2,index_2,l)
```
train accuracy : 98.94551845342707 %

We now have w_2 and b_2 as final paremeters and we have to pass the test case in the function "zscore_normalize(X)" and then we can use the "predict" function  if we want to know if the cancer is malignant or benign (If we have all the features values of a new  patient).

[1---> malignant 0----> benign]
