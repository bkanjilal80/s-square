# Classification Model

#### By subclassing the Model class: in that case, you should define your layers in __init__ and you should implement the model's forward pass in classifier.

# Classification Model

#### By subclassing the Model class: in that case, you should define your layers in __init__ and you should implement the model's forward pass in classifier.

# Classification Model

#### By subclassing the Model class: in that case, you should define your layers in __init__ and you should implement the model's forward pass in classifier.

```python
## class ClassificationModelTuner():

def __init__(self):
        self.file_object = open('logs/classificationModelsLogs.txt', 'a+')
        self.logger_object = AppLogger()
        self.file_operation = FileOperation()
```

### Method Name: get_tuned_random_forest_classifier

```python
def get_tuned_random_forest_classifier(self, x_train, y_train):
```

Description: This method will be used to build RandomForestClassifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized RandomForestClassifier model.

A random forest is a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting. The sub-sample size is controlled with the max_samples parameter if bootstrap=True (default), otherwise the whole dataset is used to build each tree.

#### Example
```python
self.rf_parameters = {
                'max_depth': [5, 10, 15, 20, 25, None],
                'n_estimators': range(10, 500, 50),
                'criterion': ['gini', 'entropy'],
                'bootstrap': [True, False],
                'min_samples_split': range(2, 10, 1),
                'max_features': ['auto', 'log2'],
                'min_samples_leaf': range(1, 10),
                
```
##### Fitting the Model ( RandomForestClassifier)
```python
self.model = RandomForestClassifier(n_jobs=-1)
            self.model.fit(x_train, y_train)
```


###  Method Name: get_tuned_xgboost_classifier
```python
def get_tuned_xgboost_classifier(self, x_train, y_train):
```
Description: This method will be used to build XGBoost Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized XGBoost model.

####  Booster Parameters

```python
self.xg_parameters = {"n_estimators": [10, 50, 100, 200],
                                  "learning_rate": [0.05, 0.10, 0.15, 0.20, 0.25, 0.30],
                                  "max_depth": [3, 4, 5, 6, 8, 10, 12, 15, 20],
                                  "min_child_weight": [1, 3, 5, 7],
                                  "gamma": [0.0, 0.1, 0.2, 0.3, 0.4, 0.5],
                                  "colsample_bytree": [0.3, 0.4, 0.5, 0.7]
                                  }
```

##### Fitting the Model  [x_train, y_train( xgboost_classifier)]

```python
self.xgboost_model = XGBClassifier(n_jobs=-1)
self.xgboost_model.fit(x_train, y_train)
```

### Method Name: get_tuned_knn_classifier
```python
def get_tuned_knn_classifier(self, x_train, y_train):
```

Description: This method will be used to build KNearestNeighbour Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized KNearestNeighbourClassifier model.


#### Patameters

The overall parameters have been divided into 3 categories by XGBoost authors:

General Parameters: Guide the overall functioning

Booster Parameters: Guide the individual booster (tree/regression) at each step

Learning Task Parameters: Guide the optimization performed

```python
rmdsearch = RandomizedSearchCV(KNeighborsClassifier(), knn_parameters, n_iter=10, cv=10, random_state=22,
                                           n_jobs=-1)
            rmdsearch.fit(x_train, y_train)
            hyperparameters = rmdsearch.best_params_
            n_neighbors, weights, algorithm, leaf_size = hyperparameters['n_neighbors'], hyperparameters['weights'], \
                                                         hyperparameters['algorithm'], hyperparameters['leaf_size']
            model = KNeighborsClassifier(n_neighbors=n_neighbors,
                                         weights=weights,
                                         algorithm=algorithm,
                                         leaf_size=leaf_size,
                                         n_jobs=-1)
```
##### Example
```python
 knn_parameters = {'n_neighbors': [50, 100, 200, 250, 300, 350],
                              'weights': ['uniform', 'distance'],
                              'algorithm': ['ball_tree', 'kd_tree'],
                              'leaf_size': [20, 25, 30, 35, 40, 45, 50],
                              }
```

### Method Name: get_best_model
```python
 def get_best_model(self, x, y):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object

#### create best model for Random Forest

prediction using the Random Forest Algorithm

```python
self.random_forest = self.get_tuned_random_forest_classifier(train_x, train_y)
self.prediction_random_forest = self.random_forest.predict(
    test_x)
