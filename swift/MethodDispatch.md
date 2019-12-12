Method Dispatch
===

Method Dispatch는 어떤 method를 실행할지 결정하는 알고리즘이다. 어느 시점에서 어떤 method를 실행하는지 아느냐에 따라 **Dynamic Dispatch**와 **Static Dispatch**가 있다. 2개념에 앞서 일단 **virtual table** 개념을 알고 넘어가자

virtual table
---
virtual table은 자신의 class 내부에 있는 method들에 대한 함수포인터의 어레이들이다. 자식 class는 자신의 v-table과 부모 class의 v-table들을 가지고 있다. 


Static Dispatch
---
*컴파일 타임*에 어떤 메소드를 실행할지 결정할 수 있다.

Dynamic Dispatch
---
*런타임*에 virtual method table을 조회에서 어떤 method를 실행할지 결정한다.  
이것은 static dispatch보다 많은 오버헤드를 필요로 한다.

Method Disptach
---
*Todo*

 Dynamic Dispatch를 이용하는 경우는 polymorphism 때문. 

![weak](/swift/img/polymorphism.png)

Dynamic Dispatch를 하고 싶지 않은 경우 ( Optimization )
---
- **Final** 키워드를 이용하자. final 키워드를 통해 이 class는 override될 수 없다를 알린다. 그러면 해당 method는 static dispatch 된다. 

- **Private** 키워드를 이용하자. 컴파일러가 메소드의 overriding 선언을 찾아보고 없으면 **final**로 만들어준다.

Swift가 실제로 distpatch 할때 고려하는것
---
- 선언된 위치
- 참조 타입

### 선언된 위치

 swift는 메소도를 선언할 수 있는곳이 두군데로 정해진다. 첫째, 타입이 선언된곳. 둘쨰 extenstion 안.

어디에 선언되었냐에 따라 사용되는 dispatch가 다르다.


![weak](/swift/img/locationDispatch.png)

### 메소드가 불린 타입에 따라서 사용되는 dispatch가 다르다

~~~swift
protocol MyProtocol {
}
struct MyStruct: MyProtocol {
}
extension MyStruct {
    func extensionMethod() {
        print("In Struct")
    }
}
extension MyProtocol {
    func extensionMethod() {
        print("In Protocol")
    }
}
 
let myStruct = MyStruct()
let proto: MyProtocol = myStruct
 
myStruct.extensionMethod() // -> “In Struct”
proto.extensionMethod() // -> “In Protocol”
~~~

proto.extensionMethod()에서 "In Struct"가 불릴꺼 같지만 "In Protocol"이 불린다. 그 이유는 proto 인스턴스의 타입이 프로토콜이라 프로토콜이 사용할 수 있는 함수들을 먼저본다. 프로토콜이 사용할 수 있는 함수는 *extension MyProtocol* 안에 있음으로 static dispatch를 쓰게된다. 

만약 extensionMethod가 프로토콜 안에 선언되었다면 dynamic dispatch가 적용되어 struct안의 함수가 불렸을것이다.



![weak](/swift/img/dispatchSummary.png
)

참고할만한 링크
https://medium.com/@leandromperez/protocol-extensions-gotcha-9ef1a42c83b6

더 추가해야할 내용
https://zeddios.tistory.com/597?category=685736

