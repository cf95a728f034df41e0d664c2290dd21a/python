## 1. 迭代器
如果一个对象遵循迭代器协议(实现了\__iter__和\__next__方法)，那么它就可以被for ... in ...迭代。
range, tuple, list, dict, collection, generator均可被迭代。

## 2. 生成器
### 2.1. 定义一个生成器
如果一个方法内部包含yield关键字，那么执行些此方法时，仅会返回一个生成器对象，与迭代器一样，
它可以被for ... in ...迭代，但不同的是，仅可被迭代一次。map关键字返回的就是一个生成器。

```python
g1 = (x * x for x in range(3))

# 0, 4, 9
for item in g1:
    print(item)

# nothing
for item in g1:
    print(item)

g2 = (x * x for x in range(2))

next(g2)  # 0
next(g2)  # 4
next(g2)  # StopIteration

def f():
    yield 0
    yield 1
    yield 2

g3 = f()

# 0, 1, 2
for item in g3:
    print(item)
```

### 2.2. 生成器的初衷是为了生成一个无限序列，通常可以将其认为是一个lazy pedding list
```python
# 递归：时间复杂度为O(2^n)
def fibonacci(n):
    return n if n < 2 else fibonacci(n-2) + fibonacci(n-1)

if __name__ == '__main__':
    print(list(map(fibonacci, range(1, 10))))
```

```python
# 循环：时间复杂度为O(n)
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

if __name__ == '__main__':
    print(list(map(fibonacci, range(1, 10))))
```

```python
# 学霸君可能会想到可以用矩阵运算来加速，时间复杂度为O(logn)
# 还有Fibonacci公式可用，不过误差随着n的变大而越来越大
```

```python
# 生成器
import itertools

def take(n, iterable):
    ''' return elements from 1 to forever '''
    return list(itertools.islice(iterable, 0, n))

def fibonacci():
    a, b = (0, 1)
    while True:
        yield b
        a, b = b, a + b


if __name__ == '__main__':
    print(take(10, fibonacci()))
```

```haskell
-- 上述实现在函数式编程语言会更加简单，比如说Haskell
fibs :: [Int]
fibs = 1 : 1 : zipWith (+) fibs (tail fibs)

Prelude> take 10 fibs
[1,1,2,3,5,8,13,21,34,55]
```


### 2.3. 如何理解yield
1. Insert a line result = [] at the start of the function.
2. Replace each yield expr with result.append(expr).
3. Insert a line return result at the bottom of the function.
4. Yay - no more yield statements! Read and figure out code.
5. Compare function to original definition.


### 2.4. send
```python
def bank_account(deposited, interest_rate):
    while True:
        calculated_interest = deposited * interest_rate 
        received = yield calculated_interest
        if received:
            deposited += received


if __name__ == '__main__':
    deposited, interest_rate = 1000, 0.05
    my_account = bank_account(deposited, interest_rate)

    for i in range(1, 11):
        interest = next(my_account)
        print(i, interest)
        my_account.send(deposited + interest)
```
