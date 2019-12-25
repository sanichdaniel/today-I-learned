Scene Delegate
===

> Xcode 11이 되면서 ios 프로젝트를 처음 만들면 **scene delegate**라는것이 새로 생겼다. iPadOS에서 multi window를 지원하며 나온 결과이다. 기존의 **app delegate**와 차이에 중점을 두어 알아보자

App Delegate
---
ios 12 까지는 app delegate는 앱의 시작점이었다. 
* root ViewController을 셋업 하고
* 앱 세팅 (로깅, 클라우드 서비스)
* 앱의 life cycle에 변화가 있을떄 대응

Scene Delegate
---
ios 13에서 등장한 Scene Delegate가 기존의 app delegate의 역할을 가져가게 된다. window 개념은 scene개념으로 대체된다. 앱은 1개 이상의 scene을 가질수 있다. 

Scene Delegate Class
---
scene delegate의 가장 중요한 함수는 scene(_:willConnectTo:options:) 인데 ios12에서 application(_:didFinishLaunchingWithOptions:)의 함수와 유사하다. 이 함수는 앱에 scene이 추가되는 순간 호출된다. 기존의 root ViewController 세팅하던 부분을 이제 여기서 해주면 된다. 
