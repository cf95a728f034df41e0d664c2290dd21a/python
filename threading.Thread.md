# 继承线程类

```python
import time
from threading import Thread

        
class MyThread(Thread):
    def __init__(self, i):
        Thread.__init__(self)
        self.i = i

    def run(self):
        self.task()
        
    def task(self):
        print('<{}>'.format(self.i))
        time.sleep(3)
        print('</{}>'.format(self.i))
        
@elapsed
def main():
    dt = datetime.now()
    
    # create
    threads = [MyThread(i) for i in range(10)]

    # start
    for t in threads:
        t.start()
    
    # wait
    for t in threads:
        t.join() 
        
  
  
if __name__ == '__main__':
    main()
```
