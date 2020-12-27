# advent-of-code-2020
My solutions for the yearly Advent of Code challenge only Python/Numpy.

👇

> [https://adventofcode.com/2020](https://adventofcode.com/2020)

---

- [Day 1](#day1)

## day1

```python
import numpy as np
l = np.loadtxt('2020_day1.dat')

# Part 1
# Find the two entries that sum to 2020; what do you get if you multiply them together?
[ i * j  for i in l for j in l if (i > j) and (i+j == 2020)]

# Part 2
# what is the product of the three entries that sum to 2020?
[ i * j * k  for i in l for j in l for k in l if (i > j > k) and (i+j+k == 2020)]
```


## Ref

- [Awesome Advent of Code](https://github.com/Bogdanp/awesome-advent-of-code)
