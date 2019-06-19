Associated Type
===

Generic에서 placeholder 같은 역할

~~~swift

protocol sanichProtocol {
    associatedtype MyType
    var name: MyType { get }
}
~~~


~~~swift
struct Zedd: ZeddProtocol{
    var name: Int{
        return 100
    }
}
~~~

Associated Type이니 어떤걸 줘도 됨

여기서 associatedType에다 조건을 줘도됨