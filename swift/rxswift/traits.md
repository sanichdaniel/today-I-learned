RxSwift Trait
===

Single
---
항상 단일 요소 또는 오류를 방출하도록 보장합니다.

Maybe
---

하나의 이벤트가 발생하거나, 이벤트 없이 종료하거나, 에러가 발생하거나 3중 하나만 방출하고 종료된다. 

사용되는곳
-  캐시에서 데이터를 가져올때 데이터가 있을때는 onSuccess, 아니면 complete 시키기.

Completable
---

complete하거나 error방출

사용되는곳: 

- 작업이 끝났을때, 작업의 결과는 안궁금할때
- 캐시를 업데이트를 할때
- 이미지를 업로드해서 성공적으로 업로드했는지 안했는지만 궁금할때

RxCocoa Trait
===

Driver
---

Control Property
---

Control Event
---