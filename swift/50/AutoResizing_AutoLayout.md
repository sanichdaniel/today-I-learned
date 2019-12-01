Auto Resizing & Auto Layout
===

Auto Resizing
---
기존의 애플에서 다이나믹하게 뷰를 레이아웃하던 기법. 예시 Screen Rotation등이 있을떄 subview를 어떻게 다룰지에 대한 몇가지 enum들. 슈퍼뷰의 leading, trailing, top, bottom에 맞추거나 width, height등에 맞추기.
(autoResizingMask)

*단점* : 다른 형제 뷰들과는 어떻게 layout할지에 대한 규칙이 없었다. 

Auto Layout
---

다른 View들 간의 관계를 이용하여 위치와 크기를 정하는 시스템. 뷰를 다시 그려야하는 상황이 오면 layoutSubviews를 호출한다. 