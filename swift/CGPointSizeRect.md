CGPoint, CGSize, CGRect의 개념들

**CGPoint**: 2차원 좌표계를 나타내는 구조체 

~~~swift
public struct CGPoint {
    public var x: CGFloat
    public var y: CGFloat
}
~~~

**CGSize**: 너비와 높이를 가진 구조체
~~~swift
public struct CGSize {
    public var width: CGFloat
    public var height: CGFloat
}
~~~

**CGRect**: 사각형의 위치와 크기를 가지는 구조체
~~~swift
public struct CGRect {
    public var origin: CGPoint
    public var size: CGSize
}
~~~

출처: https://zeddios.tistory.com/201 [ZeddiOS]