 swift properties
 ===

 prperty 의 정의

 값을 특정 class, struct, enum에 연결한다

3가지 종류의 property가 있다.

 * stored Property
 * computed Property
 * type property

 stored Property 는 constant와 variable값을 인스턴스 일부로 저장. class랑 struct에서만 사용

 computed Property는 값을 연산한다. class, struct, enum에서 사용

 stored, computed property는 특정 타입의 인스턴스와 연결된다.

 propery를 타입 자체와 연결할 수도 있다. Type Property라고 한다.

 
 Stored Property
 ---
 class와 strurct 인스턴스의 일부인것

 Lazy Stored Properties
 값이 사용되기 전까지는 값이 계산되지 않는 property
 값이 필요할때 초기화를 한다



 Computed Property
 ---
 값을 저장하기 보다는 그떄그때 특정한 연산을 통해 값을 리턴해준다. 
getter 와 setter이 연산 프로퍼티

getter, setter을 사용하려면 그 연산된 값을 저장할 변수가 있어야한다.

~~~swift
class Point {
    var tempX : Int = 1
    var x: Int {
        get {
            return tempX
        }
        set(newValue) {
            tempX = newValue * 2
        }
    }
}
var p: Point = Point()

p.x = 12
~~~


~~~swift
set {
     tempX = newValue * 2
}
~~~
shorthand setter declaration인데
무조건 newValue키워드 사용

나중에 p.x = 12 한다면
x에는 24가 저장된다.

Read-Only Computed Properties
---
연산 프로퍼티는 get, set 둘다 가질 수 있지만, get만을 가질 수 있다. (set만 가지는건 안됨)


~~~swift
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        return width * height * depth
    }
}
~~~
volume이 값을 가지고있는게 아니라 width * height * depth가 값을 가지고있는것

 Type Property
 ---
1. used on the type(class/struct/enum) instead of the instance of that type.

2. Type Properties are defined with the keyword static.
3. Static Type Properties can’t be overridden in the subclass. The keyword class is used on the computed properties in this case.

 모든 타입이 사용할 수 있는 상수 프로퍼티, 글로벌 변수 프로퍼티같이 특정 타입의 모든 인스턴스에 공통적인 값을 정의하는 데 유용합니다. 
 
 타입 프로퍼티에는 저장 타입 프로퍼티, 연산 타입 프로퍼티가 있다
