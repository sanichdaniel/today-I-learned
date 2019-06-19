Share vs Replay vs ShareReplay
===

Observable을 각각 Subscribe할때마다 다시 operator들이 불린다

~~~swift
let results = query.rx.text
    .flatMapLatest { query in
        networkRequestAPI(query)
    }
results.subscribe(...)   // a network request
results.subscribe(...)   // another network request
~~~


 share(), you’re actually calling share(replay: 0, scope: .whileConnected) 

 replay를 0으로 하는건 -> Publish Subject와 비슷하다.

 replay를 1로 하는건 -> Behavior Subject
 
 replay  2이상은 -> Replay Subject