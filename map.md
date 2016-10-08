# map

[map](https://docs.python.org/3/library/functions.html#map)

```python
import time


def f(i):
    time.sleep(1)
    return i * 2


@elapsed
def main():
    g = map(f, [i for i in range(10)])
    print(g)
    print(list(g))
    print(list(g))
    # next(g)
    
    
if __name__ == '__main__':
    main()
```
