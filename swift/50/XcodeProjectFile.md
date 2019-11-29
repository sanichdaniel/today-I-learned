Xcode Project 개념들
===

Project
---
파일, 리소스, 정보들을 들고있는 리포지토리

 .xcodeproj 안에 
 * project.pbxproj 파일
 * xcuserdata 디렉토리
 
 2개의 항목이 존재한다. 

1) project.pbxproj는 실제 프로젝트의 설정을 담은 파일입니다.
2) .xcuserdata: 프로젝트의 개인 설정을 담은 디렉토리. breakpoint, UI layout, 스냅샷 설정등이 있다.

Workspace
---
여러 개의 Project를 담아 관리할 수 있도록 해주는 개념입니다.

Workspace와 Subproject의 차이  
. Workspace를 통해 Project를 관리하면 Project들간의 관계는 형제 관계가 됩니다.

Target
---
Target은 프로젝트를 통해 생성되는 Application을 지칭합니다. 이는 일반적으로 하나의 모듈을 의미합니다. Xcode의 빌드를 통해 생성된 최종 product이다.

즉, Target은 어떻게 프로젝트를 빌드할 것인지를 담당합니다.

Xcode에서 프로젝트에서 최상단 설정 파일을 누르게되면 project 하위에 target 섹션이 있고, 여기서 프로젝트의 target을 관리할 수 있습니다. 기본적으로 Target은 프로젝트 생성시 1개만 생성되지만, 목적에 따라서 하나의 프로젝트에 여러개의 Target을 생성할 수 있습니다.

각각의 target은 프로젝트의 build setting을 설정할 수 있습니다.
각각의 target은 프로젝트에서 포함될 객체, 리소스, 혹은 별도의 스크립트를 따로 설정할 수 있도록 해줍니다.
Xcode에서는 target을 통해서 하나의 프로젝트를 여러 개의 배포판으로 사용할 수 있도록 해줍니다.

Scheme
---
*Scheme은 Target이 프로젝트를 Build, Profile, Test등을 할 때 일어날 일들을 정의할 수 있도록 해주는 항목입니다.*  

일반적으로 Target은 1개 이상의 Scheme을 가지고 있습니다. 이 Scheme에서는 프로젝트 빌드시 사용되는 환경변수나 인자를 넘겨줄 수 있습니다.

Scheme에서 Build Configuration 설정하기
---
Scheme은 앞서 언급한 것처럼 프로젝트의 런타임에서 일어날 일을 설정할 수 있습니다. 이 때 사용되는 대표적인 것 중 하나가 Build Configuration입니다. 기본적으로 Build Configuration은 debug, release가 생성됩니다. 이 Build Configuration은 실제 코드내에서 포함될 코드와 그렇지 않은 코드를 다르게 설정할 수 있도록 도와줍니다.

~~~swift
do {
  // do something
} catch let error {
  #if DEBUG
    debugPrint(error)
  #endif
}
~~~

Scheme에서 Build Configuration을 release로 설정할 경우, debugPrint는 실행되지 않습니다. 이와 같은 것을 가능하게 해주는 것이 Xcode의 PreProcessor입니다.

https://hcn1519.github.io/articles/2018-06/xcodeconfiguration 참고함