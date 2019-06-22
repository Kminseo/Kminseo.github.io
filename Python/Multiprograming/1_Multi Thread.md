---
title: Multi-Programing
subtitle: Thread 와 Process 사용법
layout: page
show_sidebar: false
menubar: Python
---

# Multi Threads

## PYQT에서는 QThread 사용해야함.

QBasicTimer 외 몇몇 QT패키지가 일반 Thread위에서 사용 시 동작하지 않음

### Python Thread Coding

일반적인 프로세스는 하나의 루틴을 가지고 직력적으로 순서대로 일을 처리한다. 하지만 쓰레드를 사용하는 경우에 하나의 프로세스 안에  여러개의 루틴을 만들어 병렬적인 방법으로 프로그램을 실행하는 것이 가능하다.

파이썬에서 Thread 모듈을 사용하기 위해 threading 을 import 시켜야 사용할 수 있다.


```python
import threading, time
def count():
    count = 0
    while(count<=10):
        print(count)
        count+=1 
        time.sleep(1)

t1 = threading.Thread(target=count) # t1에 thread를 할당시키고 목표함수는 count함수를 실행
t1.start() # t1의 thread 시작
time.sleep(3) 
t2 = threading.Thread(target=count) # t2에 thread를 할당시키고 목표함수는 count함수를 실행
t2.daemon=True # t2의 객체를 데몬 thread로 지정
t2.start() # t2의 thread 시작
```
#### Daemon Thread

```python
t2.daemon=True
```

데몬쓰레드는 백그라운드 쓰레드로 메인 쓰레드가 종료되면 같이 종료되는 쓰레드이다. 데몬스레드로 지정을 하지 않을 경우 메인 스레드가 종료되도 서브 스레드는 계속 동작한다.

#### Thread class


```python
import threading, time
class counter(threading.Thread):
    def __init__(self):
        threading.Thread.__init__(self) #class안에 thread객체를 넣어준다.
        self.count = 0
    def run(self):
        while (self.count <= 10):
            print(self.count)
            self.count += 1
            time.sleep(1)

if __name__=="__main__":
    object = counter() # object를 class로 생성
    object2 = counter()
    object2.daemon=True # object2 객체를 daemon Thread로 지정함.
    object.start() # start()함수를 사용하면 class안에 run()함수가 실행된다.
    time.sleep(3)
    object2.start()
```
[https://niceman.tistory.com/139?category=940952](https://niceman.tistory.com/139?category=940952)

# Python Thread timer

기초적인 파이썬 타이머 호출 방법

```python

import threading

class AsyncTask:
    def __init__(self):
        pass
    def TaskA(self):
        print 'Process A'
        threading.Timer(1,self.TaskA).start() # Timer 1초 간격으로 Task A 실

def main():
    print 'Async Function'
    at = AsyncTask()
    at.TaskA()

if __name__ == '__main__':
    main()
```

join\(\) 종료할때까지 대기

cancel\(\) 현재 진행중신 쓰레드 제거.

# Thread Using Tip

#### Flag를 사용하여 코딩

Thread를 사용할 때 class나 전역변수에서 특정 flag를 True, False에 의해서 동작하도록 코딩하여 Thread를 죽이지 않고 잠깐동안 정지하거나 할 때 유용하게 코딩하는 것이 가능하다.


