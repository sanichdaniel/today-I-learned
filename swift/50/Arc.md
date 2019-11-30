ARC
===

Automatic Reference Count는 ios에서 메모리를 관리하는 방식이다. 프로퍼티, 상수, 변수에 레퍼런스가 지정되면 reference count를 증가시킨다. reference count를 세면서, 0이 되기전까지는 메모리에 유지시켜주고, reference count가 0이되면 메모리 해제.

Strong Reference Cycle
---
reference type들이 서로를 참조해서, reference count가 0이 안되고, 메모리 에서 살아있는 상황.

강한 순환 참조가 발생하는 상황
---

* closure에서 self
* delegate

강한 순환 참조를 해결하는 방법
---
* weak, unowed 키워드
weak하게 참조되면 reference count를 증가시키지 않는다.
키워드로 weak, unowned가 있다. weak 프로퍼티는 옵셔널이다. weak는 할당해제시 nil이 됨. unowned는 nil이 되면 안되고 unowned가 참조하는 객체가 메모리 해제 되지 않은 인스턴스를 참조할떄만 사용해야 한다. 사용자, 신용카드 예제
