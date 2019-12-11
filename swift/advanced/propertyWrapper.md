Property Wrapper
===

> 프로퍼티를 구현할때 반복적으로 나오는 패턴이 있다면 "Wrapper"을 만들어서 반복을 없애자

Property Wrapper을 정의할려면 struct, class, enum을 만들고 **wrappedValue** 프로퍼티를 정의해야한다. 


~~~swift
struct SmallRectangle {
    @TwelveOrLess var height: Int
}

// is transformed to

struct SmallRectangle {
    private var _height = TwelveOrLess()
    var height: Int {
        get { return _height.wrappedValue }
        set { _height.wrappedValue = newValue }
    }
}
~~~

Project Value
---
*Projected Value* **$** 를 통해 접근