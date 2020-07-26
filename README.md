# Setup

```python
import scipy
from scipy.stats.stats import pearsonr
from datetime import datetime
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
```

### This class shall be used to include all Data Visualization techniques to be feed to the Machine Learning Models

```python
# class DataVisualization:
```
## Method Name: balance_imbalance_check
```python
def balance_imbalance_check(self, dataframe, target):
```
####    Description: This method will be used to plot the balance/imbalance datasets using barplot/countplot
        Input Description: data: the input dataframe with target column.
    
        target: target column name.
    
        Output: plot of target variable value count.
    
        On Failure: Raise Exception
```python
x = sns.countplot(target,data=dataframe).set_title("Balance Imbalance Count")
sns.barplot(x = 'is_promoted', y = 'is_promoted' ,data=df, hue  = 'is_promoted', estimator = lambda x: len(x)/len(df) *100).set_title("Balance Imbalance Count")
```

## Method Name: corelation_heatmap
```python
    def corelation_heatmap(self, dataframe):
```

####    Description: This method will be used to plot the heatmap to show the corelation among the variables
       
       Input Description: data: the input dataframe with target column.
       
       Output: plot of heatmap that shows the corelation among the variable.
       
       On Failure: Raise Exception

```python
    data = dataframe.select_dtypes(include=[np.number])
    plt.figure(figsize=(20, 10))
    sns.set_palette("PuBuGn_d")
    plot = sns.heatmap(data.corr(), annot=True, cmap='RdYlGn')
    plot.figure.savefig("static/graphs/correlation.png")
```

