Bean
===



@Autowired
---
Bean으로 등록된 객체를 사용하고 싶으면 클래스에 field로 선언하고 @Autowired 키워드 붙여주기

~~~
class InboxItemRepositoryTest {
    @Autowired
    lateinit var targetItemRepository: TargetItemRepository
}
~~~
