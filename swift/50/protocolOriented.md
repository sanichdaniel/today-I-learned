Protocol Oriented Language
===

*객체지향* 이란 하나의 역할을 수행하는 '메소드와 변수(데이터)'의 묶음인 객체를 만들고 객체들간의 상호작용을 통해 로직을 구성하는 프로그래밍 방식

객체지향의 단점으로 상속을 했다면, 의도하지 않은 많은 속성을 공유해야한다. 또한 단 하나의 SuperClass만 상속할 수 있다.

POP는 필요한 부분만 프로토콜로 분리가능하다. 다중 프로토콜도 구현할 수 있다. 

또한 프로토콜 규칙을 class, struct, enum에도 적용할 수 있다.

필요한 기능들을 분리하여 Protocol Extension을 만들수있다. 

(swift는 protocol 의 extension에서 기능을 구현해놓을수있다)