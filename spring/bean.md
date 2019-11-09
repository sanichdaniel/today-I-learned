Bean
===
Bean은 Spring Container 에 의해서 만들어지는 자바 객체이다.

아래 4가지 annotation을 쓰면 자동으로 bean으로 등록된다  
@Container  
@Service  
@Repository Dao(DB의 data에 access하는 트랜잭션 객체)   
@Component  

@Bean은 외부라이브러리 객체를 빈으로 만들고 싶을때, 객체를 반환하는 메소드에 붙여준다. 

Spring DI의 방법들
===

Field Injection 
---
* @Autowired

Bean으로 등록된 객체를 사용하고 싶으면 클래스에 field로 선언하고 @Autowired 키워드 붙여주기

~~~kt
class InboxItemRepositoryTest {
    @Autowired
    lateinit var targetItemRepository: TargetItemRepository
}
~~~
단점

1) 단일 책임의 원칙 위반. 의존성 주입이 쉬워짐
2) 

Setter Injection
---
Setter Method에 @Autowired를 붙여서 DI를 구현하는 방식이다.
권장되지는 않는다

Constructor Injection
---
제일 권장되는 방법

* Component를 변경이 불가능한 immutable 상태로 선언이 가능합니다.
* 특정 DI Container에 의존하지 않으며 쉽게 단위 테스트도 가능하고 필요하다면 다른 DI Container로 전환이 가능합니다.
*  순환 의존성 Constructor Injection에서는 멤버 객체가 순환 의존성을 가질 경우 BeanCurrentlyInCreationException이 발생해서 순환 의존성을 알 수 있게 된다.

 *필수적인 의존성들은 constructor Injection을 통해, 옵셔널인 의존성은 setter method를 통해 하는게 **rule of thumb***