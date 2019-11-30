Responder Chain
===

앱은 Responder Object를 통해 이벤트를 받고 다룰수있다. Responder Object는 Responder class의 인스턴스로 UIView, UIVC, UIApplication 등이 있다. UIKit은 앱의 적절한 responder object 즉 first Responder에게 이벤트를 전달한다. 만약 해당 responder object가 이벤트를 못다룬다면, responder chain을 따라 이벤트를 다룰 객체를 찾아 거슬러 올라간다. 앱의 구조에 따라 동적으로 생성된다.