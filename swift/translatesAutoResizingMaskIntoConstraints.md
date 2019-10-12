translatesAutoResizingMaskIntoConstraints
===

Auto Layout 개념을 잠깐 짚고 넘어가자
Auto Layout: 뷰들간의 관계로 뷰의 위치와 크기를 자동으로 결정하는 시스템, 관계는 constraint로 준다

translatesAutoResizingMaskIntoConstraints: 
정의: view의 autoResizingMask가 auto layout constraints로 변환 되는지 여부를 결정한다

코드로 constraint를 줄때 호출한다

autoResizingMask: 슈퍼뷰의 bound가 변했을때 어떻게 자동으로 사이즈를 조절할지에 대한 옵션

translatesAutoresizingMaskIntoContraints값이 true이면
view의 frame, bounds 등을 이용해 정적인 프레임 기반 레이아웃 만들수있다
Auto resizing mask constraint는 뷰의 위치를 완전히 지정한다
이 이후 추가적인 constraint를 만들수없다!

InterfaceBuilder( 스토리보드 ) 에서 view를 추가하면 시스템은  false로 설정
여기서 추가적으로 코드로 constraint주고 싶다면 false로 세팅해주자

