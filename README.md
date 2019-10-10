
### Questions
- nested loops/going through them
- // -> what is this?
- syntax
- lambda functions

### Objectives
YWBAT
- write functions to execute certain statistical tasks on data
- write a try/except in a function
    - What is the benefit of using a try/except over an if/else?
        - catches all the exceptions that one might overlook
        - it doesn't break your code
        - can help you loading corrupt files
        - find where your error is occuring
- explain the purpose of a try/except
- manipulate dictionaries to get certain key/value pairs from them
- write a python script
- explain what's happening in a python script

### Outline


```python
import numpy as np

from collections import Counter

import matplotlib.pyplot as plt
```

### Build functions for the following tasks
* Mean
* Mode
* Standard Deviation

### Jupyter Best Practices
- `shift+tab` x 1, x2, x4 to read documentation of a method
- let `tab` autocomplete things for you
    - avoid typos and other nonsense
- listen to jupyter and other ides when they talk to you


### Why is turning off print statements a good thing? 
- They can clutter up an output
- Takes up computational time
- Eats away the memory


```python
# How to write a function like a python developer
# Let's add a docstring to our function
def mean(lst, verbose=True):
    """
    This function will calculate the mean of a
    list or an array
    
    Paramters
    lst : list
        a list of numbers to calculate the mean on, list cannot contain NaN values 
    
    Return
    mean_list: int/float
        the mean of lst
    """
    exception_counts = 0
    sum_list = 0
    total_elements = 0
    
    for index, i in enumerate(lst):
        try:
            sum_list += i
            total_elements += 1
        except:
            if verbose:
                print(f"this index is broken {index}")
            exception_counts += 1
    
    if verbose:
        print(f"Discovered {exception_counts} Exceptions in your list")
    return sum_list/total_elements


def mode(lst):
    """
    This function will calculate the mode of a list or an array
    
    Paramters
    lst : list
        a list of numbers to calculate the mode of
    
    Return
    modes_of_list: 
        the mean of lst
    
    """
    modes_of_list = []
    
    counter_dict = Counter(lst)
    counter_dict_list = [(k, v) for k, v in counter_dict.items()]
    sorted_counter_list = sorted(counter_dict_list, key=lambda x: x[1], reverse=True)
    max_freq = sorted_counter_list[0][1]
    for number, freq in sorted_counter_list:
        if freq == max_freq:
            modes_of_list.append(number)
        else:
            break
    return modes_of_list


def standard_deviation(lst):
    pass 
```


```python
x = np.random.randint(1, 20, size=30)
x
```




    array([10,  2,  3, 10,  3,  7,  6,  6, 12,  7, 16, 13,  8,  2, 11,  9,  9,
            9, 19, 13, 16,  8,  3,  8,  7,  2,  7, 12,  4,  4])




```python
mean(x), np.mean(x)
```

    Discovered 0 Exceptions in your list





    (8.2, 8.2)




```python
# # What if we have a None value in our list
# x = np.append(x, [None, 1, 3, None, 5, 'this', 'string', 'is', 'in', 'my', 'list'])
# x
```


```python
mean(x, verbose=False)
```




    8.2



### What does Counter do?


```python
x
```




    array([10,  2,  3, 10,  3,  7,  6,  6, 12,  7, 16, 13,  8,  2, 11,  9,  9,
            9, 19, 13, 16,  8,  3,  8,  7,  2,  7, 12,  4,  4])




```python
mode(x)
```

    [(7, 4), (2, 3), (3, 3), (8, 3), (9, 3), (10, 2), (6, 2), (12, 2), (16, 2), (13, 2), (4, 2), (11, 1), (19, 1)]





    [7]




```python
c = Counter(x)
```


```python
for k, v in c.items():
    print(k, v)
```

    16 2
    3 2
    12 2
    17 1
    4 3
    15 2
    10 3
    11 4
    13 2
    9 2
    5 3
    6 2
    8 1
    19 1
    18 1
    14 1
    None 2
    1 1
    this 1
    string 1
    is 1
    in 1
    my 1
    list 1


### `lambda` functions


```python
def summ(a, b):
    return a + b

summ(8, 13), type(summ)
```




    (21, function)




```python
# convert summ to a lambda function
summ = lambda a, b: a + b 

summ(8, 13), type(summ)
```




    (21, function)




```python
summ(100, 200)
```




    300



### Let's learn about the `sorted` method


```python
x = np.random.randint(80, 90, size=20)
y = np.random.randint(0, 10, size=20)
z = np.random.randint(20, 30, size=20)

new_list = [(i, j, k) for i, j, k in zip(x, y, z)]
new_list
```




    [(82, 4, 29),
     (80, 7, 23),
     (86, 6, 22),
     (83, 9, 23),
     (82, 6, 21),
     (80, 1, 24),
     (88, 2, 27),
     (82, 7, 23),
     (87, 1, 24),
     (87, 6, 23),
     (82, 8, 29),
     (85, 9, 22),
     (85, 1, 28),
     (80, 2, 24),
     (81, 4, 29),
     (85, 2, 29),
     (85, 3, 29),
     (82, 2, 29),
     (84, 5, 22),
     (89, 2, 25)]




```python
# let's sort our list of tuples by the zeroth element
sorted(new_list) # by default this will happen
```




    [(80, 1, 24),
     (80, 2, 24),
     (80, 7, 23),
     (81, 4, 29),
     (82, 2, 29),
     (82, 4, 29),
     (82, 6, 21),
     (82, 7, 23),
     (82, 8, 29),
     (83, 9, 23),
     (84, 5, 22),
     (85, 1, 28),
     (85, 2, 29),
     (85, 3, 29),
     (85, 9, 22),
     (86, 6, 22),
     (87, 1, 24),
     (87, 6, 23),
     (88, 2, 27),
     (89, 2, 25)]




```python
# let's sort our list of tuples by the 1st indexed element
sorting_function = lambda tup: tup[1]
def sorting_function_2(tup):
    return tup[1]


sorted(new_list, key=sorting_function_2)
```




    [(80, 1, 24),
     (87, 1, 24),
     (85, 1, 28),
     (88, 2, 27),
     (80, 2, 24),
     (85, 2, 29),
     (82, 2, 29),
     (89, 2, 25),
     (85, 3, 29),
     (82, 4, 29),
     (81, 4, 29),
     (84, 5, 22),
     (86, 6, 22),
     (82, 6, 21),
     (87, 6, 23),
     (80, 7, 23),
     (82, 7, 23),
     (82, 8, 29),
     (83, 9, 23),
     (85, 9, 22)]




```python
# sort by the 2nd indexed element
sorted(new_list, key=lambda x: x[2])
```




    [(82, 6, 21),
     (86, 6, 22),
     (85, 9, 22),
     (84, 5, 22),
     (80, 7, 23),
     (83, 9, 23),
     (82, 7, 23),
     (87, 6, 23),
     (80, 1, 24),
     (87, 1, 24),
     (80, 2, 24),
     (89, 2, 25),
     (88, 2, 27),
     (85, 1, 28),
     (82, 4, 29),
     (82, 8, 29),
     (81, 4, 29),
     (85, 2, 29),
     (85, 3, 29),
     (82, 2, 29)]




```python
7/2, 7//2, 10/6, 10//6
```




    (3.5, 3, 1.6666666666666667, 1)




```python
x[6//2]
```




    10



### Assessment
