# advent-of-code-2020
My solutions for the yearly Advent of Code challenge only Python/Numpy/Pandas.

👇

> [https://adventofcode.com/2020](https://adventofcode.com/2020)

---

- [Day 1](#day1)
- [Day 2](#day2)
- [Day 3](#day3)

## day1

```python
import numpy as np
l = np.loadtxt('2020_day1.dat')

# Part 1
# Find the two entries that sum to 2020; what do you get if you multiply them together?
[ i * j  for i in l for j in l if (i > j) and (i+j == 2020)] # My answer

# Part 2
# what is the product of the three entries that sum to 2020?
[ i * j * k  for i in l for j in l for k in l if (i > j > k) and (i+j+k == 2020)] # My answer
```

## day2

```python
import pandas as pd
df = pd.read_csv('2020_day2.dat', header=None, names=['Value'])

# Part 1
# To try to debug the problem, they have created a list (your puzzle input) of passwords (according to the corrupted database) and the corporate policy when that password was set.
# The password policy indicates the lowest and highest number of times a given letter must appear for the password to be valid.
# For a valid example: `1-3 a: abcde` 
# How many passwords are valid according to their policies?
def parsing(x):
    Num, key, value = x.split(' ')
    try:
        return int(Num.split('-')[0]) <= pd.Series(list(value)).value_counts()[key.split(':')[0]] <= int(Num.split('-')[1])
    except KeyError:
        return False
df.Value.map(parsing).value_counts()[True] # My answer

# Part 2
# Each policy actually describes two positions in the password, where 1 means the first character, 2 means the second character, and so on.
# Exactly one of these positions must contain the given letter.
# For a valid example: `1-3 a: abcde`
# For two invalid examples:  `1-3 b: cdefg`, `2-9 c: ccccccccc`
# How many passwords are valid according to the new interpretation of the policies?
def parsing(x):
    Num, key, value = x.split(' ')
    try:
        return pd.Series(list(value[int(Num.split('-')[0])-1] + value[int(Num.split('-')[1])-1]) ).value_counts()[key.split(':')[0]] == 1
    except KeyError:
        return False
df.Value.map(parsing).value_counts()[True] # My answer
```

## day3

```python
import pandas as pd
import numpy as np
df = pd.read_csv('2020_day3.dat', header=None, names=['Value'])
data = df.Value.map(lambda x: [int(i) for i in list(x.replace('.','0').replace('#','1'))])
Answer = lambda Right, down: sum([np.roll(data.iloc[i], -1*Right*index)[0] for index, i in enumerate(np.arange(data.size)[::down]) if i] )

# Part 1
# The same pattern repeats to the right many times for each row.
# Starting at the top-left corner of your map and following a slope of right 3 and down 1, how many trees (`#`) would you encounter?
Answer(3,1) # My answer

# Part 2
# Determine the number of trees you would encounter if, for each of the following slopes, you start at the top-left corner and traverse the map all the way to the bottom:
# - Right 1, down 1.
# - Right 3, down 1. (This is the slope you already checked in Part 1.)
# - Right 5, down 1.
# - Right 7, down 1.
# - Right 1, down 2.
# What do you get if you multiply together the number of trees (`#`) encountered on each of the listed slopes?
Answer(1,1) * Answer(3,1) * Answer(5,1) * Answer(7,1) * Answer(1,2)  # My answer
```

## Ref

- [Awesome Advent of Code](https://github.com/Bogdanp/awesome-advent-of-code)
