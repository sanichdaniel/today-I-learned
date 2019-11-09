Controller
===

정의: 들어온 Request를 어떻게 처리할지 결정한다

``` java
@Controller
public class ExampleController {
 
    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String hello(ModelMap modelMap){
        return "/example/hello";
    }
     
}
```
Annotation
---
*  **@Controller**  
Controller의 역할을 수행한다고 명시

*  **@RequestMapping**  
Client의 Request를 처리하는 기준점들  
 **Parameter : ModelMap modelMap**  

 * @GetMapping is a composed annotation that acts as a shortcut for @RequestMapping(method = RequestMethod.GET).
 