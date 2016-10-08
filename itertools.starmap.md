# starmap

```python
import time
import itertools


def f(i, j):
    time.sleep(1)
    return i, j


@elapsed
def main():
    g = itertools.starmap(
        f,
        zip([i for i in range(10)], [i ** 2 for i in range(10)])
    )
    print(g)
    print(list(g))
    print(list(g))
    # next(g)
    
    
if __name__ == '__main__':
    main()
```