```

####  create best model for XGBoost

Predictions using the XGBoost Model

```python
train_x, test_x, train_y, test_y = train_test_split(x, y)
self.xgboost = self.get_tuned_xgboost_classifier(train_x, train_y)
self.prediction_xgboost = self.xgboost.predict(test_x)
```
### Method Name: generate_model_report

```python
def generate_model_report(self, model_object, train_x, train_y, test_x, test_y, num_classes):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object
```python
## class ClassificationModelTuner():

def __init__(self):
        self.file_object = open('logs/classificationModelsLogs.txt', 'a+')
        self.logger_object = AppLogger()
        self.file_operation = FileOperation()
```

### Method Name: get_tuned_random_forest_classifier

```python
def get_tuned_random_forest_classifier(self, x_train, y_train):
```

Description: This method will be used to build RandomForestClassifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized RandomForestClassifier model.

A random forest is a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting. The sub-sample size is controlled with the max_samples parameter if bootstrap=True (default), otherwise the whole dataset is used to build each tree.

#### Example
```python
self.rf_parameters = {
                'max_depth': [5, 10, 15, 20, 25, None],
                'n_estimators': range(10, 500, 50),
                'criterion': ['gini', 'entropy'],
                'bootstrap': [True, False],
                'min_samples_split': range(2, 10, 1),
                'max_features': ['auto', 'log2'],
                'min_samples_leaf': range(1, 10),
                
```
##### Fitting the Model ( RandomForestClassifier)
```python
self.model = RandomForestClassifier(n_jobs=-1)
            self.model.fit(x_train, y_train)
```


###  Method Name: get_tuned_xgboost_classifier
```python
def get_tuned_xgboost_classifier(self, x_train, y_train):
```
Description: This method will be used to build XGBoost Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized XGBoost model.

####  Booster Parameters

```python
self.xg_parameters = {"n_estimators": [10, 50, 100, 200],
                                  "learning_rate": [0.05, 0.10, 0.15, 0.20, 0.25, 0.30],
                                  "max_depth": [3, 4, 5, 6, 8, 10, 12, 15, 20],
                                  "min_child_weight": [1, 3, 5, 7],
                                  "gamma": [0.0, 0.1, 0.2, 0.3, 0.4, 0.5],
                                  "colsample_bytree": [0.3, 0.4, 0.5, 0.7]
                                  }
```

##### Fitting the Model  [x_train, y_train( xgboost_classifier)]

```python
self.xgboost_model = XGBClassifier(n_jobs=-1)
self.xgboost_model.fit(x_train, y_train)
```

### Method Name: get_tuned_knn_classifier
```python
def get_tuned_knn_classifier(self, x_train, y_train):
```

Description: This method will be used to build KNearestNeighbour Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized KNearestNeighbourClassifier model.


#### Patameters

The overall parameters have been divided into 3 categories by XGBoost authors:

General Parameters: Guide the overall functioning

Booster Parameters: Guide the individual booster (tree/regression) at each step

Learning Task Parameters: Guide the optimization performed

```python
rmdsearch = RandomizedSearchCV(KNeighborsClassifier(), knn_parameters, n_iter=10, cv=10, random_state=22,
                                           n_jobs=-1)
            rmdsearch.fit(x_train, y_train)
            hyperparameters = rmdsearch.best_params_
            n_neighbors, weights, algorithm, leaf_size = hyperparameters['n_neighbors'], hyperparameters['weights'], \
                                                         hyperparameters['algorithm'], hyperparameters['leaf_size']
            model = KNeighborsClassifier(n_neighbors=n_neighbors,
                                         weights=weights,
                                         algorithm=algorithm,
                                         leaf_size=leaf_size,
                                         n_jobs=-1)
```
##### Example
```python
 knn_parameters = {'n_neighbors': [50, 100, 200, 250, 300, 350],
                              'weights': ['uniform', 'distance'],
                              'algorithm': ['ball_tree', 'kd_tree'],
                              'leaf_size': [20, 25, 30, 35, 40, 45, 50],
                              }
```

### Method Name: get_best_model
```python
 def get_best_model(self, x, y):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object

#### create best model for Random Forest

prediction using the Random Forest Algorithm

```python
self.random_forest = self.get_tuned_random_forest_classifier(train_x, train_y)
self.prediction_random_forest = self.random_forest.predict(
    test_x)
```

####  create best model for XGBoost

Predictions using the XGBoost Model

```python
train_x, test_x, train_y, test_y = train_test_split(x, y)
self.xgboost = self.get_tuned_xgboost_classifier(train_x, train_y)
self.prediction_xgboost = self.xgboost.predict(test_x)
```
### Method Name: generate_model_report

```python
def generate_model_report(self, model_object, train_x, train_y, test_x, test_y, num_classes):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object
python
## class ClassificationModelTuner():

