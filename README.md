# k-NN Regression

# Model description

The k-NN algorithm is a non-parametric method whose input consists of the k-closest training examples in the feature space. Each training example has a property value in a numerical form associated with the given training example.

 The k-NN algorithm uses all training sets to predict a property value for the given test sample.
 This predicted property value is an average of the values of its k nearest neighbors. If k is 1, then the test sample is simply assigned to the property value of a single nearest neighbor.

# k - a number of nearest neighbors
#### distanceMeasure - one of the distance metrics provided by the ML framework such as Euclidean, Hamming or Manhattan
####  KNNStrategy - could be SIMPLE or WEIGHTED (it enables a weighted k-NN algorithm)
#### datasetBuilder - helps to get access to the training set of objects for which the class is already known.
 
## Seprating independent and dependent variable and coverting them into array form for fasten the conputation. We’ll be using scikit-learn to train a KNN classifier and evaluate its performance on the data set 

```python
X = dataframe.iloc[:,1:-1].values
    y = dataframe.iloc[:,-1].values
    log(file_objects," data got splited into X(independent variable) and Y ( Taregt variable)") 
```

Finally, following the above modeling pattern, we define our classifer, in this case KNN, fit it to our training data and evaluate its accuracy. We’ll be using an arbitrary K but we will see later on how cross validation can be used to find its optimal value.


```python
 knn_reg_model = KNeighborsRegressor()
 pre_CV_model = knn_reg_model.fit(X_train,y_train)
 prediction = pre_CV_model.predict(X_test)
 log(file_objects," Model prediction done")
```

Parameters
#### n_neighborsint, default='auto".
Number of neighbors to use by default for kneighbors queries.

#### weights{‘uniform’, ‘distance’} or callable, default=’auto’
weight function used in prediction. Possible values:
‘uniform’ : uniform weights. All points in each neighborhood are weighted equally.
‘distance’ : weight points by the inverse of their distance. in this case, closer neighbors of a query point will have a greater influence than neighbors which are further away.
Uniform weights are used by default.

#### algorithm{‘auto’, ‘ball_tree’, ‘kd_tree’, ‘brute’}, default=’auto’
Algorithm used to compute the nearest neighbors:
‘ball_tree’ will use BallTree
‘kd_tree’ will use KDTree
‘brute’ will use a brute-force search.
‘auto’ will attempt to decide the most appropriate algorithm based on the values passed to fit method.

#### leaf_sizeint, default='auto'
Leaf size passed to BallTree or KDTree. This can affect the speed of the construction and query, as well as the memory required to store the tree. The optimal value depends on the nature of the problem.
pint, default=2
Power parameter for the Minkowski metric. When p = 1, this is equivalent to using manhattan_distance (l1), and euclidean_distance (l2) for p = 2. For arbitrary p, minkowski_distance (l_p) is used.
#### p int, default='auto'
Power parameter for the Minkowski metric. When p = 1, this is equivalent to using manhattan_distance (l1), and euclidean_distance (l2) for p = 2. For arbitrary p, minkowski_distance (l_p) is used.

## Examples
```python
KNN_parameter = {"algorithm":["kd_tree", "brute"],
                "n_neighbors": list(range(1,30)),
                 "weights" : ["uniform","distance"],
                 "leaf_size": [5,10,15,20,25,30],
            "p": [1,2]}

```


# Problems faced when optimizing KNN code:

The main concern with optimizing the KNN classifier is to select the right number of neighbors K and the distance function to be considered.










```
