# Pandas and Numpy


```python
import pandas as pd
import numpy as np
```

## Pandas


```python
weather_data = [
    {'day': '1/1/2017', 'temperature': 32, 'windspeed': 6, 'event': 'Rain'},
    {'day': '1/2/2017', 'temperature': 35, 'windspeed': 7, 'event': 'Sunny'},
    {'day': '1/3/2017', 'temperature': 28, 'windspeed': 2, 'event': 'Snow'},
    {'day': '1/4/2017', 'temperature': 24, 'windspeed': 7, 'event': 'Snow'},
    {'day': '1/5/2017', 'temperature': 32, 'windspeed': 4, 'event': 'Rain'},
    {'day': '1/6/2017', 'temperature': 31, 'windspeed': 2, 'event': 'Sunny'}
]
df = pd.DataFrame(weather_data)
df
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
      <th>day</th>
      <th>temperature</th>
      <th>windspeed</th>
      <th>event</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>32</td>
      <td>6</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>35</td>
      <td>7</td>
      <td>Sunny</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>28</td>
      <td>2</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>24</td>
      <td>7</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>32</td>
      <td>4</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>31</td>
      <td>2</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>



### How many categories in a categorical column?(describe)

`value_counts()`


```python
df['event'].value_counts(dropna=False)
```




    Rain     2
    Sunny    2
    Snow     2
    Name: event, dtype: int64



### Convert Series to dictionary


```python
df['day'].to_dict()
```




    {0: '1/1/2017',
     1: '1/2/2017',
     2: '1/3/2017',
     3: '1/4/2017',
     4: '1/5/2017',
     5: '1/6/2017'}




```python
df[['day','event']].to_dict()
```




    {'day': {0: '1/1/2017',
      1: '1/2/2017',
      2: '1/3/2017',
      3: '1/4/2017',
      4: '1/5/2017',
      5: '1/6/2017'},
     'event': {0: 'Rain', 1: 'Sunny', 2: 'Snow', 3: 'Snow', 4: 'Rain', 5: 'Sunny'}}



### Convert Dictionary to Series

`pd.Series()`


```python
dictionary = {'A' : 10, 'B' : 20, 'C' : 30}
s1 = pd.Series(dictionary)
s1
```




    A    10
    B    20
    C    30
    dtype: int64



### Access elements in series by index

`df[''].index`


```python
type(df['day'].index)
```




    pandas.core.indexes.range.RangeIndex




```python
for x in df['day'].index:
    print(df['day'][x])
```

    1/1/2017
    1/2/2017
    1/3/2017
    1/4/2017
    1/5/2017
    1/6/2017
    

### Get several columns from the original DataFrame

`pd.DataFrame(df, columns=[])`


```python
df1 = pd.DataFrame(df, columns=['day','event'])
df1
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
      <th>day</th>
      <th>event</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>



### Initilize a DataFrame and copy from dfs


```python
title_df = pd.DataFrame()
title_df['day'] = df['day'] 
title_df['day'][0] = '2/5/2018'
title_df['day']
```




    0    2/5/2018
    1    1/2/2017
    2    1/3/2017
    3    1/4/2017
    4    1/5/2017
    5    1/6/2017
    Name: day, dtype: object




```python
df['day'] # Different memory location, are not interconnected
```




    0    1/1/2017
    1    1/2/2017
    2    1/3/2017
    3    1/4/2017
    4    1/5/2017
    5    1/6/2017
    Name: day, dtype: object



### Remove/Drop one of rows in the series based on index

`Series.drop(labels=[])`


```python
sr = pd.Series([80, 25, 3, 25, 24, 6]) 
index_ = ['Coca Cola', 'Sprite', 'Coke', 'Fanta', 'Dew', 'ThumbsUp'] 
sr.index = index_ 
sr
```




    Coca Cola    80
    Sprite       25
    Coke          3
    Fanta        25
    Dew          24
    ThumbsUp      6
    dtype: int64




```python
# drop the passed labels 
result = sr.drop(labels=['Sprite', 'Dew']) 
result
```




    Coca Cola    80
    Coke          3
    Fanta        25
    ThumbsUp      6
    dtype: int64



### Remove/Drop columns from DataFrame

`df.drop(columns=)`


```python
# Remeber to reassign the value to the original dataframe after `drop`
df2 = df.copy()
df2 = df2.drop(columns=['temperature'], axis=1)
df2
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
      <th>day</th>
      <th>windspeed</th>
      <th>event</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>6</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>7</td>
      <td>Sunny</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>2</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>7</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>4</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>2</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>



### Concate two DataFrames

`pd.concat([df1,df2], axis=1, join_axes[df1.index])`


```python
# axis=1, according to rows, which mean columns will be added(changes happen on columns)
pd.concat([df1,df2], axis=1)
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
      <th>day</th>
      <th>event</th>
      <th>day</th>
      <th>windspeed</th>
      <th>event</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
      <td>1/1/2017</td>
      <td>6</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
      <td>1/2/2017</td>
      <td>7</td>
      <td>Sunny</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
      <td>1/3/2017</td>
      <td>2</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
      <td>1/4/2017</td>
      <td>7</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
      <td>1/5/2017</td>
      <td>4</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
      <td>1/6/2017</td>
      <td>2</td>
      <td>Sunny</td>
    </tr>
  </tbody>
</table>
</div>




```python
# axis = 0, changes happen on rows
df_conc_row = pd.concat([df1,df2], axis=0)
df_conc_row
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
      <th>day</th>
      <th>event</th>
      <th>windspeed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



### Check if NaN in the data

`df.isnull().any()`


```python
df_conc_row.isnull().any()
```




    day          False
    event        False
    windspeed     True
    dtype: bool



### Fill null

`df.fillna(value)`


```python
df_conc_row.fillna(0) # fill null with 0
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
      <th>day</th>
      <th>event</th>
      <th>windspeed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1/1/2017</td>
      <td>Rain</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1/2/2017</td>
      <td>Sunny</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1/3/2017</td>
      <td>Snow</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1/4/2017</td>
      <td>Snow</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1/5/2017</td>
      <td>Rain</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1/6/2017</td>
      <td>Sunny</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



## Numpy

## Initilize an array


```python
# Empty, Random elements 
x = np.empty([3,2], dtype = int) 
x
```




    array([[-1622751248,         520],
           [          0,           0],
           [          1,     6029370]])




```python
# Zeros
x = np.zeros([3,2]) 
x
```




    array([[0., 0.],
           [0., 0.],
           [0., 0.]])




```python
# Ones
x = np.ones([3,2]) 
x
```




    array([[1., 1.],
           [1., 1.],
           [1., 1.]])




```python
# Appointed values
an_array = np.full((3, 5), 8)
an_array
```




    array([[8, 8, 8, 8, 8],
           [8, 8, 8, 8, 8],
           [8, 8, 8, 8, 8]])


