Automatic Reference Counting 이란
===

# 그건 바로



ARC 작동원리
---
새로운 인스턴스가 만들어 질때마다 ARC는 그 객체를 위한 메모리를 할당한다. 이 객체가 더 이상 필요가 없을때 ARC는 그 메모리를 자동으로 free 시킨다. 
객체가 필요한 순간에 할당이 해제되지 않은것을 보장하기 위해 ARC는 몇개의 프로퍼티, 상수, 변수가 이 객체를 참조하는지 세고 있는다. ARC는 하나라도 이 객체를 참조하는것이 있다면 할당 해제 하지 않는다. 객체를 프로퍼티, 상수, 변수에 할당하는 순간, 이들은 객체를 강하게 참조한다. `(strong reference)`

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