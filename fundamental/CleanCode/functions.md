Clean Code Functions
===

작게 만들어라!
---

함수를 만드는 가장 중요한 규칙은 **작게** 이다!

**블록과 들여쓰기**
if 문, while문에 들어가는 블록은 한 줄이어야 한다. 이렇게 해야 함수도 작아지고, 블록안에서 호출하는 함수 이름을 적절하게 짓는다면 코드도 이해하기 쉬워진다. 함수가 중첩구조가 생길만큼 커져서는 안된다.

한가지만 해라
---
함수 이름 아래에서 추상화 수준이 하나인 단계만 수행한다면 한가지 작업만 하는것이다.!

함수당 추상화 수준 한 단계만 내려가야한다
---
함수가 ‘한가지’ 작업만 하려면 함수 내 모든 문장의 추상화 수준이 동일해야 된다.
만약 한 함수 내에 추상화 수준이 섞이게 된다면 읽는 사람이 헷갈린다.

* 추상화 수준이 혼재
~~~swift
function doABC() {
  doA()

  if (a > b && c > 0 || d == 0) {
    doBasicB()
    
    if (e < -1){    
      doAnotherB()
    }
  }
  
  doC();  
}
function doA() {
  doBasicA()
  doAnotherA()
}
~~~

* 일관된 추상화 수준
~~~swift
function doABC() {
  doA()
  doB()
}

function doA() {
  doBasicA()
  doAnotherA()
}

function doB() {
  doBasicB()
  doAnotherB()
}
~~~

서술적인 이름을 사용하라
---
이름이 길어도 서술적인 이름이 짧고 어려운 이름보다 좋다

함수인수
---
함수에서 이상적인 인수 개수는 0항이다. 3,4개는 최대한 피하는것이 좋다. 3개가 넘어가면서부터 테스트가 어려워진다. 

부수 효과를 일으키지 말자
---
부수효과는 거짓말이다. 한 가지를 하겠다고 해놓고서 다른 일을 하기에


명령과 조회를 분리하라
---

오류 코드보다 예외를 사용하라
---

Try/Catch 블록 뽑아내기
try/catch 블록은 원래 추하다.

**try/catch블록을 별도 함수로 뽑아내자.**

오류 처리도 한가지 작업에 속한다.