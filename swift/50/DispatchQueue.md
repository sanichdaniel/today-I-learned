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


* Sync: 작업을 끝날때까지 caller에게 return 을 안한다.  

* async: sync와는 달리 작업을 전달하자마자 return하고 다음 작업을 실행한다.

* concurrency: 동시에 여러개의 task를 수행

* GCD는 쓰레드들 위에 지어져있다. GCD는 비싼 task들을 백그라운드나 다른 쓰레드에서 실행하게 함으로서 앱의 반응성을 높인다.

ios에서 멀티 쓰레딩: 

Threads, Grand Central Dispatch, NSOperation