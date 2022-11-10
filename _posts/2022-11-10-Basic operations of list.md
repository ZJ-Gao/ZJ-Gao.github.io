# List

## Sort the list reversely according to **index** 列表元素按照索引值逆序排列

https://blog.csdn.net/xijuezhu8128/article/details/88555003


```python
list1 = [5,7,8,10,1]
list1.reverse() # 不需要创建新的副本用于存储结果，不需要重新申请空间来保存最后的结果，但是修改了原来的数据。
list1
```




    [1, 10, 8, 7, 5]



## Sort the list reversely according to **element** 列表元素按照元素值逆序排列


```python
list1 = [5,7,8,10,1]
list1.sort()
list1
```




    [1, 5, 7, 8, 10]



## How to select an element randomly from the list?

`random.choice`


```python
import random
names = ['John', 'Juan', 'Jane', 'Jack', 'Jill', 'Jean']
def selectRandom(names):
    return random.choice(names)
selectRandom(names)
```




    'Jane'



## Convert a list to an array 

`np.array()`


```python
import numpy as np
list1 = [5,7,8,10,1]
arr1 = np.array(list1)
arr1 
```




    array([ 5,  7,  8, 10,  1])



## Combine two lists and then convert them to a DataFrame

1. Change into tuple `list(zip(,))` 

2. `pd.DataFrame(tuple, columns=[])`


```python
import pandas as pd
names = ['John', 'Juan', 'Jane', 'Jack', 'Jill', 'Jean']
num = [1,2,3,4,5,6]
data_tuples = list(zip(names,num))
pd.DataFrame(data_tuples, columns=['names','num'])
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
      <th>names</th>
      <th>num</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Juan</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jane</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jack</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jill</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jean</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



## Find the intersection, union and difference between two lists 交集、并集和差集

https://www.adamsmith.haus/python/answers/how-to-find-the-intersection-of-two-lists-in-python


```python
# Method 1 for intersection
listA = ['A', 'B', 'C','D']
listB = ['A', 'B']
retA = [i for i in listA if i in listB]
# Method 2 for intersection. Convert to `Set` to operate
retB = list(set(listA).intersection(set(listB)))
retB 
```




    ['B', 'A']




```python
# Union
listA = ['A', 'B', 'C','D']
listB = ['A', 'B']
retC = list(set(listA).union(set(listB)))
retC
```




    ['B', 'C', 'A', 'D']




```python
# difference
listA = ['A', 'B', 'C','D']
listB = ['A', 'B','F']
retD = list(set(listB).difference(set(listA))) # Elements in list B but not list A
retD
```




    ['F']



## Combine two different elements in a list 将列表中的不同元素两两组合

`itertools.permutations（list, num）`

挑选元素的先后次序matters


```python
import itertools
aa = ['a', 'b', 'c']
bb = list(itertools.permutations(aa, 2))
print(bb)
```

    [('a', 'b'), ('a', 'c'), ('b', 'a'), ('b', 'c'), ('c', 'a'), ('c', 'b')]
    

`itertools.combination（list, num）`
只关注元素组合本身，不关注先后次序


```python
import itertools
aa = ['a', 'b', 'c']
cc = list(itertools.combinations(aa, 2))
print(cc)
```

    [('a', 'b'), ('a', 'c'), ('b', 'c')]
    


