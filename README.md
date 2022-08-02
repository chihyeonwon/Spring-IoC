# Spring-IoC
템플릿 프로젝트의 파일들을 직접 만들어서 테스트

## 웹 프로젝트 생성

File -> New -> eGovFrame Web Project로 웹 프로젝트를 생성한다.

## 빈 클래스 생성

스프링 컨테이너가 생성하고 관리할 비즈니스 클래스를 작성한다.   
src/main/java 소스 폴더에서 오른쪽 마우스 클릭후 New -> Class 메뉴를 선택해 자바 클래스를 작성한다.   
패키지이름 : egovframework.sample.service.impl 클래스 이름 SampleServiceImpl   
SampleServiceImpl.java
```java
package egovframework.sample.service.impl;

public class SampleServiceImpl {
	
	public SampleServiceImpl() throws Exception {
		System.out.println("===> SampleServiceImpl 생성");
	}
	
	public void insertSample() throws Exception {
		System.out.println("SampleService---Sample 등록");
	}
	
	public void updateSample() throws Exception {
		System.out.println("SampleService---Sample 수정");
	}
	
	public void deleteSample() throws Exception {
		System.out.println("SampleService---Sample 삭제");
	}
	
	public void selectSample() throws Exception {
		System.out.println("SampleService---Sample 상세 조회");
	}
	
	public void selectSampleList() throws Exception {
		System.out.println("SampleService---Sample 목록 검색");
	}
}
```

작성된 SampleServiceImpl은 비즈니스 컴포넌트를 구성하는 요소 중 가장 중요한 클래스이며, 클라이언트가 사용할 비즈니스 메소드들을 가지고 있다.   
하지만 비즈니스 로직을 본격적으로 작성하지는 않았고 단지 이 메소드가 호출되었음을 확인할 수 있도록 간단한 메시지를 콘솔에 출력하도록 했다.   
그리고 이후에 비즈니스 로직이 추가되었을 때 발생할 수 있는 모든 예외를 나중에 처리하기 위해서 throws Exception을 추가했다.   

## 스프링 설정 파일 작성

