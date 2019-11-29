Library
===
1. CocoaPod
2. Carthage
3. Swift Package Manager

Cocoapod
---
루비로 만들어진 외부 라이브러리 종속성 관리 툴.

코코아 팟으로 사용하는 외부 라이브러리도 함께 빌드하기 때문에 .workspace 파일로 오픈해야한다.

* pod install  
Podfile에 적힌대로 라이브러리를 설치시켜준다

* pod update -dependency  
Podfile에 적힌대로 종속성을 올려준다. 

* pod repo update
로컬에 있는 spec-repo를 업데이트 시켜준다.
podspec은 podlibrary의 버젼 정보를 담고있다. 
pod repo update를 하면 가장 최신의 podspec을 받아온다.

장점
1. 제공하는 라이브러리가 많다

단점
1. clean 했을시, 외부라이브러리들을 다시 빌드하기에 빌드시간이 오래걸림.

Carthage
---


장점
1. 매번 빌드를 하는것이 아니고 미리 빌드하여 둔다
2. 워크스페이스를 따로 생성할 필요가 없습니다.
3. cocoapod보다 빌드시간이 빠르다.

단점
1. cocoapod에 비해 지원하는 라이브러리가 적다
2. 직접 설정해주어야 할것이 많다.

Swift Package Manager
---
swift의 공식 의존성 관리 툴