def __init__(self):
        self.file_object = open('logs/classificationModelsLogs.txt', 'a+')
        self.logger_object = AppLogger()
        self.file_operation = FileOperation()
```

### Method Name: get_tuned_random_forest_classifier

```python
def get_tuned_random_forest_classifier(self, x_train, y_train):
```
Description: This method will be used to build RandomForestClassifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized RandomForestClassifier model.

A random forest is a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting. The sub-sample size is controlled with the max_samples parameter if bootstrap=True (default), otherwise the whole dataset is used to build each tree.

#### Example
```python
self.rf_parameters = {
                'max_depth': [5, 10, 15, 20, 25, None],
                'n_estimators': range(10, 500, 50),
                'criterion': ['gini', 'entropy'],
                'bootstrap': [True, False],
                'min_samples_split': range(2, 10, 1),
                'max_features': ['auto', 'log2'],
                'min_samples_leaf': range(1, 10),
                
```
##### Fitting the Model ( RandomForestClassifier)
```python
self.model = RandomForestClassifier(n_jobs=-1)
            self.model.fit(x_train, y_train)
```


###  Method Name: get_tuned_xgboost_classifier
```python
def get_tuned_xgboost_classifier(self, x_train, y_train):
```
Description: This method will be used to build XGBoost Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized XGBoost model.

####  Booster Parameters

```python
self.xg_parameters = {"n_estimators": [10, 50, 100, 200],
                                  "learning_rate": [0.05, 0.10, 0.15, 0.20, 0.25, 0.30],
                                  "max_depth": [3, 4, 5, 6, 8, 10, 12, 15, 20],
                                  "min_child_weight": [1, 3, 5, 7],
                                  "gamma": [0.0, 0.1, 0.2, 0.3, 0.4, 0.5],
                                  "colsample_bytree": [0.3, 0.4, 0.5, 0.7]
                                  }
```

##### Fitting the Model  [x_train, y_train( xgboost_classifier)]

```python
self.xgboost_model = XGBClassifier(n_jobs=-1)
self.xgboost_model.fit(x_train, y_train)
```

### Method Name: get_tuned_knn_classifier
```python
def get_tuned_knn_classifier(self, x_train, y_train):
```

Description: This method will be used to build KNearestNeighbour Classifier model

Input Description: It takes x_train and y_train data for training the model.

Output:  It return Optimized KNearestNeighbourClassifier model.


#### Patameters

The overall parameters have been divided into 3 categories by XGBoost authors:

General Parameters: Guide the overall functioning

Booster Parameters: Guide the individual booster (tree/regression) at each step

Learning Task Parameters: Guide the optimization performed

```python
rmdsearch = RandomizedSearchCV(KNeighborsClassifier(), knn_parameters, n_iter=10, cv=10, random_state=22,
                                           n_jobs=-1)
            rmdsearch.fit(x_train, y_train)
            hyperparameters = rmdsearch.best_params_
            n_neighbors, weights, algorithm, leaf_size = hyperparameters['n_neighbors'], hyperparameters['weights'], \
                                                         hyperparameters['algorithm'], hyperparameters['leaf_size']
            model = KNeighborsClassifier(n_neighbors=n_neighbors,
                                         weights=weights,
                                         algorithm=algorithm,
                                         leaf_size=leaf_size,
                                         n_jobs=-1)
```
##### Example
```python
 knn_parameters = {'n_neighbors': [50, 100, 200, 250, 300, 350],
                              'weights': ['uniform', 'distance'],
                              'algorithm': ['ball_tree', 'kd_tree'],
                              'leaf_size': [20, 25, 30, 35, 40, 45, 50],
                              }
```

### Method Name: get_best_model
```python
 def get_best_model(self, x, y):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object

#### create best model for Random Forest

prediction using the Random Forest Algorithm

```python
self.random_forest = self.get_tuned_random_forest_classifier(train_x, train_y)
self.prediction_random_forest = self.random_forest.predict(
    test_x)
```

####  create best model for XGBoost

Predictions using the XGBoost Model

```python
train_x, test_x, train_y, test_y = train_test_split(x, y)
self.xgboost = self.get_tuned_xgboost_classifier(train_x, train_y)
self.prediction_xgboost = self.xgboost.predict(test_x)
```
### Method Name: generate_model_report

```python
def generate_model_report(self, model_object, train_x, train_y, test_x, test_y, num_classes):
```

Description: Find out the Model which has the best AUC score.

Output: The best model name and the model object

                                   
                                   
