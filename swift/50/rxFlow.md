RxFlow
===

Navigation을 reactive하게 바꿔주는 framework.

기존의 navigation. 뷰컨에서 다른 뷰컨을 호출, storyboard segue. 

문제점
---
앱이 커지며 navigation이 복잡해짐
의존성이 커짐
재사용성이 떨어짐

철학적 문제
---
화면 그리기 담당인 뷰컨이 navigation을 하는건 철학적으로 맞지 않다.

RxFlow
---

Naviagtaion은 Coordinator가 담당

* Step
* Stepper
* Flow
* Presentable
* FlowContributor
* Coordinator

Step
---
navigation state이다

예시) 결제가 끝낸 상태, 로그인을 한 상태

Stepper
---
Step을 발생시키는 모든것

Stepper 프로토콜을 따르는 모든것

뷰컨, 뷰모델, 클래스

Flow
---
어플리케이션의 네비게이션 공간을 규정
기능별로 큼지막하게 나눈다

flow에서 stepper에서 방출한 step에 따라 어떤 navigation을 할지 정해놓는다.

navigation이 일어나기 전에 전처리도 해준다.


ex) loginFlow, setting flow

Presentable
---
보일(present) 수 있는 무언가를 추상화한 것
기본적으로 viewController와 Flow가 Presentable

FlowContributor
---
Presentable 과 Stepper을 인자로 가진 enum 
coordinator에게 다음에는 어떤 presentable과 stepper가 있을지 알려준다

Coordinator
---
stepper에서 step이 발생하면 해당 step에 맞게 뷰컨트로를 띄워주거나 flow 시작한다.

사용후 느낀점
---
1) 네비게이션 흐름을 따라갈라면 뷰컨트롤에서 네비게이션 하는 부분을 일일히 찾아야했다
이제는 step에서 어떤 navigation이 발생할지 enum으로 명시되어있고
Flow안에서 어떤 navigation이 일어나는지 확인 할 있어 코드 가독성이 좋아짐

2) 아직은 아니지만 Flow를 StreetHailing Flow, RideFlow, LoginFlow처럼 기능별로 나누어 앱을 네비게이션 단위로 분리 할 수 있다

3) 기존의 뷰컨트롤에서 네비게이션을 할때보다 뷰컨트롤러 재사용성이 높아짐
각 뷰컨트롤러는 어디로 네비게이션을 할지 몰라도됨

4) Flow에서 의존성주입을 해줄수있다. 의존성 주입이 쉬워짐 

5) 코드가 더 리액티브 해진다
