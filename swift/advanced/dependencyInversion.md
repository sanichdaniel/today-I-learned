Dependency Inversion in Swift
===

> http://blog.cleancoder.com/uncle-bob/2016/01/04/ALittleArchitecture.html  
https://clean-swift.com/dependency-inversion-a-little-swifty-architecture/  
> 2개의 글을 정리

~~~swift
protocol Receiver
{
  func receiveThis()
}
 
class Sender
{
  private var receiver: Receiver
 
  init(r: Receiver)
  {
    receiver = r
  }
 
  func doSomething()
  {
    receiver.receiveThis()
  }
}


class SpecificReceiver: Receiver
{
  func receiveThis()
  {
    // do something interesting.
  }
}
 
~~~

Traditional Dependency
---
![unowned](/swift/img/inversion2.png)

일반적인 경우에는 Sender class가 상위 모듈이고 Specific Receiver가 하위 모듈이다.  
전통적으로는 Sender 클래스가 Sepcific Receiver 인스턴스를 만들고, Specific Receiver의 함수를 호출한다. 

Dependecny Inversion
---
![unowned](/swift/img/inversion1.png)
Receiver라는 SpecificReceiver의 프로토콜을 정의한다. 이제 Sender class과 SpecificReceiver 둘다 Receiver 프로토콜이라는 추상화에 의존하게 된다. 

이제 SpecificReceiver class는 Receiver 프로토콜을 따르는 다른 class에 의해 대체 될 수 있다.

왜 Dependency Inversion이 중요한가?
---
~~~swift
class Sender
{
  private var receiver: SpecificReceiver
 
  func doSomething()
  {
    receiver.receiveThis()
  }
}
~~~
dependency inversion이 없었더라면 SpecificReceiver이라는 구현체 타입 receiver에서 함수를 직접 호출을 해야한다. 이렇게 되면 상위 모듈 Sender가 하위 모듈 SpecifirReceiver에 의존하게 된다.

만약 SpecificReceiver을 바꾸려한다면 Sender도 바꿔야한다. 

Dependency Inversion을 가능하게 하는것은?
---
Polymorphism
*  variable이 concrete(class) 타입이 아니라 abstract(protocol) type이 될 수 있게 해준다. 

* 런타임에는 concrete type이 되겠지만 컴파일 타임에는 concrete type을 가질 필요가 없다. 

* Dependency Inversion은 source code 의존성만 바꿔준다. 런타임 의존성은 여전히 상위 모듈에서 아래 모듈로. 

Dependency Inversion 의 또 다른 장점
* Unit Test를 할때 TestService등으로 갈아끼워서 테스트를 더 빠르게 진행 할 수 있다. 

