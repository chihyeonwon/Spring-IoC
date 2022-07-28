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
