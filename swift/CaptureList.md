Closure Capture List 란
===

closure은 자신이 선언된 맥락에서 변수들과 상수들을 capture한다. Capture 한다는것은 참조를 하는게 아니라 값을 복사해서 자신이 쓴다는 뜻이다. Capture을 한후 closure은 이 변수들과 상수들이 사라지거나 변경되더라도 caputure 한 순간의 값을 가질 수 있다.

클로져에서의 강한 순환 참조
---
강한 순환 참조는 클로져에서 발생 할 수 있다. 만약 클래스의 프로퍼티에 클로져를 할당하고, 그 클로져가 클래스의 인스턴스의 프로퍼티 또는 인스턴스 자체인 self를 참조할때 강한 순환 참조가 발생한다. class와 closure가 각각을 참조하는 상황인것이다. 

Swift 는 해결책으로 Closure Capture List를 제시한다. 

클로져에서 강한 순환 참조 해결책
---
클로져를 정의할때 Closure Capture List(arrya이다)를 작성한다. 위치는 parameter 앞에 적어준다.  이들은 한개 또는 여러개의 값을 capture한다. 이제 이 값들을 weak, unowned로 참조하는것이다. 

~~~swift
//Look at that sweet, sweet Array of capture values.
let closure = { [weak self, unowned krakenInstance] in
    self?.doSomething() //weak variables are Optionals!
    krakenInstance.eatMoreHumans() //unowned variables are not.
}
~~~

unowned도 weak랑 동작이 거의 똑같다. 딱 하나 차이가 있는데 그것은, unowned는 optional이 아니다. Unowned는 초기화된후 절대 nil이 되지 않을것을 보장 할 수 있을때 쓰는것이다. ( ! 와 비슷하다 ) Closure같은 경우 unowned reference를 갖게될때 둘의 할당해제 시점이 같을때만 쓰인다. 

~~~swift
class RetainCycle {
    var closure: (() -> Void)!
    var string = "Hello"

    init() {
        closure = { [unowned self] in
            self.string = "Hello, World!"
        }
    }
}

//Initialize the class and activate the retain cycle.
let retainCycleInstance = RetainCycle()
retainCycleInstance.closure() //At this point we can guarantee the captured self inside the closure will not be nil. Any further code after this (especially code that alters self's reference) needs to be judged on whether or not unowned still works here.
~~~

closure에서 self가 nil이 아닌걸 보장 할 수 있다. 왜냐하면 초기화 되고 바로 class를 부르기 때문이다. 

