Behavior Relay
===

Behavior Relay 는 Behavior Subject의 wrapper이다.
Variable을 대체하는 애이다

Behavior Subject
---
**Behavior Subject**는 subject의 타입중 하나이다. 

Behavior Subject는 
1) initial value를 가지고 있어야한다.
2) next를 받기 전에도, subscription이 시작되었다면 value를 return해야한다


~~~swift
// Behavior Subject
// a is an initial value. if there is a subscription 
// after this, it would get "a" value immediately
let bSubject = new BehaviorSubject("a"); 

bSubject.next("b");
bSubject.subscribe(value => {
  console.log("Subscription got", value); // Subscription got b, 
// ^ This would not happen 
// for a generic observable 
// or generic subject by default
});

bSubject.next("c"); // Subscription got c
bSubject.next("d"); // Subscription got d
~~~

Single
---
정확히 하나의 요소 또는 error을 방출한다.
부수작용을 공유하지 않는다.

응답, 오류만 반환할 수 있는 HTTP요청을 수행하는데 사용된다


Driver
---
UI레이어에 reactive코드를 작성하거나, 애플리케이션에서 데이터 스트림을 모델링하는 경우를 위한것

1) 오류가 없다
2) observe는 Main Schedular에서 발생
3) 부수작용을 공유(shareReplayLatestWhileConnected)

~~~swift
let results = query.rx.text
    .throttle(0.3, scheduler: MainScheduler.instance)
    .flatMapLatest { query in
        fetchAutoCompleteItems(query)
    }

results
    .map { "\($0.count)" }
    .bind(to: resultCount.rx.text)
    .disposed(by: disposeBag)

results
    .bind(to: resultsTableView.rx.items(cellIdentifier: "Cell")) { (_, result, cell) in
        cell.textLabel?.text = "\(result)"
    }
    .disposed(by: disposeBag)
~~~

* 여기서 문제는 **fetchAutoCompleteItems**가 error을 방출하면, 모든 바인딩이 해제되고 더이상 UI가 새로운 쿼리에 응답하질 않는다. 

 * **fetchAutoCompleteItems**가 background thread에서 결과를 반환하면 백그라운드 스레드의 UI요소에 바인딩이 된다.

 * Result는 2개의 UI요소에 바인딩되어서 2개의 HTTP요청이 날라간다 

~~~swift
fetchAutoCompleteItems(query)
            .observeOn(MainScheduler.instance)  // results are returned on MainScheduler
            .catchErrorJustReturn([])           // in the worst case, errors are handled
    }
    .shareReplay(1)                             // HTTP requests are shared and results replayed
                                                // to all UI elements

~~~

Relay
---
**Relay** class는 error, completed으로 terminate하지 않는다.

Relay로 event를 보낼려면
accept 메소드를 쓰거나
~~~swift
someRelay.accept(someEvent)
~~~

Driver 로부터 BehaviorRelay를 바인딩해주는 방법 2가지가 있다.

Domain과 Network Layer에서는, Observable 들을 쓰는게 나을 수 도 있다.
하지만 UILayer에서는 RxCocoa의 Trait인 **Driver, Signal, Relay**를 쓰는게 유용하다.
---