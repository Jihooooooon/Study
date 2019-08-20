DB, Mybatis 연동하기
==========================================
개발 환경은

~~~
<java-version>1.8</java-version>
<org.springframework-version>5.1.4.RELEASE</org.springframework-version>
<org.aspectj-version>1.9.2</org.aspectj-version>
<org.slf4j-version>1.7.25</org.slf4j-version>
~~~
으로 셋팅

pom.xml
~~~
<!-- mysql -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.13</version>
</dependency>

<!-- mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.6</version>
</dependency>


<!-- mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.2</version>
</dependency>

<!-- spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>${org.springframework-version}</version>
</dependency>


<!-- spring-test -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>${org.springframework-version}</version>
    <scope>test</scope>
</dependency>
~~~

src/main/resources 폴더의 spring 폴더에 db설정을 위한 dataSource-context.xml 파일을 만들고 다음과 같이 작성한다
~~~
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"

	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xmlns:mybatis-spring="http://mybatis.org/schema/mybatis-spring"

	xsi:schemaLocation="

http://mybatis.org/schema/mybatis-spring 

http://mybatis.org/schema/mybatis-spring.xsd

http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">




	<!--dataSource 빈 설정 -->
     
	<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">

		<!-- <property name="driverClassName" value="com.mysql.cj.jdbc.Driver" 
			/> <property name="url" value="jdbc:mysql://localhost:3306/mess?useSSL=false&amp;serverTimezone=Asia/Seoul" 
			/> -->

		<property name="driverClassName"
			value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy" />

		<property name="url"
			value="jdbc:log4jdbc:mysql://localhost:3306/mess?allowPublicKeyRetrieval=true&amp;useSSL=false&amp;serverTimezone=UTC" />


		<property name="username" value="root"></property>

		<property name="password" value="1q2w3e4r"></property>

	</bean>



	<!-- SqlSessionFactory 객체 설정 mappers폴더의 sql문 매핑 -->

	<bean id="SqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">

		<property name="dataSource" ref="dataSource" />

		<property name="mapperLocations"
			value="classpath:/mappers/**/*Mapper.xml" />

	</bean>



	<!-- SqlSession Template 설정 -->

	<bean id="sqlSession"
		class="org.mybatis.spring.SqlSessionTemplate"
		destroy-method="clearCache">

		<constructor-arg name="sqlSessionFactory"
			ref="SqlSessionFactory" />

	</bean>


</beans>

~~~

mappers 폴더 안에 mybatis로 사용할 sql문을 작성하고 Dao,Controller, Service를 구현하면 Mybatis 까지 사용 완료!
