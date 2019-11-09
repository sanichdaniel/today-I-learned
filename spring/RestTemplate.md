RestTemplate
===

 REST API 호출이후 응답을 받을 때까지 기다리는 동기방식이다

 자주 쓰이는 메소드
 ---
 1)  getForObject()  
 - 주어진 URL 주소로 HTTP GET 메서드로 객체로 결과를 반환받는다
 2) getForEntity()
- 또한 ResponseEntity<T> 제네릭 타입에 따라서 응답을 String이나 Object 객체로 받을 수 있습니다. 