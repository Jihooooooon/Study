Junit
============================================
java에서 제공 해주는 테스트 프레임워크, dao,controller,service 등을 다 구현하고 테스트를 진행할 때 에러가 발생시 찾기 힏들다.

따라서 단위 테스트를 하고자 할 때 사용


환경구성
---------------------------
1. Build Path 에서 add Library를 통해 Junit 을 넣는다.(자동으로 들어가 있음)
2. pom.xml 에 다음을 추가
~~~
<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>4.3.20.RELEASE</version>
        </dependency>
~~~

3. src/test/java 에 테스트 코드 작성

~~~
import java.sql.Connection;



import javax.inject.Inject;
import javax.sql.DataSource;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;



@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = { "classpath:spring/dataSource-context.xml" })
public class MysqlConnectionTest {

	private static final Logger logger = LoggerFactory.getLogger(MysqlConnectionTest.class);

	

	@Autowired
	private DataSource ds;

	

	@Test
	public void testConnection() {

		try (Connection con = ds.getConnection()){

			logger.info("\n MySQL 연결 : " + con);

		} catch (Exception e) {

			e.printStackTrace();

		}

	}

}
~~~
참조 : https://devjjo.tistory.com/29?category=752419
------------------------------------------------------------------------------------
테스트 코드 만들고 환경 설정하는 것도 생각보다 시간이 걸린다...
일을 위한 일을 만드는 느낌
