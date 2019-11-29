Class vs Struct
===

둘의 공통점
---
1) 값을 저장하기 위한 프로퍼티 가질수 있다, 함수, subscript를 정의할수있다.
2) extenstion을 이용해 extend할 수 있다.
3) 생성자 존재

Class만의 특징
---
1) 상속 가능
2) 참조 타입
3) Deinitializer가 존재

Value type (값 타입): 값을 복사할때 매번 새로운 인스턴스를 만들어낸다. 그래서 하나의 인스턴스를 바꾼다고 다른 인스턴스가 바뀌지 않는다.

Reference type(참조 타입): 참조가 복사되기에 모든 인스턴스는 데이터를 공유하고, 하나의 인스턴스를 바꾸면 다른 인스턴스가 바뀐다.

* Reference type은 Heap, value type은 stack에 할당된다
Stack은 static 메모리 할당, Heap 은 dynamic 메모리 할당

Heap은 사용되지 않는 메모리를 ARC를 이용해 찾아야하고, 쓰레드 문제까지 있어서 stack에 할당하는것보다 메모리 할당에 시간이 더 걸린다.

Reference 타입은 참조는 stack에 값은 heap에, value type은 stack에
class는 reference count overhead까지 있다.

 Escaping Closure:- An important note to keep in mind is that in cases where a value stored on a stack is captured in a closure, that value will be copied to the heap so that it's still available by the time the closure is executed.

* Struct는 값(Value)이다. 정확히, 값의 타입을 정의하기 위해 사용한다.

* 대입시 내용이 복사된다.

* 참조 카운트가 없어서 메모리 관리에 안전하다.

* 레퍼런스 형태가 아니기 때문에 공유가 불가능하다.

* 불변성(Immutable) 구현에 유리하다.

* 멀티스레딩에 안전하다.

* 상속이 불가능하다. 하지만 프로토콜은 사용 할 수 있다. (protocol extension 이용하기)

* 상속이 안되기에 struct의 함수는 static dispatch되어 런타임 시간을 벌 수 있다.

struct를 사용할곳
---
* 불변성(Immutable)이 필요한 데이터 타입
* 적은 데이터, 즉 멤버 프로퍼티의 갯수나 차지하는 메모리 용량이 적은 타입
* 대입 보다는 생성되는 경우가 많은 타입
* 공유될 필요가 없는 타입
* 클래스 타입 등 레퍼런스에 기반한 자료형을 저장용 프로퍼티로 쓰지 않는 경우

class를 상용할곳
---
* 공유되는 변할수있는 상태를 가지고 싶을때

struct mutate할때 var로 선언해야하는 이유
---

struct는 값타입이기에 필드를 mutate한다면, 새로운 struct를 만들어서 대입한다.

When we call our mutating scaleBy function, it actually replaces the original rectangle stored in the myRect variable with a brand new rectangle (with the new scaled width and height in our case).


성능 개선
https://medium.com/flawless-app-stories/static-vs-dynamic-dispatch-in-swift-a-decisive-choice-cece1e872d