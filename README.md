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


