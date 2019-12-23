inout
===

함수 인자로 넘어간 인자를 변경하고 싶은 경우가 있다.
하지만 함수 인자로 넘어간 값들은 immutable type이라 바꿀수 없다.

reference type인 경우 reference type안의 프로퍼티들을 바꿀수 있지만
만약 primitive data type인 경우 값을 바꿀수 없다. 

inout 키워드를 쓴다면 parameter을 reference하면서 넘길수 있다. 

~~~swift
var variable: Int = 1
func changeNumber (num:inout Int) {
    num = 2
    print(num) // 2
}
changeNumber(num : &variable)
~~~

parameter을 넘길때 **&** 붙여야한다 

Reference type을 넘길수도있다!!
