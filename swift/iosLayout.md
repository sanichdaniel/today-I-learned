Demystifying iOS Layout
=
http://tech.gc.com/demystifying-ios-layout  의 번역


iOS의 Main run loop
-
main run loop는 유저의 인풋 이벤트( touch, text input)와 이에 맞는 적절한 반응을 처리해줍니다. 모든 유저 상호작용은 event queue안에 들어갑니다. Application 객체는 이벤트 큐에서 이벤트를 받아와서 다른 객체들에게 전달합니다. Application Object는 유저 인풋을 받아서 적절한 handler를 호출하면서 run loop를 실행 시킵니다. 이 handler는 개발자가 작성한 handler입니다. 이 함수들이 리턴되면 다시 main run loop에게 제어권이 돌아가고 update cycle이 시작됩니다. Update cycle은 view를 layout, redraw 하는것을 담당합니다. 

main run loop는 앱의 main thread를 실행한다. 

![weak](/swift/img/mainRunloop.png)

Update Cycle
-
update cycle 은 앱이 이벤트 다루는 코드를 처리하고, main run loop에게 제어권이 돌아올때 시작됩니다. 이떄 layout, display, constraint들을 업데이트 하기 시작합니다. 만약 이벤트 handler를 다루던중 view를 다시 그려야 한다고 요청한다면, 시스템은 view가 redraw가 필요하다고 체크해 놓는다. iOS는 60fps, 1/60초 마다 새로 고침을 합니다. 이것은 유저가 변화를 느끼기에는 매우 짧은 시간이지만, event가 처리되는데 걸리는 시간과 실제로 해당 뷰가 다시 그려지는데는 시간 간격이 생긴다. 따라서 실행 루프 중 원하는 시점에서 뷰가 업데이트 되지 않을 수 있다. 

업데이트 cycle은 아래 사진처럼 run loop에게 제어가 돌아오면 일어난다. 

![weak](/swift/img/updateCycle.png)

Layout
-
뷰의 layout은 화면에서 뷰의 사이즈, 위치를 말한다. 모든 뷰는 frame이 있다. UIView는 시트템에게 view의 layout이 바꼈다고 알려주고, view의 layout이 다시 계산되었을떄 어떤 액션들을 처리할지에 대한 함수들도 주어진다. 

layoutSubviews()
-
이 메소드는 뷰와 그 뷰의 subview들의 위치 및 크기를 조정합니다. 이 메소드는 그 뷰와 모든 subview들의 layoutSubviews 메소드를 실행시키기에 비용이 많이 든다. 시스템은 뷰의 frame를 다시 계산해야할때마다 호출한다. 하지만 절대로 새로 고침을 위해 layoutSubviews를 직접 호출하는 일은 없어야한다. 대신 layoutSubviews 를 호출해주는 layoutSubviews 보다는 비용이 덜드는 함수들이 있다. 

layoutSubviews가 종료되면, 해당  뷰의 뷰컨트롤로의 viewDidLayoutSubviews 함수가 호출된다. layoutSubviews는 뷰의 레이아웃이 업데이트 될때마다 확실히 불리는 함수이다. 따라서 layout과 크기에 대한 로직은 viewDidLayoutSubviews에 배치하면 된다.

Automatic refresh triggers
-
뷰의 layout이 바뀌었다고 자동으로 체크해놓는 이벤트에는 여러가지가 있고, layoutSubviews가 개발자가 수동으로 할 필요없이 호출이된다.  
#
시스템에게 뷰의 layout 바뀌었다고 알리는 것들에는  
* 뷰의 사이즈 변화
* 서브뷰를 추가해줄때
* 유저의 스크롤뷰 스크롤 ( layoutSubviews가 UIScrollView와 이것의 superview가 호출된다)
* 유저의 기기 회전
* 뷰의 constraint 업데이트  

이것들 이외에도 layoutSubviews의 호출을 유도하는 방식들이 있다.

###  setNeedsLayout()

가장 비용이 덜 드는 방식으로 layoutSubviews를 호출하는 방식에는 setNeedsLayout 메소드가 있다. 이 메소드는 시스템에게 뷰의 layout이 다시 계산되어야 한다고 알린다. setNeedsLayout는 바로 리턴된다. 대신 다음 update cycle에서 시스템은 layoutSubviews를 해당 뷰와 서브뷰에 호출해준다. 

### layoutIfNeeded()
layoutIfNeeded를 호출하면 시스템은 뷰가 레이아웃 업데이트가 필요하다면 즉시 layoutSubviews를 호출해준다. 만약 setNeedsLayout을 호출한 직후나, automatic refresh trigger가 일어난 직후 layoutIfNeeded를 호출해준다면, layoutSubviews가 해당 뷰에 호출이될것이다. 하지만 layoutIfNeeded가 호출되더라도 시스템에게 변화가 있다는 액션을 알리지 않으면 호출이된다.  
  
이 메소드는 즉시 레이아웃을 실행한다. 하지만 즉시 뷰를 업데이트 해야할 상황이 아니라면 setNeedsLayout를 호출해줘서, 다음 update cycle에서 모든 뷰의 레이아웃 업데이트를 통합해서 처리하는게 바람직하다. 
  
  layoutIfNeeded는 애니메이션에서  constraint을 바꿔줄때 유용하다

  Display
  -
  뷰의 디스플레이는 뷰와 그 서브 뷰의 크기와 위치를 포함하지 않는 **뷰의 컨텐츠**를 말한다. 색상, 텍스트, 이미지 및 코어 그래픽 드로잉이 들어간다. 

  ### draw(_ :)
  layoutSubview가  뷰의 사이즈와 위치 변화를 다루듯 뷰의 컨텐츠에 대해 다룬다. 하지만 서브뷰까지 다시 그리지는 않는다. layoutSubviews처럼 마찬가지로 절대로 직접 호출하는 일은 없어야한다.

  ### setNeedsDisplay()

  setNeedsLayout과 함수이다. 컨텐츠가 변했다고 체크를 해주고 바로 리턴해버린다. 시스템은 다음 update cycle에서 체크된 뷰에가서 draw를 호출한다.  
  대부분의 경우에는 자동으로 컨텐츠가 바뀌면 뷰를 다시 그리라고 체크해둔다. 
  display에는 layoutIfNeeded에 해당하는 함수는 없다. 

  Constraints
  -
  오토 레이아웃을 실행하는데는 3단계를 거친다. 1 constraint를 업데이트한다. 2.뷰와 서브뷰들의 layout을 계산한다. 3. 디스플레이의 컨텐츠를 필요하면 다시 draw한다.

  ### updateConstraints()
  layoutSubviews나 draw처럼 직접 호출될일은 없어야된다.  
  constraint를 주거나 지우거나, priority를 주거나 뷰 계층에서 뷰를 지우면 내부적으로 체크해놓고 다음 update cycle에서 updateContraints 가 불린다. 당연히 layout, display 처럼 "update constraints" 플래그를 세팅하는 방법이 있다. 

  ### setNeedsUpdateConstraints()
  setNeedLayout처럼 동작

  ### updateContraintsIfNeeded()
오토 레이아웃을 쓰는 뷰들에게 있어 layoutIfNeeded

### invalidateIntrinsicContentSize()
오토 레이아웃을 쓰는 뷰들중에 intrinsicContentSize 프로퍼티를 가지는 뷰들이 있다. 이것은 뷰의 사이즈를 나타낸다. 하지만 이 값이 변했고 다시 계산되어야한다면 이 함수를 직접적으로 호출을 해줘야한다. 

![weak](/swift/img/constraintDisplayLayout.png)