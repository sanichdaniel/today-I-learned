How to find Memory Leak
===

Debug Memory Graph
---

1) Scheme에서 malloc Stack logging을 켜준다
2) 메모리그래프에서 메모리 누수가 의심되는 곳을 찾는다

* 장점  
한번에 모든 memory leak들을 볼 수 있고, 운 좋게 모르던 메모리 누수를 찾을 수 있다.
* 단점
메모리 누수가 아닌데 메모리 누수라 하는 경우가있다. 

Instrument
---
Xcode profile에서 실행시켜 런타임에 메모리를 확인할수있다.


Library LifetimeTracker
---
메모리 누수가 자주 일어나는 뷰컨트롤러, 뷰모델의 초기화 부분에 셋업을 해주면 개발하면서 메모리 누수가 일어나는지 확인할수있다.

* 단점 - 라이브러리 종속성