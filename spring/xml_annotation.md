XML
--------------------------
+ 결합도를 낮추고 유지보수성을 높이기 위해 xml을 사용하였으나 xml이 너무 많아지면 오히려 유지보수성이 떨어지는
문제가 발생할 수도 있다.
+ 시스템 전체에 영향을 주고 변경 가능성이 있는 것은 xml로 설정

annotation
-------------------------------
+ xml과 같은 기능을 하지만 @선언을 통해 메타데이터를 지원한다. 런타임시에 반영되고
xml의 단점을 보완할 수 있다.
+ 시스템 전반에 영향을 주는 것은 xml로 설정하고 이후 설계시 확정되는 부분은 annotation 기반 설정으로 생산성을
높이는 것이 바람직하다.


xml 설정 방법
--------------------------------------------
기본적으로 spring 프로젝트를 생성시 4개의 xml 파일이 존재하게 된다.
 + pom.xml
 + web.xml
 + root-context.xml
 + servlet-content.xml
 ------------------------------------------------
 + web.xml 
     * 서버가 처음 구동될 때 설정 정보가 담겨져 있다. filter나 welecom-file 인코딩 정보, 어떤 root-context,servlet.xml
 파일을 참조할 건지 url-pattern , dispatcherservlet 설정 등의 정보가 있다.
 
 + root-context.xml
     * 뷰를 제외한 공통빈을 설정한다. db나 log 등을 설정한다.
 
 + servlet-context.xml
     * 서블릿에 관련된 설정을 한다. <annotation-driven/> 어노테이션을 사용할 건지
 정적 리소스 매핑 <resource mapping="/resources/**/" location="/resources/">
 viewresolver로 jsp와 name 매핑
 <context:componext-scan base-package=""/> 베이스 패키지 하위의 모든 어노테이션을 스캔해서 빈으로 등록
 하는 등의 설정 정보가 있다.
 
 + pom.xml
     * maven으로 라이브러리를 자동으로 다운받을수 있게 해주는 xml이다. <dependency></dependency>를 통해 필요한 라이브러리와 
 사용 스프링 버전, 자바 등을 설정할 수 있다.
 
 xml bean 설정
 ---------------------------------
 **beans**를 루트 엘리먼트로 사용
 
 ~~~
 <bean>
  id: 빈의 이름을 나타낸다
  class : 빈으로 등록할 클래스를 나타낸다
  <property>
    프로퍼티의 경우 bean 에 주입할 setter를 나타낸다
    name: class에 사용할 setter 이름
    ref : setter에 주입할 bean의 이름
    value : 주입할 인자
  </property>
 </bean>
 ~~~
 
 
 annotation 설정
 ----------------------------------
 
+ @ComponentScan
    - @Component @Service, @Configuration, @Controller, @Repository 이 붙은 클래스 Bean을 찾아서 Context에 등록해주는 annotation
 
+ @EnableAutoConfiguration
    - 스프링 context를 만들때 classpath 내용에 기반해서 자동으로 설정하는 기능(만약 tomcat-embed-core.jar이 있다면 톰캣서버가 셋팅)
 
+ @Required
    - setter에 적용하면 빈 생성시 필수 프로퍼티임을 알린다
 
+ @Resource
    - 이름으로 빈 객체를 주입( @Resource(name="redisTemplate") private ListOperations<String, String> listOps;)
 
+ @Autowired
    - 타입으로 빈 객체를 주입
 
+ @ConfigurationProperties
    - default로 classpath:application.properties파일이 조회된다
 
+ @Value
    - properties에서 값을 가져와 적용할 때 사용 (@Value("${value.from.file}"))
 
+ @SpringBootApplication
    - @Configuration, @EnableAutoConfiguration, @ComponentScan 3가지를 하나로 합친 것
 
+ @RequestMapping
    - 요청 URL을 어떤 메소드가 매핑할것인지 알려주는 annotation
 
+ @CookieValue
    - 쿠키 값을 파라미터로 전달 받을 수 있는 방법 (ex: public String view(@CookieValue(value="auth")String auth))
 
+ @ModelAttribute
    - view에서 전달해주는 파라미터를 클래스의 멤버 변수로 바인딩 해주는 annotation
    
+ @SessionAttribute
    - @SessionAttribute("name")이라고 한다면 Model에 key값이 "name"으로 있는 값은 자동으로 session에 저장된다
    
+ @Transactional
    -  메서드 내부에 있는 트랜잭션을 롤백할 수 있게 해주는 annotation(@Transactional(readOnly=true,rollbackFor=Exception.class), timeout, noRollBackFor)
    
+ @Cacheable
    - 메서드 최초 호출에서는 캐쉬에 저장하고 두번째 호출 부터는 캐쉬의 값으 ㄹ반환 
 
