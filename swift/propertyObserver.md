Property Observer 
===

Property Obersever은, property 값의 변화를 관찰하고 반응한다.

Property Observer은, property의 값이 set될때마다 불리고, 새로운 값이 과거의 값과 바뀌더라도 불린다. 

얘내는 var로 선언된다. 왜냐하면 계속 바뀌는 property이기 떄문이다.

initial value를 set 할때, willSet과 didSet은 불리지 않는다.

이들은 default 인자로 newValue와 oldValue를 가지고있다.