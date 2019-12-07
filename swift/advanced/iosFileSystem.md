iOS File System
===

![unowned](/swift/img/iosFileSystem.png)

ios앱의 파일시스템은 앱의 샌드박스 디렉토리에 한정되어있다.

![unowned](/swift/img/iosSandbox.png)

1) Bundle Container  
앱의 번들
2) Data Container  
앱과 유저에 관한 데이터
3) iCloud Container

앱은 자신의 컨테이너 바깥으로 접근하는게 허락되어 있지 않으나 유일한 예외 사항은 연락처나, 음악들을 접근할때이다.

AppName.app
---
write 불가. read only  
읽기 전용, 수정이 필요한 경우 데이터 컨테이너로 옮겨서 작업

Documents
---
유저가 만들어낸 컨텐츠를 저장하는곳.iTunes, iCloud에 의해 백업

Library
---
사용자의 파일을 제외한 파일들이 저장되고 그들의 최상위 디렉토리입. UserDefaults, Preferecnes등

Tmp
---
앱이 실행되는 동안 생성되거나 사용되는 일시적인 파일들을 저장
