Tail Call & Tail Recursion
===

재귀로 짜면 함수 호출 횟수가 많아져 Stack 깊이가 깊어진다

함수 실행 후 돌아갈 원래 자리를 Stack에 저장한다고 했는데, 원래 자리로 돌아가야만 하는 이유가 뭘까?

**원래 자리로 돌아가야만 하는 이유는 원래 자리에서 해야할 일이 남아있기 때문이다.**

~~~swift
func fibonacci(n) {
    if (n < 2)
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
}
~~~

return fibonacci(n - 1) + fibonacci(n - 2)을 보면 fibonacci(n - 1)를 호출한 후에 바로 리턴하는 것이 아니라 다시 한 번 fibonacci(n - 2)를 실행해서 두 값을 더한 후에 리턴한다. 다시 말해, **원래 자리로 돌아와서 해야할 일이 남아있으므로 돌아올 원래 자리의 정보를 Stack에 추가해서 저장해야 한다.**

그렇다면 원래 자리에서 해야할 일을 남겨두지 않는 방법은 무엇인가?

그 방법이 바로 **Tail Call**이다.

> Tail Call은 함수를 호출해서 값을 반환 받은 후 아무 일도 하지 않고 바로 반환하게 하기 위해 논리적으로 가장 마지막(꼬리) 위치에서 함수를 호출하는 방식을 말한다.

Tail Recursion
---

> Tail Call의 특별한 경우로서 Tail Call로 호출하는 함수가 자기 자신인 경우

* 반복이나 꼬리 호출 단계별 계산 결과를 어딘가에 계속 저장한다.

Tail Call Optimization
---

Tail Call 방식으로 짜여지면 Stack을 새로 만들지 않고 이미 있는 Stack 속의 값만 대체해서 Stack을 재사용하는 방식으로 동작하도록 최적화 할 수 있다. 이러한 최적화를 Tail Call Optimization(또는 Tail Call Elimination)이라고 하며 **언어의 실행 환경에서 지원해줘야 한다.**

Tail Recursion 예시
~~~swift
func fibonacciTailRecursion(n, previousFibo, previousPreviousFibo) {
    if (n < 2)
        return n * previousFibo;
    return fibonacciTailRecursion(n - 1,
                                  previousFibo + previousPreviousFibo,
                                  previousFibo);
}

fibonacciTailRecursion(6, 1, 0)
   fibonacciTailRecursion(5, 1, 1)
     fibonacciTailRecursion(4, 2, 1)
       fibonacciTailRecursion(3, 3, 2)
        fibonacciTailRecursion(2, 5, 3)
          fibonacciTailRecursion(1, 8, 5)
          return 8
        return 8
      return 8
    return 8
  return 8
return 8
~~~