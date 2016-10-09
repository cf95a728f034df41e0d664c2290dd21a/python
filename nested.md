```python
# 求素数原始版本
import math


def is_prime(number):
    if number > 1:
        if number == 2:
            return True
            
        if number % 2 == 0:
            return False
            
        for current in range(3, int(math.sqrt(number) + 1), 2):
            if number % current == 0:
                return False
            return True
            
    return False
```

```python
# 求素数优化版本
import math


def is_prime(number):
    if number <= 1:
        return False

    if number == 2:
        return True

    if number % 2 == 0:
        return False

    for current in range(3, int(math.sqrt(number) + 1), 2):
        return number % current == 0
```


```python
# 更直观的版本，直接根据素数定义来写的，时间复杂度并不好
def get_primes(n):
    for n in range(2, n):
        for x in range(2, n):
            if n % x == 0:
                break
        else:
            yield n
```
