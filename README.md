
# The Influence of Building Shapes and Glazing on Energy Loads

In this project, we will be predicting building heating and cooling loads with respect to 8 building features.  The buildings differ with respect to shape, glazing area, the glazing area distribution, and orientation.  To acquire the data, an energy analysis was performed using 12 different building shapes to estimate the heating and cooling loads. The simulations were performed in the city of Athens, Greece.

Different settings were simulated with the 8 building features to obtain a total of 768 shapes.  The goal is to use these features to predict the [thermal energy load](https://www.energy.gov/energysaver/heat-and-cool) for each building shape. The features are:

- relative compactness - volume divided by the (surface area * 1.53). Usually the more compact the building is, the taller and more narrow it is.
- surface area - in meters squared. Includes wall areas + roof area + floor area
- wall area - in meters squared
- roof area - in meters squared
- overall height - in meters
- orientation - 2: North, 3: East, 4: South, 5: West
- glazing area - as a percentage of the floor area - 0%, 10%, 25%, and 40%
- glazing area distribution: 
    - 0: uniform - with 25% glazing on each side
    - 1: north - 55% on the north side and 15% on each of the other sides
    - 2: east - 55% on the east side and 15% on each of the other sides
    - 3: south - 55% on the south side and 15% on each of the other sides
    - 4: west - 55% on the west side and 15% on each of the other sides
- the heating and cooling loads listed in kWh/m2.

12 buildings were modeled with different shapes, surface areas and dimensions.  The overall volume was kept the same for each building at 772 meters cubed.  Considering twelve building forms with three glazing area variations, six glazing area distributions each (5 distributions + 1 with no glazing), for four orientations, we obtain 12 × 3 × 6 × 4 = 768 different building variations. 

Building thermal properties, such as solar heat transfer coefficient for the glass and U-values for the walls, floors and roofs, are assumed to be constant and are not part of this analysis.

The dataset, which can be found [here](https://archive.ics.uci.edu/ml/datasets/Energy+efficiency) was donated to the University of California at Irving.

The performance of the model for successfully predicting the outcome will be evaluated using the Root Mean Squared Error [(RMSE)](https://www.statisticshowto.datasciencecentral.com/rmse/). It measures how close the predictions are close to the real values. We want to achieve a low RMSE.  The lower this value, the better the model fits the data.

### Importing Python Libraries


```python
import pandas as pd
import numpy as np

from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import train_test_split

import matplotlib.pyplot as plt
from pandas.plotting import scatter_matrix
import seaborn as sns
%matplotlib inline
```

### Creating a Dataframe with The Data


```python
data = pd.read_csv('Energy data.csv')
```


```python
data.columns = ['relative_compactness', 'surface_area', 'wall_area', 'roof_area', 'overall_height',
                'orientation', 'glazing_area', 'glazing_area_distribution', 'heating_load', 'cooling_load']
```

### Table of Building Features


```python
data.head(20)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>heating_load</th>
      <th>cooling_load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.55</td>
      <td>21.33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>20.84</td>
      <td>28.28</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>21.46</td>
      <td>25.38</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>20.71</td>
      <td>25.16</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>19.68</td>
      <td>29.60</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.86</td>
      <td>588.0</td>
      <td>294.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>19.50</td>
      <td>27.30</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.86</td>
      <td>588.0</td>
      <td>294.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>19.95</td>
      <td>21.97</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.86</td>
      <td>588.0</td>
      <td>294.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>19.34</td>
      <td>23.49</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.86</td>
      <td>588.0</td>
      <td>294.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>18.31</td>
      <td>27.87</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.82</td>
      <td>612.5</td>
      <td>318.5</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>17.05</td>
      <td>23.77</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.82</td>
      <td>612.5</td>
      <td>318.5</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>17.41</td>
      <td>21.46</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.82</td>
      <td>612.5</td>
      <td>318.5</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>16.95</td>
      <td>21.16</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.82</td>
      <td>612.5</td>
      <td>318.5</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>15.98</td>
      <td>24.93</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0.79</td>
      <td>637.0</td>
      <td>343.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>28.52</td>
      <td>37.73</td>
    </tr>
    <tr>
      <th>17</th>
      <td>0.79</td>
      <td>637.0</td>
      <td>343.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>29.90</td>
      <td>31.27</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.79</td>
      <td>637.0</td>
      <td>343.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>29.63</td>
      <td>30.93</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.79</td>
      <td>637.0</td>
      <td>343.0</td>
      <td>147.00</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>28.75</td>
      <td>39.44</td>
    </tr>
  </tbody>
</table>
</div>



To simplify this analysis, we'll sum the heating and cooling load into a new column called "energy load". Then we'll eliminate the heating and cooling load columns.


```python
data_new = data.copy()
```


```python
data_new['energy load'] = data['heating_load'] + data['cooling_load']
```


```python
data_new = data_new.drop(columns=['heating_load', 'cooling_load'])
```

### New Table of Building Features


```python
data_new.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>energy load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>4</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.98</td>
      <td>514.5</td>
      <td>294.0</td>
      <td>110.25</td>
      <td>7.0</td>
      <td>5</td>
      <td>0.0</td>
      <td>0</td>
      <td>36.88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.90</td>
      <td>563.5</td>
      <td>318.5</td>
      <td>122.50</td>
      <td>7.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>49.12</td>
    </tr>
  </tbody>
</table>
</div>



### Statistical Description for Each Variable


```python
data_new.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>energy load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.00000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.00000</td>
      <td>768.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.764167</td>
      <td>671.708333</td>
      <td>318.500000</td>
      <td>176.604167</td>
      <td>5.25000</td>
      <td>3.500000</td>
      <td>0.234375</td>
      <td>2.81250</td>
      <td>46.894961</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.105777</td>
      <td>88.086116</td>
      <td>43.626481</td>
      <td>45.165950</td>
      <td>1.75114</td>
      <td>1.118763</td>
      <td>0.133221</td>
      <td>1.55096</td>
      <td>19.484947</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.620000</td>
      <td>514.500000</td>
      <td>245.000000</td>
      <td>110.250000</td>
      <td>3.50000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>16.950000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.682500</td>
      <td>606.375000</td>
      <td>294.000000</td>
      <td>140.875000</td>
      <td>3.50000</td>
      <td>2.750000</td>
      <td>0.100000</td>
      <td>1.75000</td>
      <td>28.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.750000</td>
      <td>673.750000</td>
      <td>318.500000</td>
      <td>183.750000</td>
      <td>5.25000</td>
      <td>3.500000</td>
      <td>0.250000</td>
      <td>3.00000</td>
      <td>40.970000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.830000</td>
      <td>741.125000</td>
      <td>343.000000</td>
      <td>220.500000</td>
      <td>7.00000</td>
      <td>4.250000</td>
      <td>0.400000</td>
      <td>4.00000</td>
      <td>64.335000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.980000</td>
      <td>808.500000</td>
      <td>416.500000</td>
      <td>220.500000</td>
      <td>7.00000</td>
      <td>5.000000</td>
      <td>0.400000</td>
      <td>5.00000</td>
      <td>89.950000</td>
    </tr>
  </tbody>
</table>
</div>



### Linear Correlation Between Variables


```python
# Setting the format for diplaying the correlation table
pd.set_option('display.float_format', lambda x: '{:,.3f}'.format(x))
```


```python
data_new.corr().sort_values('energy load', ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
      <th>energy load</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>energy load</th>
      <td>0.632</td>
      <td>-0.669</td>
      <td>0.445</td>
      <td>-0.867</td>
      <td>0.898</td>
      <td>0.006</td>
      <td>0.241</td>
      <td>0.070</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>overall_height</th>
      <td>0.828</td>
      <td>-0.858</td>
      <td>0.281</td>
      <td>-0.973</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.898</td>
    </tr>
    <tr>
      <th>relative_compactness</th>
      <td>1.000</td>
      <td>-0.992</td>
      <td>-0.204</td>
      <td>-0.869</td>
      <td>0.828</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.632</td>
    </tr>
    <tr>
      <th>wall_area</th>
      <td>-0.204</td>
      <td>0.196</td>
      <td>1.000</td>
      <td>-0.292</td>
      <td>0.281</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.445</td>
    </tr>
    <tr>
      <th>glazing_area</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.213</td>
      <td>0.241</td>
    </tr>
    <tr>
      <th>glazing_area_distribution</th>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.213</td>
      <td>1.000</td>
      <td>0.070</td>
    </tr>
    <tr>
      <th>orientation</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.006</td>
    </tr>
    <tr>
      <th>surface_area</th>
      <td>-0.992</td>
      <td>1.000</td>
      <td>0.196</td>
      <td>0.881</td>
      <td>-0.858</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.669</td>
    </tr>
    <tr>
      <th>roof_area</th>
      <td>-0.869</td>
      <td>0.881</td>
      <td>-0.292</td>
      <td>1.000</td>
      <td>-0.973</td>
      <td>0.000</td>
      <td>-0.000</td>
      <td>-0.000</td>
      <td>-0.867</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (10,10))
sns.heatmap(data_new.corr(), annot=True, linewidths=1, linecolor='blue');
```


![png](output_20_0.png)


Correlation shows how features are related to each other using a linear relationship between variables. The higher the number, the stronger the correlation.  For example, in the figure above, overall height of a building is the strongest variable linearly-correlated to energy load. The taller the building, the larger the energy load.

The problem with using this method is that it is not able to accurately determine the correlation between variables if there is a non-linear dependency.  And these variables are not linearly-dependent with the energy load. However, it is possible to compare height, compactness, and areas since there are linear relationship between them.

To determine the correlation with the energy load, a better metric to use is called *feature importance*, which we will determine after the model is built.

On to the model.

## Predictive Modeling


```python
# The dependent variable --> Energy Load
y = data_new['energy load'] 
```


```python
# The independent variables --> Building features
X = data_new.drop(columns='energy load')
X.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>relative_compactness</th>
      <th>surface_area</th>
      <th>wall_area</th>
      <th>roof_area</th>
      <th>overall_height</th>
      <th>orientation</th>
      <th>glazing_area</th>
      <th>glazing_area_distribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.980</td>
      <td>514.500</td>
      <td>294.000</td>
      <td>110.250</td>
      <td>7.000</td>
      <td>2</td>
      <td>0.000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.980</td>
      <td>514.500</td>
      <td>294.000</td>
      <td>110.250</td>
      <td>7.000</td>
      <td>3</td>
      <td>0.000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.980</td>
      <td>514.500</td>
      <td>294.000</td>
      <td>110.250</td>
      <td>7.000</td>
      <td>4</td>
      <td>0.000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.980</td>
      <td>514.500</td>
      <td>294.000</td>
      <td>110.250</td>
      <td>7.000</td>
      <td>5</td>
      <td>0.000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.900</td>
      <td>563.500</td>
      <td>318.500</td>
      <td>122.500</td>
      <td>7.000</td>
      <td>2</td>
      <td>0.000</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### Train/ Test Split

The data will be split into a training set to train the model, and a testing set to test how accurate the training was.  80% of the data will be used to train the model and 20% of the data will be used to test it.


```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=23)
```

### Training

The model will be trained using a [random forest regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html). This is an [ensemble technique](https://en.wikipedia.org/wiki/Ensemble_learning) for regression that uses multiple [decision trees](https://www.lucidchart.com/pages/decision-tree) and [bootstrap aggregating](https://en.wikipedia.org/wiki/Bootstrap_aggregating) or bagging. Bagging involves training several decision trees on different data samples, and then aggregating or combining those samples into one final output.  This technique allows the model to generalize its predictions better for new data that it has not seen.

For our model we will use 100 decision trees (see below: n_estimators=100).


```python
model = RandomForestRegressor(n_estimators=100, random_state=23)
```


```python
# Fitting the random forest regressor model to the training set data
model.fit(X_train, y_train)
```




    RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
               max_features='auto', max_leaf_nodes=None,
               min_impurity_decrease=0.0, min_impurity_split=None,
               min_samples_leaf=1, min_samples_split=2,
               min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=None,
               oob_score=False, random_state=23, verbose=0, warm_start=False)




```python
# Using the fit model to make energy load predictions using the test data building features
predictions = model.predict(X_test)
```

### Visualizing the Results

Now we'll plot a graph to show how close where our predicted values to the actual values in the test set.  The predicted values where determined by the model above ("predictions"), and the actual values are the energy loads from the test set (y_test).


```python
fig, ax = plt.subplots(figsize=(8,8))

ax.plot(range(0,len(X_test)), y_test.values, 'o', color='green', label = 'Actual Values')
ax.plot(range(0,len(X_test)), predictions, '*', color='blue', label = 'Predicted Values')
ax.set_xlabel('Test Sample Number')
ax.set_ylabel('Energy Load')
ax.set_title('Comparing Actual vs Predicted Values')
ax.legend(loc = 'upper right')

plt.grid()
plt.show()
```


![png](output_33_0.png)


We can see the predicted values are very close to the actual values. From the graph it appears that the model is more accurate at predicting lower energy loads vs higher.

### Statistical Metric RMSE

The root mean squared error is a measure of how far the predictions errors are from the regression line. The lower this value, the more accurate was the model at predicting the right outcome.


```python
from sklearn.metrics import mean_squared_error
```


```python
#RMSE = sqrt(MSE)
np.sqrt(mean_squared_error(y_test, predictions))
```




    1.5884910221960344



The RMSE for predicting the energy load is 1.6 kWh/m. Being that the average energy load is 46.9 kWh/m, the prediction error is only 3.4% when compared to the average load.  Thus, the Random Forest Regressor was a good strategy to use for training the model.

### Feature Importance


```python
# Table of feature importance
for feature in zip(data_new.columns, model.feature_importances_):
    print(feature)
```

    ('relative_compactness', 0.5060543116884478)
    ('surface_area', 0.14821753795820464)
    ('wall_area', 0.04233577705009435)
    ('roof_area', 0.08329432066422113)
    ('overall_height', 0.14625311504507843)
    ('orientation', 0.0023343330653874043)
    ('glazing_area', 0.06172701478673418)
    ('glazing_area_distribution', 0.009783589741831876)
    


```python
# Plotting the feature importance
feat_series = pd.Series(model.feature_importances_, index=X.columns)
feat_series.nlargest(8).plot(kind='barh')
plt.show()
```


![png](output_42_0.png)


After training the model, relative compactness is the most important feature for predicting the heating and cooling load of a building.  The glazing area distribution and orientation are relatively unimportant.

The higher the feature importance score, the more relevant the feature is to the output variable. In this case the output is energy load.

Lets plot how the energy load varies due to building relative compactness


```python
data_new.plot(kind='scatter', x="relative_compactness", y="energy load", figsize=(9,6), grid=True);
```


![png](output_46_0.png)


A building relative compactness of around 0.78 produces the highest energy loads.  And in general, buildings with low relative compactness (large surface area), generally shorter, flatter, longer buildings, have a lower thermal energy load and require less heating and cooling.

Please note that this statistical analysis is only valid for buildings in Athens, Greece and with specific building materials held constant throughout the analysis.  If one were to use another city and different building thermal properties, then relative compactness might not be the most important feature and its relationship to energy load would be different.
