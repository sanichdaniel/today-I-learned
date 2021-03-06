Clean Architecture
===

앱이 레이어로 구분지어져 있다. 안쪽 레이어는 바깥쪽 레이어를 몰라야한다

소프트웨어를 계층(layer)로 나눠서 관심사를 분리함.  

 
이렇게만 하면 어떤 소프트웨어가 만들어지냐면

1. Independent of Frameworks. 아키텍쳐는 소프트웨어 라이브러리의 존재에 의존하지 않음.

2. Testable. 비즈니스 로직은 UI, DB, 웹 서버 또는 기타 외부 요소 없이 테스트 할 수 있음.

3. Independent of UI. UI는 시스템을 변경하지 않고도 쉽게 변경 가능. (ex. 비즈니스 로직을 바꾸지 않고 웹 UI를 콘솔 UI로 변경가능.)

4. Independent of Database. 비즈니스 로직이 DB에 바인딩 되지 않음. 

5. Independent of any external agency. 비즈니스 로직은 외부 세계;;(outside world에 대해 전혀 알지 못함



출처: https://zeddios.tistory.com/1065 [ZeddiOS]

Solid Principle
---

### 1) Single Responsibility
    - 단일 책임의 원칙.
### 2) Open Closed
    - 기존의 코드를 변경하지 않으며 기능을 추가 할 수 있도록
    - 확장 개방적, 수정에는 폐쇄적
### 3) Liskov substitution
    - 자식 클래스는 언제나 부모 클래스의 역할을 대체할 수 있어야 한다
    - 대체 할 수 없다면, 상속관계가 아닐수도
### 4) Interface Segreagation
    - 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다
### 5) Dependency Inversion
    - 하이 레벨 모듈은 로우 레벨 모듈에 의존하되, 둘다 추상에 의존해야 한다.
    - 상세는 추상에 의존해야한다. 

Clean Architecture
---
좋은 아키텍쳐는 비지니스 로직(UseCase)에 집중해야한다. 

Layer 들을 분리시켜서 코드를 쉽게 바꿀수 있다.

테스트가 쉬워진다.

코드 재사용성이 올라간다.
 
![unowned](/swift/img/iosArchitecture.png)  
Clean Architecture 그래프에 따르면 안쪽 레이어는 바깥쪽 레이어에 대해 의존성을 가지면 안된다. 즉 바깥에서만 안에 내용을 알 수 있는것.

### Domain Layer  
>가장 안쪽의 다른 레이어들과는 독립적인 레이어. 비지니스로직, Entities, Use Cases, and Repository Interfaces를 가진다. 
UseCase는 비지니스 로직인데, 앱에서는 유저가 보낸 데이터로 리포지토리에 데이터를 요청하고 이걸 다시 뷰모델에 전달한다 
### Presentation Layer
>UI(UIViewController, SwiftUI, ViewModel)를 가진다. Domain Layer에만 종속된다.
### Data Layer  
>Repository 구현체가 포함되어있다. Data를 도메인에게 전달한다. Domain Layer은 인터페이스로 접근 한다. 

![unowned](/swift/img/iosClean.png)
![unowned](/swift/img/layers.png)


### Data Flow

1. UI 는 Presenter/ViewModel의 메소드 호출
2. Presenter/ViewModel이 Use case코드를 실행
3. Use case에서 Respository에서 데이터를 가져오기
4. Repository는 데이터 소스에서 데이터를 리턴한다
5. UI에게 다시 데이터를 뿌려준다

References
---
https://tech.olx.com/clean-architecture-and-mvvm-on-ios-c9d167d9f5b3

https://github.com/kudoleh/iOS-Clean-Architecture-MVVM?source=post_page-----c9d167d9f5b3----------------------