대부분의 컨테이너는 컨테이너가 구동될 때 XML 설정 파일을 읽어들인다.   
읽어들인 XML 파일로부터 자신이 생성하고 관리할 객체들의 정보를 확인한다.   
스프링 컨테이너도 다른 컨테이너와 같이 XML 설정 파일이 필요한데 이때 표준프레임워크에 내장된 STS(Spring Tool Suite)를 이용하면 간단하게 설정 파일을 생성하고 편집할 수 있다.   
src/main/resources 소스 폴더를 선택하고 오른쪽 마우스 클릭 후 New -> folder 메뉴를 선택하여 egovframework 폴더와 그 밑에 spring 폴더를 연속해서 만든다.   
spring 폴더를 선택하고 오른쪽 마우스 클릭 후 New -> Spring Bean Configuration File 메뉴를 선택한다.   
![image](https://user-images.githubusercontent.com/58906858/181417192-df1bfcec-a504-47b0-962c-1d95f1e3dc3c.png)
이렇게 생성된 XML 파일은 기본 에디터로 실행되는 데 이를 스프링 전용 에디터로 변경해야한다.   
context-common.xml 파일을 선택하고 오른쪽 마우스 클릭 후 Open With -> Spring Config Editor 메뉴를 선택하여 오픈한다.   
![image](https://user-images.githubusercontent.com/58906858/181418098-a829e3ca-6466-40b4-8647-1b53218bacd8.png)

<bean> 설정에서 다음과 같이 스프링 설정을 추가한다. class 속성값에 패키지 경로가 포함된 경로를 지정해준다. 

## 스프링 컨테이너 구동 및 테스트

스프링 설정 파일을 작성한 후에 SampleServiceImpl 객체를 테스트하는 클라이언트를 만들어야한다.   
src/test/java 소스 폴더에 SampleServiceClient.java 클래스 파일을 생성한다.      
![image](https://user-images.githubusercontent.com/58906858/182079098-6ce1a326-deab-42e8-872b-ee1b874b11dc.png)

SampleServiceClient.java
```java
package egovframework.example.sample.service;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class SampleServiceClient {
	public static void main(String[] args) throws Exception {
		// 1. Spring 컨테이너를 구동한다.
		AbstractApplicationContext container = new GenericXmlApplicationContext(
				"egovframework/spring/context-common.xml");
				
	}
}
```

이 자바 클라이언트가 가장 먼저 하는 일은 GenericXmlApplicationContext 객체(스프링 컨테이너)를 생성하는 것이다. 컨테이너가 생성될 때 스프링설정파일을 로딩할 수 있도록 생성자 인자로 넘겨주면 스프링 컨테이너를 구동할 수 있다.   
클라이언트 프로그램을 저장하고 Ctrl + F11를 이용해서 자바 프로그램을 실행한다.   
![image](https://user-images.githubusercontent.com/58906858/182079894-bc4f0ab7-8b17-4df0-86ef-0b46c4f42f50.png)
실행결과를 보면 log4j2 관련 설정 파일이 없어서 문제가 발생하는데, log4j2는 스프링과 상관없으며 스프링 컨테이너가 출력하는 다양한 로그를 관리하기 위해 사용한다.

## 로그 출력하기

스프링 컨테이너가 제공하는 로그를 콘솔에 출력하기 위해서는 log4j2.xml 파일을 작성해야 한다.   
src/main/resources 소스 폴더에서 오른쪽 마우스 클릭 후 New -> Other -> XML File을 선택한다.   
![image](https://user-images.githubusercontent.com/58906858/182083030-eacb7822-0779-45c1-86a7-0a9e9433d44b.png)

생성된 log4j2.xml 파일에 다음과 같은 내용을 입력한다.   
```java
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
    <Appenders>
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d %5p [%c] %m%n" />
        </Console>
    </Appenders>
    <Loggers>
        <Logger name="java.sql" level="INFO" additivity="false">
            <AppenderRef ref="console" />
        </Logger>
        <Logger name="egovframework" level="DEBUG" additivity="false">
            <AppenderRef ref="console" />
        </Logger>
        <Logger name="org.springframework" level="INFO" additivity="false">
            <AppenderRef ref="console" />
        </Logger>
        <Root level="INFO">
            <AppenderRef ref="console" />
        </Root>
    </Loggers>
</Configuration>
```

로그 설정에서 중요한 것은 <Appender>와 <Logger> 두 가지이다.   
<Appender>는 어디에 어떤 패턴으로 로그를 출력할지 결정해준다.   
로그 메시지는 크게 콘솔, 파일, 데이터베이스에 출력할 수 있는데 Console 엘리먼트를 사용했기 때문에 콘솔에 로그 메시지를 출력한다.
콘솔은 PatternLayout을 사용하여 로그의 패턴도 지정할 수 있다.   
<Logger>는 메시지를 <Appender>로 전달하여 실질적으로 <Appender>가 로그를 출력하도록 한다.   
<Logger>의 로그 레벨은 5가지 (DEBUG, INFO, WARN, ERROR, FATAL)로 지정할 수 있다. 만약 WARN으로 설정하면 그 위 이상의 단계 WARN, ERROR, FATAL 로그가 모두 출력된다.   
보통 개발단계에서 DEBUG, INFO로 설정하지만 운영 단계에서 WARN, ERROR로 설정한다.   
로그 설정을 저장하고 클라이언트 프로그램인 SampleServiceClient 를 다시 실행하면 다음과 같은 로그 관련 메시지가 콘솔창에 뜨게 된다.   
```java
2022-08-01 15:16:56,884  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from class path resource [egovframework/spring/context-common.xml]
2022-08-01 15:16:56,972  INFO [org.springframework.context.support.GenericXmlApplicationContext] Refreshing org.springframework.context.support.GenericXmlApplicationContext@77e4c80f: startup date [Mon Aug 01 15:16:56 KST 2022]; root of context hierarchy
===> SampleServiceImpl 생성
```
실행결과를 보면 환경 설정 파일인 context-common.xml을 로딩하여 스프링 컨테이너 중 하나인 GenericXmlApplicationContext를 생성하고 있다. 컨테이너를 구동(생성)되면서 context-common.xml 파일에 등록한 SampleService 클래스의 객체가 메모리에 올라갔다는 것인데, 이렇게 컨테이너가 구동(생성)되면서 객체를 메모리에 생성하는 것을 Pre-Loading이라고 한다.   
반대로 클라이언트의 요청에 의해서 해당 객체만 메모리에 생성하는 것을 Lazy-Loading이라고 하는데 기본적으로 GenericXmlApplicationContext는 Pre-Loading으로 작동한다.   
   
스프링 컨테이너가 정상적으로 구동됐으면 컨테이너로부터 SampleServiceImpl 객체를 검색(Lookup)하여 비즈니스 메소드를 호출해본다.
SampleServiceClient.java
```java
package egovframework.example.sample.service;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

import egovframework.sample.service.impl.SampleServiceImpl;

public class SampleServiceClient {
	public static void main(String[] args) throws Exception {
		// 1. Spring 컨테이너를 구동한다.
		AbstractApplicationContext container = new GenericXmlApplicationContext(
				"egovframework/spring/context-common.xml");
		
		// 2. Spring 컨테이너로부터 SampleServiceImpl 객체를 Lookup한다.
		SampleServiceImpl sampleService = (SampleServiceImpl) container.getBean("sampleService");
		sampleService.insertSample();
		sampleService.selectSampleList();
		
		// 3. Spring 컨테이너를 종료한다.
		container.close();
	}
}
```

추가한 소스 중 첫번째는 아이디가 sampleService인 객체를 getBean() 메소드를 통해 검색하는 것이다. 검색된 객체를 원하는 타입으로 형변환한후 검색한 객체의 메소드를 호출할 수 있다.   
두 번째로 추가한 소스는 컨테이너를 종료하는 것이다. 이때 컨테이너의 close()메소드를 호출하여 컨테이너를 종료하는데, 컨테이너는 종료되기 직전에 자신이 생성해서 관리했던 모든 객체들을 메모리에서 삭제한다.   
   
이제 수정된 클라이언트를 저장하고 다시 실행보면 다음과 같이 SampleServiceImpl 객체의 insertSample()과 selectSampleList()메소드가 실행되는 것을 확인할 수 있다.
```java
2022-08-01 15:37:43,356  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from class path resource [egovframework/spring/context-common.xml]
2022-08-01 15:37:43,447  INFO [org.springframework.context.support.GenericXmlApplicationContext] Refreshing org.springframework.context.support.GenericXmlApplicationContext@77e4c80f: startup date [Mon Aug 01 15:37:43 KST 2022]; root of context hierarchy
===> SampleServiceImpl 생성
SampleService---Sample 등록
SampleService---Sample 목록 검색
2022-08-01 15:37:43,508  INFO [org.springframework.context.support.GenericXmlApplicationContext] Closing org.springframework.context.support.GenericXmlApplicationContext@77e4c80f: startup date [Mon Aug 01 15:37:43 KST 2022]; root of context hierarchy
```

지금까지의 실행과정은 다음과 같다.   
1. 스프링 설정 파일(context-common.xml)을 로딩하여 컨테이너를 구동한다.
2. 스프링 컨테이너는 <bean> 등록된 SampleServiceImpl 객체를 생성(Pre-Loading)한다.
3. 클라이언트가 getBean() 메소드로 아이디가 sampleService인 객체를 검색한다.
4. 컨테이너는 SampleServiceImpl 객체를 검색하여 리턴한다.

## 스프링 설정 파일

스프링 설정파일은 스프링 컨테이너의 동작에 영향을 미치는 매우 중요한 파일이며, 이 XML 설정을 통해 다양한 요청을 컨테이너에게 지시할 수 있다.   
STS를 이용해서 만든 스프링 설정 파일에는 beans 네임스페이스가 기본 네임스페이스로 선언되어있으며 bean, description, alias, import 등 네 개의 엘리먼트를 자식으로 사용할 수 있는데 이 중에서 bean 엘리먼트만 정확하게 이해하면 되며 나머지는 사용할 일이 거의 없음으로 무시해도 된다.   

## <bean> 엘리먼트 속성

bean 엘리먼트는 id와 class 속성 외에도 여러 속성을 사용할 수 있지만 일반적으로 많이 사용하는 몇 가지 속성을 확인해본다.

1. init-method 속성

스프링 컨테이너는 스프링 설정 파일에 등록된 클래스의 객체를 생성할 때 기본적으로 디폴트 생성자를 호출한다.   
SampleServiceImpl 클래스에 멤버변수와 멤버변수를 초기화할 메소드를 추가한다.   

SampleServiceImpl 
```java
package egovframework.sample.service.impl;

public class SampleServiceImpl {
	private String name;
	
	public SampleServiceImpl() throws Exception {
		System.out.println("===> SampleServiceImpl 생성");
	}
	
	public void initMethod() {
		System.out.println("---> initMethod() 호출");
		name = "샘플 서비스 객체";
	}
	
	public void insertSample() throws Exception {
		System.out.println(name + "---Sample 등록");
	}
	
	public void updateSample() throws Exception {
		System.out.println("SampleService---Sample 수정");
	}
	
	public void deleteSample() throws Exception {
		System.out.println("SampleService---Sample 삭제");
	}
	
	public void selectSample() throws Exception {
		System.out.println("SampleService---Sample 상세 조회");
	}
	
	public void selectSampleList() throws Exception {
		System.out.println(name + "---Sample 목록 검색");
	}
}
```

이제 스프링 설정 파일에 init-method 속성을 추가한다.   
context-common.xml
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<bean id="sampleService"
	class="egovframework.sample.service.impl.SampleServiceImpl"
	init-method="initMethod"></bean>

</beans>
```

앞서 작성한 SampleServiceClient 프로그램을 다시 실행하면 다음과 같은 결과 화면을 볼 수 있다.   
![image](https://user-images.githubusercontent.com/58906858/182286225-4c6ce311-3dce-47a6-903b-f2fc169ffd73.png)

2. destroy-method 속성

init-method를 객체의 초기화를 위해 사용한다면 destroy-method는 객체가 삭제되기 전에 수행될 작업을 처리하기 위해 사용한다.   
destroy-method 속성을 테스트하기 위해서 SampleServiceImpl 클래스에 destroyMethod()메소드를 추가한다.   

SampleServiceImpl
```java
package egovframework.sample.service.impl;

public class SampleServiceImpl {
	private String name;
	
	public SampleServiceImpl() throws Exception {
		System.out.println("===> SampleServiceImpl 생성");
	}
	
	public void initMethod() {
		System.out.println("---> initMethod() 호출");
		name = "샘플 서비스 객체";
	}
	
	public void destroyMethod() {
		System.out.println("---> destroyMethod() 호출");
		name = null;
	}
	
	public void insertSample() throws Exception {
		System.out.println(name + "---Sample 등록");
	}
	
	public void updateSample() throws Exception {
		System.out.println("SampleService---Sample 수정");
	}
	
	public void deleteSample() throws Exception {
		System.out.println("SampleService---Sample 삭제");
	}
	
	public void selectSample() throws Exception {
		System.out.println("SampleService---Sample 상세 조회");
	}
	
	public void selectSampleList() throws Exception {
		System.out.println(name + "---Sample 목록 검색");
	}
}
```

스프링 설정 파일에 destroy-method 속성을 추가한다.   

context-common.xml
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<bean id="sampleService"
	class="egovframework.sample.service.impl.SampleServiceImpl"
	init-method="initMethod" destroy-method="destroyMethod"></bean>

</beans>
```

SampleServiceClient 프로그램을 다시 실행해서 실행결과를 확인해본다.   
![image](https://user-images.githubusercontent.com/58906858/182286983-8f6f0d73-437f-45f1-b69d-e557d3e304f2.png)

스프링 컨테이너는 close() 메소드를 통해 종료할 수 있는데, 컨테이너가 종료되기 직전에 컨테이너는 자신이 관리하는 모든 객체를 삭제한다.   
이때 삭제되는 객체의 destroyMethod() 메소드가 호출되는 것이다.

