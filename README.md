- [What to find in this repository](#what-to-find-in-this-repository)
- [Machine learning basics](#machine-learning-basics)
  - [Supervised learning](#supervised-learning)
  - [Unsupervised learning](#unsupervised-learning)
  - [Clustering](#clustering)   
  - [Classification](#classification)    
  - [k-Fold Cross-Validation (CV)](#k-fold-cross-validation-cv)
- [scikit-learn python library](scikit-learn-python-library)  
  - [requirements](#requirements)  
  - [installation](#installation)  
- [Machine learning demo with Python (iris flowers classification)](machine-learning-demo-with-python-iris-flowers-classification)
  - [iris flowers data set](#iris-flowers-data-set)  
  - [Load the dataset](#load-the-dataset)
  - [Examine the dataset](#examine-the-dataset)
  - [measure the performance of prediction](#measure-the-performance-of-prediction)
    - [split randomly the data set into a train and a test subset](#split-randomly-the-data-set-into-a-train-and-a-test-subset)
    - [Select an algorithm](#select-an-algorithm)
    - [Fit the model](#fit-the-model)
    - [Evaluate the trained model performance](#evaluate-the-trained-model-performance)
    - [Use k-Fold Cross-Validation to better evaluate the trained model performance](#use-k-Fold-cross-validation-to-better-evaluate-the-trained-model-performance)

# What to find in this repository

Machine learning hello world demo with Python

# Machine learning basics 

## Supervised learning  

The machine learning algorithm learns on a labeled dataset

## Unsupervised learning

The machine learning uses unlabeled dataset.

## Clustering

Clustering uses unsupervised learning.  
Clustering creates regions in space without being given any labels.  
Clustering divides the data points into groups, such that data points in the same group are more similar to other data points in the same group and dissimilar to the data points in other groups.  Groups are basically a collection of data points based on their similarity  

k-means clustering and DBSCAN are unsupervised clustering machine learning algorithms.
They group the data that has not been previously labelled, classified or categorized.

## Classification 

Classification categorizes data points into the desired class.  
There is a distinct number of classes.  
Classes are sometimes called targets, labels or categories    

Takes as input a training set and output a classifier which predict the class for any new data point  

Classification uses supervised learning.  
The machine learning algorithm learns on a labeled dataset  
We know the labels from the training set 

## k-Fold Cross-Validation (CV)

CV can be used to test a model. It helps to estimate the model performance.  
It gives an indication of how well the model generalizes to unseen data.  
CV uses a single parameter called k.  
It works like this:  
it splits the dataset into k groups.  
For each unique group:
- Take the group as a test data set
- Take the remaining groups as a training data set
- Use the on the training set to build the model, and then use the test set and evaluate
Example:
A dataset 6 datapoints: [0.1, 0.2, 0.3, 0.4, 0.5, 0.6]  
The first step is to pick a value for k in order to determine the number of folds used to split the dataset.  
Here, we will use a value of k=3.  
so we split the dataset into 3 groups.  
each group will have an equal number of 2 observations.

For example:  
Fold1: [0.5, 0.2]  
Fold2: [0.1, 0.3]  
Fold3: [0.4, 0.6]  
Three models are built and evaluated.  
Model1: Trained on Fold1 + Fold2, Tested on Fold3  
Model2: Trained on Fold2 + Fold3, Tested on Fold1  
Model3: Trained on Fold1 + Fold3, Tested on Fold2  

# scikit-learn python library  

Scikit-Learn, also known as sklearn, is Python general-purpose machine learning library  
Scikit-Learn is very versatile. 

## Requirements 
sklearn requires python 3  

## Installation  
```
pip3 install sklearn
```

# Machine learning demo with Python (iris flowers classification)  

The demo is about iris flowers classification.  
We will use this example [accuracy_of_SVC.py](accuracy_of_SVC.py)  

##  iris flowers data set  

We will use the iris flowers data set.    
It has data to quantify the morphologic variation of Iris flowers of three related species.  
The iris dataset consists of measurements of three types of Iris flowers: Iris Setosa, Iris Versicolor, and Iris Virginica.  

The iris dataset is intended to be for a supervised machine learning task because it has labels.  
It is a classification problem: we are trying to determine the flower categories.  
This is a supervised classification problem.  

The dataset contains a set of 150 records under five attributes: petal length, petal width, sepal length, sepal width and species.  

The data set consists of 50 samples from each of three species of Iris (Iris setosa, Iris virginica and Iris versicolor).  
Four features were measured from each sample: the length and the width of the sepals and petals, in centimeters.  
Based on the combination of these four features, we can distinguish the species  

Classes: 3  
Samples per class: 50  
Samples total: 150  
Dimensionality: 4  


## Load the dataset

```
>>> from sklearn.datasets import load_iris
>>> iris=load_iris()
```
it returns a kind of dictionary. 

## Examine the dataset

### shape  
It has 150 rows and 4 columns
```
>>> iris.data.shape
(150, 4)
```
### data attribute 
the data to learn
```
>>> iris["data"]
array([[5.1, 3.5, 1.4, 0.2],
       [4.9, 3. , 1.4, 0.2],
       [4.7, 3.2, 1.3, 0.2],
       [4.6, 3.1, 1.5, 0.2],
       [5. , 3.6, 1.4, 0.2],
       [5.4, 3.9, 1.7, 0.4],
       [4.6, 3.4, 1.4, 0.3],
       [5. , 3.4, 1.5, 0.2],
       [4.4, 2.9, 1.4, 0.2],
       [4.9, 3.1, 1.5, 0.1],
       [5.4, 3.7, 1.5, 0.2],
       [4.8, 3.4, 1.6, 0.2],
       [4.8, 3. , 1.4, 0.1],
       [4.3, 3. , 1.1, 0.1],
       [5.8, 4. , 1.2, 0.2],
       [5.7, 4.4, 1.5, 0.4],
       [5.4, 3.9, 1.3, 0.4],
       [5.1, 3.5, 1.4, 0.3],
       [5.7, 3.8, 1.7, 0.3],
       [5.1, 3.8, 1.5, 0.3],
       [5.4, 3.4, 1.7, 0.2],
       [5.1, 3.7, 1.5, 0.4],
       [4.6, 3.6, 1. , 0.2],
       [5.1, 3.3, 1.7, 0.5],
       [4.8, 3.4, 1.9, 0.2],
       [5. , 3. , 1.6, 0.2],
       [5. , 3.4, 1.6, 0.4],
       [5.2, 3.5, 1.5, 0.2],
       [5.2, 3.4, 1.4, 0.2],
       [4.7, 3.2, 1.6, 0.2],
       [4.8, 3.1, 1.6, 0.2],
       [5.4, 3.4, 1.5, 0.4],
       [5.2, 4.1, 1.5, 0.1],
       [5.5, 4.2, 1.4, 0.2],
       [4.9, 3.1, 1.5, 0.2],
       [5. , 3.2, 1.2, 0.2],
       [5.5, 3.5, 1.3, 0.2],
       [4.9, 3.6, 1.4, 0.1],
       [4.4, 3. , 1.3, 0.2],
       [5.1, 3.4, 1.5, 0.2],
       [5. , 3.5, 1.3, 0.3],
       [4.5, 2.3, 1.3, 0.3],
       [4.4, 3.2, 1.3, 0.2],
       [5. , 3.5, 1.6, 0.6],
       [5.1, 3.8, 1.9, 0.4],
       [4.8, 3. , 1.4, 0.3],
       [5.1, 3.8, 1.6, 0.2],
       [4.6, 3.2, 1.4, 0.2],
       [5.3, 3.7, 1.5, 0.2],
       [5. , 3.3, 1.4, 0.2],
       [7. , 3.2, 4.7, 1.4],
       [6.4, 3.2, 4.5, 1.5],
       [6.9, 3.1, 4.9, 1.5],
       [5.5, 2.3, 4. , 1.3],
       [6.5, 2.8, 4.6, 1.5],
       [5.7, 2.8, 4.5, 1.3],
       [6.3, 3.3, 4.7, 1.6],
       [4.9, 2.4, 3.3, 1. ],
       [6.6, 2.9, 4.6, 1.3],
       [5.2, 2.7, 3.9, 1.4],
       [5. , 2. , 3.5, 1. ],
       [5.9, 3. , 4.2, 1.5],
       [6. , 2.2, 4. , 1. ],
       [6.1, 2.9, 4.7, 1.4],
       [5.6, 2.9, 3.6, 1.3],
       [6.7, 3.1, 4.4, 1.4],
       [5.6, 3. , 4.5, 1.5],
       [5.8, 2.7, 4.1, 1. ],
       [6.2, 2.2, 4.5, 1.5],
       [5.6, 2.5, 3.9, 1.1],
       [5.9, 3.2, 4.8, 1.8],
       [6.1, 2.8, 4. , 1.3],
       [6.3, 2.5, 4.9, 1.5],
       [6.1, 2.8, 4.7, 1.2],
       [6.4, 2.9, 4.3, 1.3],
       [6.6, 3. , 4.4, 1.4],
       [6.8, 2.8, 4.8, 1.4],
       [6.7, 3. , 5. , 1.7],
       [6. , 2.9, 4.5, 1.5],
       [5.7, 2.6, 3.5, 1. ],
       [5.5, 2.4, 3.8, 1.1],
       [5.5, 2.4, 3.7, 1. ],
       [5.8, 2.7, 3.9, 1.2],
       [6. , 2.7, 5.1, 1.6],
       [5.4, 3. , 4.5, 1.5],
       [6. , 3.4, 4.5, 1.6],
       [6.7, 3.1, 4.7, 1.5],
       [6.3, 2.3, 4.4, 1.3],
       [5.6, 3. , 4.1, 1.3],
       [5.5, 2.5, 4. , 1.3],
       [5.5, 2.6, 4.4, 1.2],
       [6.1, 3. , 4.6, 1.4],
       [5.8, 2.6, 4. , 1.2],
       [5. , 2.3, 3.3, 1. ],
       [5.6, 2.7, 4.2, 1.3],
       [5.7, 3. , 4.2, 1.2],
       [5.7, 2.9, 4.2, 1.3],
       [6.2, 2.9, 4.3, 1.3],
       [5.1, 2.5, 3. , 1.1],
       [5.7, 2.8, 4.1, 1.3],
       [6.3, 3.3, 6. , 2.5],
       [5.8, 2.7, 5.1, 1.9],
       [7.1, 3. , 5.9, 2.1],
       [6.3, 2.9, 5.6, 1.8],
       [6.5, 3. , 5.8, 2.2],
       [7.6, 3. , 6.6, 2.1],
       [4.9, 2.5, 4.5, 1.7],
       [7.3, 2.9, 6.3, 1.8],
       [6.7, 2.5, 5.8, 1.8],
       [7.2, 3.6, 6.1, 2.5],
       [6.5, 3.2, 5.1, 2. ],
       [6.4, 2.7, 5.3, 1.9],
       [6.8, 3. , 5.5, 2.1],
       [5.7, 2.5, 5. , 2. ],
       [5.8, 2.8, 5.1, 2.4],
       [6.4, 3.2, 5.3, 2.3],
       [6.5, 3. , 5.5, 1.8],
       [7.7, 3.8, 6.7, 2.2],
       [7.7, 2.6, 6.9, 2.3],
       [6. , 2.2, 5. , 1.5],
       [6.9, 3.2, 5.7, 2.3],
       [5.6, 2.8, 4.9, 2. ],
       [7.7, 2.8, 6.7, 2. ],
       [6.3, 2.7, 4.9, 1.8],
       [6.7, 3.3, 5.7, 2.1],
       [7.2, 3.2, 6. , 1.8],
       [6.2, 2.8, 4.8, 1.8],
       [6.1, 3. , 4.9, 1.8],
       [6.4, 2.8, 5.6, 2.1],
       [7.2, 3. , 5.8, 1.6],
       [7.4, 2.8, 6.1, 1.9],
       [7.9, 3.8, 6.4, 2. ],
       [6.4, 2.8, 5.6, 2.2],
       [6.3, 2.8, 5.1, 1.5],
       [6.1, 2.6, 5.6, 1.4],
       [7.7, 3. , 6.1, 2.3],
       [6.3, 3.4, 5.6, 2.4],
       [6.4, 3.1, 5.5, 1.8],
       [6. , 3. , 4.8, 1.8],
       [6.9, 3.1, 5.4, 2.1],
       [6.7, 3.1, 5.6, 2.4],
       [6.9, 3.1, 5.1, 2.3],
       [5.8, 2.7, 5.1, 1.9],
       [6.8, 3.2, 5.9, 2.3],
       [6.7, 3.3, 5.7, 2.5],
       [6.7, 3. , 5.2, 2.3],
       [6.3, 2.5, 5. , 1.9],
       [6.5, 3. , 5.2, 2. ],
       [6.2, 3.4, 5.4, 2.3],
       [5.9, 3. , 5.1, 1.8]])
```
first raw
```
>>> iris.data[0]
array([5.1, 3.5, 1.4, 0.2])
```
last raw
```
>>> iris.data[-1]
array([5.9, 3. , 5.1, 1.8])
```
Let’s say you are interested in the samples 10, 25, and 50
```
>>> iris.data[[10, 25, 50]]
array([[5.4, 3.7, 1.5, 0.2],
       [5. , 3. , 1.6, 0.2],
       [7. , 3.2, 4.7, 1.4]])
>>> 
```
### feature_names attribute
```
>>> iris["feature_names"]
['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)', 'petal width (cm)']
```
### target_names attribute 
the meaning of the labels 
```
>>> iris["target_names"]
array(['setosa', 'versicolor', 'virginica'], dtype='<U10')
>>> iris.target_names
array(['setosa', 'versicolor', 'virginica'], dtype='<U10')
>>> list(iris.target_names)
['setosa', 'versicolor', 'virginica']
```
### target attribute 
the classification labels 
```
>>> iris["target"]
array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
       0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2])
```
Let’s say you are interested in the samples 10, 25, and 50
```
>>> iris.target[[10, 25, 50]]
array([0, 0, 1])
```

## measure the performance of prediction 

To measure the performance of prediction, we will split the dataset into training and test sets.  
- The training set refers to data we will learn from.  
- The test set is the data we pretend not to know  
- We will use the test set to measure the performance of our learning   

### split randomly the data set into a train and a test subset  

X has the data to learn and Y the target
```
>>> X = iris.data
>>> Y = iris.target
```
split randomly the iris data set into a train and a test subset.  
`test_size` is a float that represent the proportion of the dataset to include in the test split.  
The test size is 50% of the whole dataset. 

```
>>> from sklearn.model_selection import train_test_split
>>> X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size=0.5)
```

X_train has the data for the train split  
y_train has the target for the train split    
X_test has the data for the test split  
y_test has the target for the test split  

X_train has the data for the train split
```
>>> X_train
array([[5.4, 3.9, 1.7, 0.4],
       [6.7, 3.1, 4.7, 1.5],
       [5.5, 2.6, 4.4, 1.2],
       [5. , 3. , 1.6, 0.2],
       [5.7, 2.8, 4.1, 1.3],
       [5.7, 2.8, 4.5, 1.3],
       [4.6, 3.6, 1. , 0.2],
       [6.3, 2.5, 4.9, 1.5],
       [7.2, 3.6, 6.1, 2.5],
       [4.8, 3.4, 1.9, 0.2],
       [5.4, 3.9, 1.3, 0.4],
       [4.4, 3.2, 1.3, 0.2],
       [5.6, 2.8, 4.9, 2. ],
       [5.4, 3.4, 1.5, 0.4],
       [6.3, 2.9, 5.6, 1.8],
       [5.1, 3.3, 1.7, 0.5],
       [5.5, 2.4, 3.8, 1.1],
       [5. , 2.3, 3.3, 1. ],
       [5. , 3.3, 1.4, 0.2],
       [6.3, 2.7, 4.9, 1.8],
       [5.1, 3.5, 1.4, 0.2],
       [5. , 3.5, 1.3, 0.3],
       [4.3, 3. , 1.1, 0.1],
       [6.1, 2.9, 4.7, 1.4],
       [5.4, 3.7, 1.5, 0.2],
       [6.5, 3. , 5.2, 2. ],
       [6.4, 2.8, 5.6, 2.1],
       [7.9, 3.8, 6.4, 2. ],
       [7. , 3.2, 4.7, 1.4],
       [5.7, 3. , 4.2, 1.2],
       [4.5, 2.3, 1.3, 0.3],
       [4.9, 3.6, 1.4, 0.1],
       [4.8, 3. , 1.4, 0.1],
       [6.5, 3.2, 5.1, 2. ],
       [5. , 3.6, 1.4, 0.2],
       [6.2, 2.8, 4.8, 1.8],
       [4.9, 2.4, 3.3, 1. ],
       [6.9, 3.1, 4.9, 1.5],
       [5.4, 3.4, 1.7, 0.2],
       [4.4, 2.9, 1.4, 0.2],
       [4.8, 3. , 1.4, 0.3],
       [6.1, 2.6, 5.6, 1.4],
       [5.6, 3. , 4.5, 1.5],
       [5. , 3.4, 1.5, 0.2],
       [6. , 2.2, 5. , 1.5],
       [6.5, 3. , 5.8, 2.2],
       [6. , 2.2, 4. , 1. ],
       [4.9, 2.5, 4.5, 1.7],
       [6.3, 2.5, 5. , 1.9],
       [6. , 2.7, 5.1, 1.6],
       [6.4, 2.7, 5.3, 1.9],
       [7.2, 3.2, 6. , 1.8],
       [6.3, 3.4, 5.6, 2.4],
       [4.7, 3.2, 1.6, 0.2],
       [7.7, 2.6, 6.9, 2.3],
       [6.9, 3.2, 5.7, 2.3],
       [7.1, 3. , 5.9, 2.1],
       [6.8, 3. , 5.5, 2.1],
       [5.1, 3.7, 1.5, 0.4],
       [5.7, 2.6, 3.5, 1. ],
       [4.7, 3.2, 1.3, 0.2],
       [6.3, 3.3, 6. , 2.5],
       [6.2, 2.2, 4.5, 1.5],
       [5.7, 4.4, 1.5, 0.4],
       [5.6, 2.9, 3.6, 1.3],
       [6.3, 2.8, 5.1, 1.5],
       [4.8, 3.1, 1.6, 0.2],
       [5.2, 4.1, 1.5, 0.1],
       [4.9, 3.1, 1.5, 0.2],
       [6. , 3.4, 4.5, 1.6],
       [6.5, 2.8, 4.6, 1.5],
       [5.1, 2.5, 3. , 1.1],
       [7.7, 3.8, 6.7, 2.2],
       [6.9, 3.1, 5.4, 2.1],
       [6.3, 2.3, 4.4, 1.3]])
```
X_test has the data for the test split
```
>>> X_test
array([[6.7, 3.3, 5.7, 2.1],
       [5.5, 4.2, 1.4, 0.2],
       [6.4, 3.2, 5.3, 2.3],
       [6.4, 2.9, 4.3, 1.3],
       [6.7, 3. , 5. , 1.7],
       [5.9, 3. , 4.2, 1.5],
       [5.5, 2.4, 3.7, 1. ],
       [5.1, 3.8, 1.6, 0.2],
       [6.5, 3. , 5.5, 1.8],
       [5.1, 3.4, 1.5, 0.2],
       [5.8, 2.8, 5.1, 2.4],
       [6.9, 3.1, 5.1, 2.3],
       [6.1, 2.8, 4. , 1.3],
       [5.8, 2.7, 5.1, 1.9],
       [7.6, 3. , 6.6, 2.1],
       [6.1, 2.8, 4.7, 1.2],
       [7.7, 2.8, 6.7, 2. ],
       [4.6, 3.2, 1.4, 0.2],
       [6. , 2.9, 4.5, 1.5],
       [6.4, 3.1, 5.5, 1.8],
       [5.6, 2.7, 4.2, 1.3],
       [4.8, 3.4, 1.6, 0.2],
       [5.7, 2.9, 4.2, 1.3],
       [5. , 3.4, 1.6, 0.4],
       [6.7, 2.5, 5.8, 1.8],
       [5.3, 3.7, 1.5, 0.2],
       [7.4, 2.8, 6.1, 1.9],
       [5.8, 2.6, 4. , 1.2],
       [6.8, 2.8, 4.8, 1.4],
       [5.6, 3. , 4.1, 1.3],
       [7.2, 3. , 5.8, 1.6],
       [6.4, 2.8, 5.6, 2.2],
       [6.6, 3. , 4.4, 1.4],
       [7.7, 3. , 6.1, 2.3],
       [5.8, 4. , 1.2, 0.2],
       [5. , 2. , 3.5, 1. ],
       [7.3, 2.9, 6.3, 1.8],
       [6.7, 3.1, 4.4, 1.4],
       [5.5, 2.3, 4. , 1.3],
       [5.5, 2.5, 4. , 1.3],
       [6.3, 3.3, 4.7, 1.6],
       [5.2, 3.5, 1.5, 0.2],
       [5.1, 3.8, 1.5, 0.3],
       [5.6, 2.5, 3.9, 1.1],
       [5. , 3.2, 1.2, 0.2],
       [4.6, 3.1, 1.5, 0.2],
       [5.2, 2.7, 3.9, 1.4],
       [6.7, 3. , 5.2, 2.3],
       [6.8, 3.2, 5.9, 2.3],
       [5. , 3.5, 1.6, 0.6],
       [5.8, 2.7, 4.1, 1. ],
       [6.1, 3. , 4.9, 1.8],
       [6.4, 3.2, 4.5, 1.5],
       [6.2, 2.9, 4.3, 1.3],
       [5.1, 3.5, 1.4, 0.3],
       [6.1, 3. , 4.6, 1.4],
       [4.4, 3. , 1.3, 0.2],
       [5.4, 3. , 4.5, 1.5],
       [5.2, 3.4, 1.4, 0.2],
       [5.9, 3. , 5.1, 1.8],
       [4.6, 3.4, 1.4, 0.3],
       [5.7, 3.8, 1.7, 0.3],
       [6.7, 3.1, 5.6, 2.4],
       [5.5, 3.5, 1.3, 0.2],
       [5.8, 2.7, 5.1, 1.9],
       [4.9, 3. , 1.4, 0.2],
       [6.6, 2.9, 4.6, 1.3],
       [5.8, 2.7, 3.9, 1.2],
       [5.1, 3.8, 1.9, 0.4],
       [4.9, 3.1, 1.5, 0.1],
       [5.9, 3.2, 4.8, 1.8],
       [5.7, 2.5, 5. , 2. ],
       [6. , 3. , 4.8, 1.8],
       [6.7, 3.3, 5.7, 2.5],
       [6.2, 3.4, 5.4, 2.3]])
```
y_train has the target for the train split
```
>>> y_train
array([0, 1, 1, 0, 1, 1, 0, 1, 2, 0, 0, 0, 2, 0, 2, 0, 1, 1, 0, 2, 0, 0,
       0, 1, 0, 2, 2, 2, 1, 1, 0, 0, 0, 2, 0, 2, 1, 1, 0, 0, 0, 2, 1, 0,
       2, 2, 1, 2, 2, 1, 2, 2, 2, 0, 2, 2, 2, 2, 0, 1, 0, 2, 1, 0, 1, 2,
       0, 0, 0, 1, 1, 1, 2, 2, 1])
```
y_test has the target for the test split
```
>>> y_test
array([2, 0, 2, 1, 1, 1, 1, 0, 2, 0, 2, 2, 1, 2, 2, 1, 2, 0, 1, 2, 1, 0,
       1, 0, 2, 0, 2, 1, 1, 1, 2, 2, 1, 2, 0, 1, 2, 1, 1, 1, 1, 0, 0, 1,
       0, 0, 1, 2, 2, 0, 1, 2, 1, 1, 0, 1, 0, 1, 0, 2, 0, 0, 2, 0, 2, 0,
       1, 1, 0, 0, 1, 2, 2, 2, 2])
```

### Select an algorithm

Support vector machines (SVM) is a set of supervised learning methods.  
Support vector classifier (SVC) is a python class capable of performing classification on a dataset.  

We will use SVC.  
This classifier will: 
- Find a linear separator. A line separating classes. A line separating (classifying) Iris setosa from Iris virginica from Iris versicolor.
- There are many linear separators: It will choose the optimal one, i.e the one that maximizes our confidence, i.e the one that maximizes the geometrical margin, i.e the one that maximizes the distance between itself and the closest/nearest data point point

From the module svm import the class SVC
```
>>> from sklearn.svm import SVC
```

Create an instance of a linear SVC
```
>>> clf = SVC(kernel='linear')
```
clf is a variable (we choosed the name clf for classifier).  

### Fit the model 

let's use the fit method with this instance.  
This method trains the model and returns the trained model  
This will fit the model according to the training data.
```    
>>> clf.fit(X_train, y_train)
```
Now, the clf variable is the fitted model, or trained model.  

### Evaluate the trained model performance 

Lets use the predict method. This method returns predictions for several unlabeled observations 
```
>>> y_pred = clf.predict(X_test)
>>> y_pred
array([2, 2, 0, 0, 2, 2, 1, 0, 1, 1, 0, 0, 2, 2, 1, 2, 1, 1, 2, 1, 2, 1,
       1, 2, 1, 0, 2, 2, 1, 1, 2, 0, 2, 1, 0, 1, 0, 0, 1, 2, 0, 1, 2, 1,
       1, 2, 1, 1, 0, 0, 0, 2, 0, 0, 0, 0, 2, 2, 0, 2, 0, 1, 0, 1, 2, 2,
       0, 1, 2, 1, 1, 0, 0, 0, 1])
```

Examine the trained model performance, comparing the predictions with the test target

```
>>> y_test
array([1, 2, 0, 0, 2, 2, 1, 0, 1, 1, 0, 0, 2, 2, 1, 2, 1, 1, 2, 1, 1, 1,
       1, 2, 1, 0, 2, 2, 1, 1, 2, 0, 2, 1, 0, 1, 0, 0, 1, 2, 0, 1, 2, 1,
       1, 2, 1, 1, 0, 0, 0, 2, 0, 0, 0, 0, 2, 2, 0, 2, 0, 1, 0, 1, 2, 2,
       0, 1, 2, 1, 1, 0, 0, 0, 1])
```
There are two mismatches
```
>>> y_pred[0]
2
>>> y_test[0]
1

```
and
```
>>> y_pred[20]
2
>>> y_test[20]
1
>>> 
```
75 samples, 2 mismatches, so 0.97333% accuracy  
```
>>> from sklearn.metrics import accuracy_score
>>> accuracy_score(y_test,y_pred)
0.9733333333333334
>>> 
```

### Use k-Fold Cross-Validation to better evaluate the trained model performance 

we will use this example [k_fold_cross_validation.py](k_fold_cross_validation.py)  
```
>>> from sklearn.model_selection import cross_val_score
>>> from sklearn import datasets
>>> from sklearn.model_selection import train_test_split
>>> from sklearn.metrics import accuracy_score
>>> from sklearn.svm import SVC
```
load the data set 
```
>>> iris = datasets.load_iris()
>>> X = iris.data
>>> y = iris.target
```
split the data set in a training set and a test set
```
>>> X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25)
```
select a model and fit it
```
>>> svc_clf = SVC(kernel = 'linear')
>>> svc_clf.fit(X_train, y_train)
```
use 10 fold cross validation to evaluate the trained model 
```
>>> svc_scores = cross_val_score(svc_clf, X_train, y_train, cv=10)
```
SVC 10 fold cross validation score
```
>>> svc_scores
array([1.        , 0.83333333, 1.        , 1.        , 1.        ,
       1.        , 1.        , 1.        , 1.        , 1.        ])
>>> 
```
SVC 10 fold cross validation mean
```
>>> svc_scores.mean()
0.9833333333333334
```
SVC 10 fold cross validation standart devaiation
```
>>> svc_scores.std()
0.04999999999999999
```
