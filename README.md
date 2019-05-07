Comparing building heating and cooling loads with respect to building characteristics. The data contains 768 different building shapes and 8 characteristics.  The goal is to use the 8 building features to predict the heating and cooling load. The features are:

* relative compactness
* surface area - in meters squared
* wall area - in meters squared
* roof area - in meters squared
* overall height - in meters
* orientation - 2: North, 3: East, 4: South, 5: West
* glazing area - as a percentage of the floor area - 0%, 10%, 25%, and 40%
* glazing area distribution:
  - 0: uniform - with 25% glazing on each side
  - 1: north - 55% on the north side and 15% on each of the other sides
  - 2: east - 55% on the east side and 15% on each of the other sides
  - 3: south - 55% on the south side and 15% on each of the other sides
  - 4: west - 55% on the west side and 15% on each of the other sides

The values to predict are the heating and cooling loads listed in kWh/m2.

12 buildings were modeled with different shapes, surface areas and dimensions.  The overall volume was kept the same for each building at 772 meters squared.  Considering twelve building forms with three glazing area variations, six glazing area distributions each (5 distributions + 1 with no glazing), for four orientations, we obtain 12 × 3 × 6 × 4 = 768 different building variations.

The dataset, which can be found [here](https://archive.ics.uci.edu/ml/datasets/Energy+efficiency) was donated to the University of California at Irving.
In [1]:

```hl-ipython3
import pandas as pd
import numpy as np

from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import train_test_split

import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```

In [2]:

```hl-ipython3
data = pd.read_csv('Energy data.csv')
```

In [3]:

```hl-ipython3
data.columns = ['relative_compactness', 'surface_area', 'wall_area', 'roof_area', 'overall_height',
                'orientation', 'glazing_area', 'glazing_area_distribution', 'heating_load', 'cooling_load']
```

In [4]:

```hl-ipython3
data.head()
```

Out[4]:

|  | relative_compactness | surface_area | wall_area | roof_area | overall_height | orientation | glazing_area | glazing_area_distribution | heating_load | cooling_load |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 2 | 0.0 | 0 | 15.55 | 21.33 |
| 1 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 3 | 0.0 | 0 | 15.55 | 21.33 |
| 2 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 4 | 0.0 | 0 | 15.55 | 21.33 |
| 3 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 5 | 0.0 | 0 | 15.55 | 21.33 |
| 4 | 0.90 | 563.5 | 318.5 | 122.50 | 7.0 | 2 | 0.0 | 0 | 20.84 | 28.28 |

In [5]:

```hl-ipython3
data.describe()
```

Out[5]:

|  | relative_compactness | surface_area | wall_area | roof_area | overall_height | orientation | glazing_area | glazing_area_distribution | heating_load | cooling_load |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| count | 768.000000 | 768.000000 | 768.000000 | 768.000000 | 768.00000 | 768.000000 | 768.000000 | 768.00000 | 768.000000 | 768.000000 |
| mean | 0.764167 | 671.708333 | 318.500000 | 176.604167 | 5.25000 | 3.500000 | 0.234375 | 2.81250 | 22.307201 | 24.587760 |
| std | 0.105777 | 88.086116 | 43.626481 | 45.165950 | 1.75114 | 1.118763 | 0.133221 | 1.55096 | 10.090196 | 9.513306 |
| min | 0.620000 | 514.500000 | 245.000000 | 110.250000 | 3.50000 | 2.000000 | 0.000000 | 0.00000 | 6.010000 | 10.900000 |
| 25% | 0.682500 | 606.375000 | 294.000000 | 140.875000 | 3.50000 | 2.750000 | 0.100000 | 1.75000 | 12.992500 | 15.620000 |
| 50% | 0.750000 | 673.750000 | 318.500000 | 183.750000 | 5.25000 | 3.500000 | 0.250000 | 3.00000 | 18.950000 | 22.080000 |
| 75% | 0.830000 | 741.125000 | 343.000000 | 220.500000 | 7.00000 | 4.250000 | 0.400000 | 4.00000 | 31.667500 | 33.132500 |
| max | 0.980000 | 808.500000 | 416.500000 | 220.500000 | 7.00000 | 5.000000 | 0.400000 | 5.00000 | 43.100000 | 48.030000 |

To simplify the model, we'll sum heating and cooling load into a new column called "energy load". Then we'll eliminate the heating and cooling load columns.
In [6]:

```hl-ipython3
data_new = data.copy()
```

In [7]:

```hl-ipython3
data_new['energy load'] = data['heating_load'] + data['cooling_load']
```

In [8]:

```hl-ipython3
data_new = data_new.drop(columns=['heating_load', 'cooling_load'])
```

The new dataset:
In [9]:

```hl-ipython3
data_new.head(2)
```

Out[9]:

|  | relative_compactness | surface_area | wall_area | roof_area | overall_height | orientation | glazing_area | glazing_area_distribution | energy load |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 2 | 0.0 | 0 | 36.88 |
| 1 | 0.98 | 514.5 | 294.0 | 110.25 | 7.0 | 3 | 0.0 | 0 | 36.88 |

Correlation between variables
In [10]:

```hl-ipython3
# Setting the format for diplaying the correlation table
pd.set_option('display.float_format', lambda x: '{:,.3f}'.format(x))
```

In [11]:

```hl-ipython3
data_new.corr().sort_values('energy load', ascending=False)
```

Out[11]:

|  | relative_compactness | surface_area | wall_area | roof_area | overall_height | orientation | glazing_area | glazing_area_distribution | energy load |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| energy load | 0.632 | -0.669 | 0.445 | -0.867 | 0.898 | 0.006 | 0.241 | 0.070 | 1.000 |
| overall_height | 0.828 | -0.858 | 0.281 | -0.973 | 1.000 | 0.000 | 0.000 | 0.000 | 0.898 |
| relative_compactness | 1.000 | -0.992 | -0.204 | -0.869 | 0.828 | 0.000 | 0.000 | 0.000 | 0.632 |
| wall_area | -0.204 | 0.196 | 1.000 | -0.292 | 0.281 | 0.000 | -0.000 | 0.000 | 0.445 |
| glazing_area | 0.000 | 0.000 | -0.000 | -0.000 | 0.000 | 0.000 | 1.000 | 0.213 | 0.241 |
| glazing_area_distribution | 0.000 | -0.000 | 0.000 | -0.000 | 0.000 | 0.000 | 0.213 | 1.000 | 0.070 |
| orientation | 0.000 | 0.000 | 0.000 | 0.000 | 0.000 | 1.000 | 0.000 | 0.000 | 0.006 |
| surface_area | -0.992 | 1.000 | 0.196 | 0.881 | -0.858 | 0.000 | 0.000 | -0.000 | -0.669 |
| roof_area | -0.869 | 0.881 | -0.292 | 1.000 | -0.973 | 0.000 | -0.000 | -0.000 | -0.867 |

In [12]:

```hl-ipython3
plt.figure(figsize = (12,12))
sns.heatmap(data_new.corr(), annot=True, linewidths=1, linecolor='blue');
```

Correlation shows how features are related to each other using a linear correlation between variables.  Keep in mind that since it only find the linear relationship between variables, it will not be able to find the non-linear relationship.  A better metric to use is called _feature importance_, which we will determine after the model is built.

On to the model
In [12]:

```hl-ipython3
y = data_new['energy load']
```

In [13]:

```hl-ipython3
X = data_new.drop(columns='energy load')
```

In [14]:

```hl-ipython3
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=23)
```

In [15]:

```hl-ipython3
model = RandomForestRegressor(n_estimators=100, random_state=23)
```

In [16]:

```hl-ipython3
model.fit(X_train, y_train)
```

Out[16]:

```
RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
           max_features='auto', max_leaf_nodes=None,
           min_impurity_decrease=0.0, min_impurity_split=None,
           min_samples_leaf=1, min_samples_split=2,
           min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=None,
           oob_score=False, random_state=23, verbose=0, warm_start=False)
```

In [17]:

```hl-ipython3
predictions = model.predict(X_test)
```

In [18]:

```hl-ipython3
from sklearn.metrics import r2_score
```

In [19]:

```hl-ipython3
r2_score(y_test, predictions)
```

Out[19]:

```
0.9931211166410133
```

The random forest model provides us with a highly accurate R2 score of 0.993
In [20]:

```hl-ipython3
for feature in zip(data_new.columns, model.feature_importances_):
    print(feature)
```

```
('relative_compactness', 0.5060543116884478)
('surface_area', 0.14821753795820464)
('wall_area', 0.04233577705009435)
('roof_area', 0.08329432066422113)
('overall_height', 0.14625311504507843)
('orientation', 0.0023343330653874043)
('glazing_area', 0.06172701478673418)
('glazing_area_distribution', 0.009783589741831876)
```

After training the model, relative compactness is the most important feature for predicting the heating and cooling load of a building.  The glazing area distribution is relatively unimportant.

The higher the feature importance score, the more relevant the feature is to the output variable, which is energy load in this case.
In [21]:

```hl-ipython3
feat_importances = pd.Series(model.feature_importances_, index=X.columns)
feat_importances.nlargest(10).plot(kind='barh')
plt.show()
```

In [ ]:
