Frame Bound
===

**Frame** 과 **Bound**는 UIView의 인스턴스 프로퍼티이다

~~~swift
open var frame: CGRect
open var bounds: CGRect
~~~

둘다 CGRect 타입이다

* Frame:   
SuperView(한단계 상위)의 좌표계 안에서 View의 위치와 크기를 나타낸다

* Bounds:
자신의 좌표계에서 View의 위치와 크기를 나타낸다.

상위뷰 A 와 하위뷰 B가 있다고 했을때

A의 Bound origin을 바꿔주면 그 안에있던 하위뷰 B가 움직이는것처럼 보인다.

**Scroll View**에서 이 원리를 이용해 bound를 바꿔주면 내부의 뷰들이 움직이는것처럼 보인다