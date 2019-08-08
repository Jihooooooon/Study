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
 
 > web.xml
 
 서버가 처음 구동될 때 설정 정보가 담겨져 있다. filter나 welecom-file 인코딩 정보, 어떤 root-context,servlet.xml
 파일을 참조할 건지 url-pattern , dispatcherservlet 설정 등의 정보가 있다.
 
 >root-context.xml
 뷰를 제외한 공통빈을 설정한다. db나 log 등을 설정한다.
 
 >servlet-context.xml
 서블릿에 관련된 설정을 한다. <annotation-driven/> 어노테이션을 사용할 건지
 정적 리소스 매핑 <resource mapping="/resources/**/" location="/resources/">
 viewresolver로 jsp와 name 매핑
 <context:componext-scan base-package=""/> 베이스 패키지 하위의 모든 어노테이션을 스캔해서 빈으로 등록
 하는 등의 설정 정보가 있다.
 
 >pom.xml
 maven으로 라이브러리를 자동으로 다운받을수 있게 해주는 xml이다. <dependency></dependency>를 통해 필요한 라이브러리와 
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
 
