---
title: Multi-Programing
subtitle: Thread 와 Process 사용법
layout: page
show_sidebar: false
menubar: Python
---

# Multi-Processing

```python
import multiprocessing,time
def count(d):
    while(d<=15):
        print(d)
        time.sleep(1)
        d += 1
if __name__ == '__main__':
    p1 = multiprocessing.Process(target=count,args=(3,)) # Thread 생성법과 유사
    p2 = multiprocessing.Process(target=count,args=(3,))
    p1.start()
    time.sleep(2)
    p2.start()
```
