앱의 생명주기
===
5개의 상태가 있다
* Not Running
* In Active
* Active
* Background
* Suspended 

![weak](/swift/img/appLifeCycle.png)

* Not Running: 앱이 아직 시작도 안되고, 앱을 종료한 상태
* In Active: 앱이 foreground에 있지만, 이벤트를 받고있지 않는 상태다. 전화나 문자 왔을때또는 앱 state가 변하고 있을떄. 앱 UI 상호작용은 안됨.
* Active: In Active 상태를 거쳐야 올 수 있고, UI상호작용이 된다.
* Background: 백그라운드에 있고 코드가 실행되는 상태. 앱을 처음 킬때는  In-Active → Active. suspend된 상태였으면, background 갔다가 In-Active -> Active.
* Suspended: 백그라운드에 있고, 코드가 실행되지 않는 상태. 메모리 부족시 앱 강제 종료된다.


* willFinishLaunchingWithOptions : 앱을 처음 켰을떄
* didFinishLaunchingWithOptions: 앱 window 보이기 직전에
* applicationDidBecomeActive : inactive -> active
* applicationWillResignActive: active -> inactive 으로 문자나 전화왔을 경우 등이 있다.
* applicationDidEnterBackground: 백그라운드 들어가기전에 5초 정도 함수들을 실행할 시간이 주어진다.
* applicationWillTerminate: 앱을 종료시키기전에 5초 정도의 시간이 주어진다. 