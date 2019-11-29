Access Control (접근 제어)
===

객체지향의 기본 개념 캡슐화, 은닉화, 추상화, 상속성, 다형성중 은닉화에 관한 내용

* 모듈: . 모듈은 코드의 묶음 단위로 프레임워크, 라이브러리, 어플리케이션처럼 배포할 코드들의 묶음을 나타낸다. 즉 하나의 프레임워크는 하나의 모듈이고 우리가 Xcode로 만드는 프로젝트 역시 하나의 모듈이다. 그리고 우리는 import를 통해 외부 모듈을 사용할 수 있다.
* 소스파일: 단일 Swift 소스 코드 파일

1) open, public차이  
* open은 클래스 클래스멤버에만

* 외부 모듈에서 import한곳에서 subclass, override가능

2) internal

 * 모듈내에서 기본접근수준 

3) file private 
* 소스코드

4) private:
* enclosing 선언과 동일 파일내의 extension

swift guiding principle
---

1. internal, fileprivate, private타입안에서 public변수를 정의할 수 없습니다. 왜냐하면 해당 타입은 public변수가 사용되는 모든곳(내부모듈, 외부모듈)에서 사용 할 수 없기 때문입니다. 



2. 함수는 해당 매개변수 타입 및 리턴 타입보다 더 높은(덜 제한적인) 접근 수준을 가질 수 없습니다. 왜냐하면 해당 타입을 주변 코드에서 사용할 수 없는 상황에서 함수를 사용할 수 있기 때문입니다. 

출처: https://zeddios.tistory.com/389 [ZeddiOS]