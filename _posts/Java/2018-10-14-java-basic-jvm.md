---
layout: post
title:  "기초 : 자바 프로그램 실행과정, JVM"
date:   2018-10-14
author: EunHye Jung
categories: java
comment : true
tags:	java, 자바, JVM, 자바가상머신
cover:  "/assets/instacode.png"
---   
  
  
##  <font color = "#0E4D92"> 자바 프로그램 실행과정 </font>  
  
* <b>JRE</b>는 자바 API와 JVM으로 구성되며, <b>JVM</b>의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 들여서 자바 API와 함께 실행하는 것임.
  
  
  ![content01](/assets/contents/java/content01_jvm.PNG)     
   
   
* 자바 프로그램을 컴파일하면, JVM은 클래스 로더를 이용해서 컴파일된 바이트 코드를 메모리로 읽어들인다.  
  클래스로더에 의해 바이트코드가 <b>런타임 데이터 영역(Runtime Data Area)</b>에 올라가게 되면   
  실행 엔진(Execution Engine)이 바이트코드를 한줄씩 실행시킨다.  
* JVM의 메모리 구조는 활용 용도에 따라 여러 영역으로 구분되어 있는데, 메소드, 스택, 힙 영역이 프로그래밍과 밀접환 관련이 있다.  
   
   
- - - 
  
  
##  <font color = "#0E4D92"> JVM 메모리 구조 </font>  
  
### <font color="#04635b"> 메소드 영역 (Method Area) </font>  
* 런타임시 생성된 모든 스레드가 공유하는 영역
* JVM이 기본적으로 할당받는 메소드 영역의 메모리 사이즈는 일정하게 정해져 있다.  
  (이 범위를 벗어나게 되면 OutOfMemory 에러가 발생)  
   
### <font color="#04635b"> 스택 영역(Stack Area) </font>  
* 스택 영역에는 메소드 정보, 지역변수 정보, 파라미터 값 등이 저장됨.  
* 메소드가 호출되면 슽개 프레임이라는 자료구조가 생성되고, 실행 순서에 따라 스택 동작을 수행하다가, 모든 동작이 완료되면 메모리에서 사라진다.  
   
### <font color="#04635b"> 힙 영역 (Heap Area) </font>  
* New라는 키워드로 생성된 객체를 저장하는 영역  
* 런타임시 생성되는 객체를 저장하는 공간, 자바에서 가비지 컬렉션이 수행되는 영역  
  
cf) `가비지 컬렉션` : 불필요한 메모리 공간을 정리하는 역할을 담당하는 역할  
  
   
- - -  
   
[참조1 (Naver D2 - JVM Internal)](https://d2.naver.com/helloworld/1230)   

