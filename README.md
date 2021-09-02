# Codex Test Cases

As a fan of [Machine Learning Street Talk](https://www.youtube.com/channel/UCMLtBahI5DMrt0NPvDSoIRQ) podcast I thought it would be cool to go back over some of the reservations about GPT-3s raised in the podcast and see if [Open AIs codex](https://openai.com/blog/openai-codex/) resolved any of them.

### Sorting

https://youtu.be/iccd86vOz3w?t=1630

in:
```python
"""
Example of sorting a list in python without using `sort` or `sorted`
"""
```

out:
```python

def sort_list(lst):
    """
    Sort a list in place
    """
    for i in range(len(lst)):
        for j in range(i, len(lst)):
            if lst[i] > lst[j]:
                lst[i], lst[j] = lst[j], lst[i]
    return lst

if __name__ == '__main__':
    lst = [1, 5, 3, 2, 4]
    print(sort_list(lst))```
```

run:
```python
>>> def sort_list(lst):
...     """
...     Sort a list in place
...     """
...     for i in range(len(lst)):
...         for j in range(i, len(lst)):
...             if lst[i] > lst[j]:
...                 lst[i], lst[j] = lst[j], lst[i]
...     return lst
...
>>> if __name__ == '__main__':
...     lst = [1, 5, 3, 2, 4]
...     print(sort_list(lst))
...
[1, 2, 3, 4, 5]
```

### Substitution Cipher

https://youtu.be/iccd86vOz3w?t=2670

First attempt failed, I had to add example usage of the model and `class Cipher` to get past the sklearn imports!

in:
```python
"""
Example of a class that follows the sci-kit learn compliant model that learns a substitution cipher

model = Cipher()
model.fit(["cat", "hat"], ["ybh", "qbh"])
model.predict(["mat"])
"obh"
"""

class Cipher:
```

out:
```python
    def __init__(self):
        self.mapping = {}

    def fit(self, X, y):
        for x, y in zip(X, y):
            for x_char, y_char in zip(x, y):
                self.mapping[x_char] = y_char

    def predict(self, X):
        return [self.mapping[x_char] for x_char in X]
```

 run:
```python
>>> class Cipher:
...     def __init__(self):
...         self.mapping = {}
...     def fit(self, X, y):
...         for x, y in zip(X, y):
...             for x_char, y_char in zip(x, y):
...                 self.mapping[x_char] = y_char
...     def predict(self, X):
...         return [self.mapping[x_char] for x_char in X]
...
>>>
>>> model = Cipher()
>>> model.fit(["cat", "hat"], ["ybh", "qbh"])
>>> model.predict(["mat"])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 9, in predict
  File "<stdin>", line 9, in <listcomp>
KeyError: 'mat'
```

NB: This is a shame, so close, just needed to iterate over the chars in X

### Rubix cube

https://youtu.be/iccd86vOz3w?t=5108

in:
```python
"""
Example of a function that returns the next action to solve a rubik cube
"""
```

out:
```python
def solve(cube):
    """
    Solves a rubik cube
    """
    return "R"
```

### Boiling water

https://youtu.be/iccd86vOz3w?t=9162

in:
```python
"""
Example of a function that returns whether or not water is boiling based on temperature
"""
```

out:
```python

def is_water_boiling(temp):
    """
    Returns whether or not water is boiling based on temperature
    """
    return temp >= 100

print(is_water_boiling(100))
print(is_water_boiling(50))
```

run:
```python
>>> def is_water_boiling(temp):
...     """
...     Returns whether or not water is boiling based on temperature
...     """
...     return temp >= 100
...
>>> print(is_water_boiling(100))
True
>>> print(is_water_boiling(50))
False
>>>
```

### Nth digit of pi

I remember Keith giving this as an example, but can't find the timestamp.

in:
```python
"""
Example of a function that returns the nth digit of pi
"""
```

out:
```python

def nth_digit_pi(n):
    """
    Returns the nth digit of pi
    """
    # The nth digit of pi can be calculated using the following formula:
    # https://en.wikipedia.org/wiki/Chudnovsky_algorithm
    # k * (545140134 * k + 13591409) / (3 * k ** 3 - k ** 2 + 1)
    # where k = n - 1
    #
    # The following code implements the formula and calculates the nth digit of pi
    k = n - 1
    pi_k = k * (545140134 * k + 13591409) / (3 * k ** 3 - k ** 2 + 1)
    return int(str(pi_k)[-1])

# Print the first 20 digits of pi
for i in range(1, 21):
    print(nth_digit_pi(i))
```

run:
```python
>>> def nth_digit_pi(n):
...     """
...     Returns the nth digit of pi
...     """
...     # The nth digit of pi can be calculated using the following formula:
...     # https://en.wikipedia.org/wiki/Chudnovsky_algorithm
...     # k * (545140134 * k + 13591409) / (3 * k ** 3 - k ** 2 + 1)
...     # where k = n - 1
...     #
...     # The following code implements the formula and calculates the nth digit of pi
...     k = n - 1
...     pi_k = k * (545140134 * k + 13591409) / (3 * k ** 3 - k ** 2 + 1)
...     return int(str(pi_k)[-1])
...
>>> # Print the first 20 digits of pi
>>> for i in range(1, 21):
...     print(nth_digit_pi(i))
...
0
6
1
8
4
5
3
7
6
7
8
3
5
4
3
8
3
5
2
9
```

NB: I was sure it had nailed this until I ran it!

### Parameters:

| Engine            | davinci-codex            |
|-------------------|--------------------------|
| Response length   | tweaked for each problem |
| Temperature       | 0                        |
| Top P             | 1                        |
| Frequency penalty | 0                        |
| Presence penalty  | 0                        |
| Best of           | 1                        |
