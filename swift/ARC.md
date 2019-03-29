Automatic Reference Counting 이란
===

# 그건 바로
https://krakendev.io/blog/weak-and-unowned-references-in-swift



ARC 작동원리
---
하나의 인스턴스를 몇개가 참조하는지 세는것.
새로운 인스턴스가 만들어 질때마다 ARC는 그 객체를 위한 메모리를 할당한다. 이 객체가 더 이상 필요가 없을때 ARC는 그 메모리를 자동으로 free 시킨다. 
객체가 필요한 순간에 할당이 해제되지 않은것을 보장하기 위해 ARC는 몇개의 프로퍼티, 상수, 변수가 이 객체를 참조하는지 세고 있는다. ARC는 하나라도 이 객체를 참조하는것이 있다면 할당 해제 하지 않는다. 객체를 프로퍼티, 상수, 변수에 할당하는 순간, 이들은 객체를 강하게 참조한다. `strong reference` Reference Counting은 클래스의 인스턴스에만 적용이된다. 

ARC Example
---


~~~swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}
~~~
이런 Person class가 있다고 하자
~~~swift
var reference1: Person?
var reference2: Person?
var reference3: Person?
~~~
위의 3개의 객체들은 옵셔널임으로 nil 이고 아직은 Person 객체를 참조하지 않는다

~~~swift
reference1 = Person(name: "John Appleseed")
reference2 = reference1
reference3 = reference1
~~~
자 이제 3개의 reference들 객체들이 하나의 Person객체를 참조하고 있다. 

~~~swift
reference1 = nil
reference2 = nil
~~~
만약 reference1 과 reference2 를 초기화 시킨다고 했을때 아직 reference3 가 Person객체를 참조함으로 이 객체는 아직 메모리 할당해제되지 않는다.   

~~~swift
reference3 = nil
~~~
최종적으로 Person 객체를 강하게 참조하고 있던것들을 없애주는 순간, Person 객체는 할당해제가 된다. 

객체들 사이의 강한 순환 참조
---

john과 unit4A가 nil이 되면 원래라면, person 인스턴스와 unit4A 인스턴스를 참조하는 개수가 각각 0이라 메모리 해제가 되어야한다. 하지만 person객체와 unit4A객체가 각각 서로를 참조하고 있기때문에 강한 순환 참조가 발생한다.  
코드를 작성하다보면, 객체가 절대로 강한 참조당하는 


Weak 과 Unowned 참조
---
Weak는 객체를 참조 하지만, 객체가 ARC에게 메모리해제 되는것을 막지 않는다. 다르게 말하면 weak reference는 retain count를 1 증가 시켜주지 않는다. 그리고 객체가 할당해제 될때 포인터도 해제 시켜준다. weak는 var로 선언이 되는데 그 이유는 언제든 nil이 될 수 있기 때문이다. 

Weak
---
인스턴스가 메모리 해제 되어도, weak Reference가 아직 참조하고 있는 상황이 가능하다. 따라서 ARC가 자동으로 인스턴스가 메모리 해제될때 weak Reference를 nil로 해준다. 

![weak](/swift/img/Weak.png)
위의 예시처럼 이제 Apartment 인스턴스는 Person 인스턴스를 약하게 참조한다. 따라서 만약 john을 nil로 하면 이제 Person 인스턴스를 참조하는건 reference counting 이 0이 됨으로 Person Instance는 메모리 해제가 된다. 

![weak2](/swift/img/Weak2.png)
Person 인스턴스가 사라지니 tenant도 nil이 된다. 

Unowned References 
---
Weak와 역할이 똑같지만, 상대 인스턴스가 reference와 같거나 긴 수명주기를 가질때 쓴다. 이 reference는 절대 nil이 되지 않는다고 기대된다. 따라서 ARC는 절대로 nil로 세팅하지 않는다. Unowned는 unowned가 참조하는 객체가 메모리 해제 되지 않은 인스턴스를 참조할떄만 사용해야 한다. 

![unowned](/swift/img/unowned.png)
customer는 creditcard를 가질수도있고 안가질수도 있지만, creditcard는 무조건 customer을 가져야 하는 상황이다. 
creditcard 인스턴스의 customer는 unowned referecne로 customer인스턴스를 참조한다. 

![unowned](/swift/img/unowned2.png)
여기서 john = nil이 라하면 customer를 참조하는게 없으니 customer인스턴스가 메모리 해제 된다. creditcard인스턴스를 유일하게 참조하고 있던 customer가 사라지니 ARC에 의해 순차적으로 creditCard가 메모리 해제된다.  


클로져에서 강한 순환 참조
---
[capturelist](/swift/CaptureList.md) 쪽을 읽자
