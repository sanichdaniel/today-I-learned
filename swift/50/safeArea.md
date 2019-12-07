Safe Area
===

SafeArea는 다른 컨텐츠에 가려지지 않는 영역의 view이다. (status bar, navigation bar, toolbar, tab bar 등) top,bottom layoutguide와는 달리 뷰에게도 적용 가능


만약 Navigation Bar을 앱에다가 더하면 safeArea가 줄어든다.

portrait 모드일떄는 위아래로 inset가 생기고, landscape모드일때는 아래와 좌우로 생긴다. 
![weak](/swift/img/safeArea.png)

![weak](/swift/img/viewSafeArea.png)

Safe Area
---
UIView의 프로퍼티

TopLayoutGuide, BottomLayoutGuide
---
UIViewController 의 프로퍼티