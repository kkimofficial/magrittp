# adverb: pipe operator

DISCLAIMER: THIS WORK IS NOT NECESSARILY A REPRESENTATION OF ANY PAST OR CURRENT EMPLOYER OF MINE

## Introduction

It is a very basic attempt to provide pipe functionality similar to R magrittr library and it's %>% operator. I believe chaining significantly improves code readability in cases when there are a lot of nested brackets.

## Installation

Import
```python
>>> from adverb import Adverb
>>> p = Adverb
```

## Overview

- `p(x) >> p(f)` is equalent to `f(x)`

```python
>>> p(-2) >> p(print) # print(-2)
-2
```

- `p(x) >> p(f) >> p(g)` is equalent to `g(f(x))`

```python
>>> p(-2) >> p(abs) >> p(print) # print(abs(-2))
2
```

- `p(x) >> p(f, y)` is equalent to `f(x, y)`

```python
>>> p(-2) >> p(pow, 2) >> p(print) # print(pow(-2, 2))
4
```

- `p(x) >> p(f, y, p)` is equalent to `f(y, x)`

```python
>>> p(-2) >> p(pow, 2, p) >> p(print) # print(pow(2, -2))
0.25
```


- In order to "unwrap" object the chain must be closed with Adverb class object
```python
>>> result = p(-2) >> p(pow, 2, p) >> p
>>> print(result)
9
```




Example with filter and map (where filter and map are standard Python functions) applied to array
```python
>>> f = Adverb
>>> f([1, 2, 3]) >>\
      f(filter, lambda x: x > 1, f) >>\
      f(map, lambda x: x ** 2, f) >>\
      f(list) >>\
      f(print)
[4, 9]
```
The above is equalent in terms of standard function notation
```python
>>> print(list(map(lambda x: x ** 2, filter(lambda x: x > 1, [1, 2, 3]))))
[4, 9]
```
