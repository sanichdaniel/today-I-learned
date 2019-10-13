Obseravble Basic
===
Observable은 이벤트의 시퀀스를 내뿜는다

ObservableType protocol을 따른다.

Observable Type에 의해 Observable은, next, completed, error 3가지를 내뿜을수있다

completed, error이면 이벤트 내뿜는걸 종료한다.

Observable은 Subscriber 가 있어야만 이벤트를 내뿜는다.

Create Observable
===
* create

    Api를 원하는대로 wrap할 수 있다.

    Observable.create() 의 인자는, subscribe하나이다. 여기다가 subscribe가 있을시 어떻게 해야할지 알려준다. 

    An Observer is what you actually pass to subscribe(...)

The syntax subscribe(onNext:onError:onCompleted:) is just syntactic sugar to not have to actually create an Observer object every time.

     subscribe. Its job is to provide the implementation of calling subscribe on the observable. In other words, it defines all the events that will be emitted to subscribers. 

    The subscribe parameter is an escaping closure that takes an AnyObserver and returns a Disposable. AnyObserver is a generic type that facilitates adding values onto an observable sequence, which will then be emitted to subscribers.

* just


* deferred



Traits
===
Observable중 기존의 Observable보다 제한된 특성을 가진것

* Single

    .success(.next & .completed), .error만 내뿜음

* Completable

    .completed, .next만 내뿜음


Subject
===
Subject 는 observable이면서 observer


RX 직접 구현하기

http://minsone.github.io/programming/swift4-implement-own-rx-event-disposable-observer-observable


https://medium.com/@SergDort/learn-rx-by-implementing-observable-e5cb08c9c35

Observable

~~~swift
public protocol ObservableType {
    associatedtype E
    
    func subscribe<O: ObserverType>(observer: O) -> Disposable where O.E == E
}
~~~

Observer을 받고 Disposable을 return한다


~~~swift


public protocol ObserverType {
    associatedtype E
    
    func on(event: Event<E>)
}

public enum Event<T> {
    case next(T)
    case error(Error)
    case completed
}
~~~

Event를 다룬다

~~~swift
public final class Observer<E>: ObserverType {
    private let _handler: (Event<E>) -> Void
    
    public init(handler: @escaping (Event<E>) -> Void) {
        _handler = handler
    }
    
    public func on(event: Event<E>) {
        _handler(event)
    }
}
~~~
Observer은 eventHandler로 initialize되고, newEvent가 만들어지면 initialize 된다
Observer은 이벤트를 받으면 동작할 closure을 가진다

Observable은 Observer을 subscribe함수를 통해 넘길 수 있는 타입이다. 
