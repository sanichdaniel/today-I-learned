Copy on Write
===

Copy on Write는 struct을 복사할때 퍼포먼스를 증가시키는 방법이다.

10000개의 아이템을 들고있는 어레이가 있다고 하자. 이 어레이를 다른 변수에 대입할 경우 10000개의 아이템을 다 복사해야한다. 

해결책
---

**Copy on Write**  
2개의 어레이들은 같은 데이터를 가리키고있다. 언제까지? 두번째 어레이의 값이 변하기 전까지

즉 값이 바뀔때 복사를 하는것을 Copy on write라고 한다.

지원되는 곳
---
String, Collection Types( array, set, dictionary )
