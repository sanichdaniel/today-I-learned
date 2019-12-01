Dispatch Queue
===

* 정의: closure로 구성된 task를 큐에다가 등록해 두면 별도의 쓰레드에서 실행

Dispatch queue type
---

Serial Queue
---
큐에 추가된 순서대로 한번에 하나의 task를 실행합니다.

Concurrent Queue
---

동시에 하나 이상의 task를 실행하지만 task는 큐에 추가된 순서대로 게속 시작됩니다.

 Main dispatch queue
 ---
 Main 쓰레드에서 task실행


 Dispatch Queue를 사용하면 쓰레드 생성 및 관리에 대해 신경을 안써도 된다. 


A *Synchronous* function returns control to the caller after the task is completed.
An *asynchronous* function returns immediately, ordering the task to be done but not waiting for it. Thus, an asynchronous function does not block the current thread of execution from proceeding on to the next function.

Concurrency is the notion of multiple tasks running at the same time.

GCD is built on top of threads. Under the hood it manages a shared thread pool. GCD can improve your app’s responsiveness by helping you defer computationally expensive tasks and run them in the background.

ios에서 멀티 쓰레딩: 

Threads, Grand Central Dispatch, NSOperation