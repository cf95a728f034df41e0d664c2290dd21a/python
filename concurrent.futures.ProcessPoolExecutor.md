# 使用进程池

[processpoolexecutor](https://docs.python.org/3/library/concurrent.futures.html#processpoolexecutor)

## submit


```python
import time
import random
from concurrent.futures import ProcessPoolExecutor


def f1(a, b=''):
    print('<{}, {}>'.format(a, b))
    time.sleep(3)
    print('</{}, {}>'.format(a, b))
    

def f2(a, b=''):
    time.sleep(3)
    return '{}, {}'.format(a, b)


def main():
    with ProcessPoolExecutor(max_workers=10) as executor:
        for i in range(30):
            executor.submit(f1, i, b=[ 'x', 'y', 'z'][random.randint(0, 2)])
            
        for i in range(5):
            future = executor.submit(f2, i, b=[ 'x', 'y', 'z'][random.randint(0, 2)])
            print(future.result())

if __name__ == '__main__':
    main()
```

## map
map(func, *iterables, timeout=None, chunksize=1)
