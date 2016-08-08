# 스프링 프로젝트 시작 환경
[코드로 배우는 스프링 웹 프로젝트](http://book.naver.com/bookdb/book_detail.nhn?bid=9425458)를 보고 작성한 프로젝트 시작 환경이다.

1. 스프링 프로젝트 생성
2. JDK 설정
3. pom.xml 수정
4. root-context.xml 수정
5. mybatis-config.xml 파일 추가
6. 테스트 코드 작성

## 1. 스프링 프로젝트 생성
File -> New -> Spring Legacy Project -> Spring MVC Project

## 2. JDK 설정
프로젝트 우클릭 -> Properties ->
- Project Facets -> Java 버전 변경
- Java Compiler -> JDK 버전 변경

## 3. pom.xml 수정
- 수정

```xml
//스프링 버전 변경
<properties>
		<java-version>1.8</java-version>
		<org.springframework-version>4.1.7.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>

//JUnit 버전 변경
<!-- Test -->
<dependency>
  	<groupId>junit</groupId>
  	<artifactId>junit</artifactId>
  	<version>4.12</version>
  	<scope>test</scope>
</dependency>

//Servlet 버전 변경
<!-- Servlet -->
<dependency>
  	<groupId>javax.servlet</groupId>
  	<artifactId>javax.servlet-api</artifactId>
  	<version>3.1.0</version>
</dependency>
```

- 추가

```xml
//MySQL 연결
<!-- mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.36</version>
</dependency>

//스프링과 MyBatis 연결
<!-- mybatis -->
<dependency>
  	<groupId>org.mybatis</groupId>
  	<artifactId>mybatis</artifactId>
  	<version>3.4.0</version>
</dependency>
<!-- mybatis-spring -->
<dependency>
  	<groupId>org.mybatis</groupId>
  	<artifactId>mybatis-spring</artifactId>
  	<version>1.3.0</version>
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
</dependency>

//JSON 사용
<!-- jackson-databind -->
<dependency>
  	<groupId>com.fasterxml.jackson.core</groupId>
  	<artifactId>jackson-databind</artifactId>
  	<version>2.5.4</version>
</dependency>
```

## 4. root-context.xml 수정
- aop, context, jdbc, mybatis-spring 네임스페이스 추가
- 소스 추가

```xml
<!-- MySQL 연결: database, name, pw 입력 -->
<bean id="dataSource"	class="org.springframework.jdbc.datasource.DriverManagerDataSource">
  	<property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
  	<property name="url" value="jdbc:mysql://localhost:3306/database"></property>
  	<property name="username" value="name"></property>
  	<property name="password" value="pw"></property>
</bean>

<!-- MyBatis 연결 -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  	<property name="dataSource" ref="dataSource"></property>
  	<property name="configLocation" value="classpath:/mybatis-config.xml"></property>
</bean>
```

## 5. mybatis-config.xml 파일 생성
'src/main/resources'에 다음의 코드로 파일 생성
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>

</configuration>

```

## 6. 테스트 코드 작성

- MyBatis의 연결 테스트

```java
package com.jin.review;

import javax.inject.Inject;

import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = { "file:src/main/webapp/WEB-INF/spring/**/*.xml" })
public class MyBatisTest {

	@Inject
	private SqlSessionFactory sqlFactory;

	@Test
	public void testFactory() {
		System.out.println(sqlFactory);
	}

	@Test
	public void testSession() throws Exception {

		try(SqlSession session = sqlFactory.openSession()) {

			System.out.println(session);

		} catch(Exception e) {
			e.printStackTrace();
		}

	}

}
```

- WAS없이 컨트롤러 테스트

```java
package com.jin.review;

import javax.inject.Inject;

import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration(locations = { "file:src/main/webapp/WEB-INF/spring/**/*.xml" })
public class SampleControllerTest {

	private static final Logger logger = LoggerFactory.getLogger(SampleControllerTest.class);

	@Inject
	private WebApplicationContext wac;

	private MockMvc mockMvc;

	@Before
	public void setup() {
		this.mockMvc = MockMvcBuilders.webAppContextSetup(this.wac).build();
		logger.info("setup......");
	}

	@Test
	public void testDoA() throws Exception {
		mockMvc.perform(MockMvcRequestBuilders.get("/"));
	}

}
```
