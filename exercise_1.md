# Exercise 1
### Description
I used this exercise to get familiar with pycharm, numpy, and pandas. I decided to create different functions for each "sub" exercise
so that if I had an issue importing something I could comment out the area that was causing me problems.

### Code
``` python
import math
import numpy as np
import pandas as pd

def basic_ops():
    sum = 1+1
    print("what is 1 + 1? It's " + str(sum) )
    x = 1
    print("x is: " + str(x))
    x += 1
    print("x has been incremented to: " + str(x))

def log_ops():
    bool_1 = (1 + 1) == 2
    print(bool_1)
    bool_2 = ('cat' == 'dog')
    print(bool_2)
    bool_3 = (6**4 == 4**6)
    print(bool_3)
    bool_4 = bool_2 | bool_1
    print(bool_4)
    bool_5 = bool_2 & bool_1
    print(bool_5)

def nan_ops():
    x = float('nan')
    a = (x == x) # nan is never equal to itself!
    print(a)
    print(math.isnan(a))

def list_review():
    y = [1, 2, float('nan'), 4, 5, float('nan')]
    print(y)
    for item in y:
        print(item == item)

    # or simpler...
    [item == item for item in y]
    # even simpler!
    bool_1 = np.isnan(y[2])
    print(bool_1)

    idx = np.isnan(y)
    print(~idx)
    # change type to array
    y = np.array(y)
    print(y[~idx])
    # filter array
    y_filtered = y[~idx]
    print(y_filtered)

def pandas_practice():
    path_to_file = 'gapminder.tsv'
    data = pd.read_csv(path_to_file, sep = '\t')
    # print(data) # won't print everything in terminal -- need to specify what you want
    head_1 = data.head(2)
    print(head_1)
    tail_1 = data.tail(2)
    print(tail_1)

    print(data.size)
    print(data.shape[0] * data.shape[1])
    print(data.info())
    print(data.columns)
    print(list(data.columns))
    print(data.describe())

if __name__ == '__main__':
    basic_ops()
    log_ops()
    nan_ops()
    list_review()
    pandas_practice()

```

I ran the program (called main.py) with the command `python3 main.py`
