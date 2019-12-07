Defer
===

Defer은 현재 스코프(함수, loop)를 벗어날때 실행된다.

Defer은 어떻게 scope를 벗어나가든 실행이 되기에 defer에서 생성된 리소스를 닫아주는 경우에 유용

defer 주의점: defer내부에서 return을 할 수는 없다.