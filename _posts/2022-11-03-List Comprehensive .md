# List Comprehensive

## e.g. #1


```python
a_list = [-4, -5, 1, 6, 10]
```


```python
# Select numbers which are larger than 0 in the list
list_larger_zero = [i for i in a_list if i>0]
list_larger_zero 
```




    [1, 6, 10]



## e.g. #2


```python
# Select odd numbers from a list and then double them
list_new = [i*2 for i in a_list if i%2 != 0]
list_new
```




    [-10, 2]



# Dict Comprehensive


```python
# switch key and value in a dict
dict_personal_info = {'Mike': 26, 'Grace': 17, 'Nick':31}
```


```python
dict_reverse_info = {v:k for k, v in dict_personal_info.items()}
```


```python
dict_reverse_info 
```




    {26: 'Mike', 17: 'Grace', 31: 'Nick'}


