---
layout: post
title:  "기초 : 클래스, 객체, 객체지향 언어의 특징"
date:   2018-10-22
author: EunHye Jung
categories: java
comment : true
tags:	java, 자바, 클래스, 객체, 객체지향
cover:  "/assets/instacode.png"
---   
  
  
##  <font color = "#0E4D92"> 클래스 </font>  
  
* 현실 세계에 있는 대상의 속성과 동작을 추려내 필드와 메서드로 정의한 것.  
  '아직 메모리가 할당되지 않은 상태'  
  
   
- - - 
  
  
##  <font color = "#0E4D92"> 객체 </font>  
  
* 클래스라는 설계도를 기반으로 실제 메모리가 잡힌 것을 의미.   
  이런 객체들을 조합해서 전체 프로그램을 완성해나가는 것을 OOP(객체지향 프로그래밍)이라고 함.  
  
   
- - - 
  
  
##  <font color = "#0E4D92"> 객체지향 언어의 특징 </font>  
  
### <font color="#04635b"> 상속성 (Inheritance) </font>  
* 상위클래스의 특징을 하위 클래스가 물려받는 것.  
* 상속에 의해 메소드의 오버로딩과 오버라이딩의 개념, this와 super 키워드 등 OOP를 지원하기 위한 다양한 문법들이 생김.    
   
### <font color="#04635b"> 캡슐화 (Encapsulation) </font>  
* 실제 기능은 숨기고 접근 방법만 노출하는 것.  
* 캡슐화는 프로그램의 복잡도를 줄이는데 주로 사용한다. (알 필요가 없는 정보는 숨겨서 프로그램의 복잡도를 제어함)  
* 자바는 캡슐화를 위해 default, public, priate, protected 등 네 가지 타입의 접근 제한자를 제공.  
   
### <font color="#04635b"> 추상화 (Abstraction) </font>  
* 객체의 공통적인 기능을 뽑아내는 과정, 추상화를 이용하면 객체를 단순하게 표현하는 것이 가능해진다.  
* 추상화 과정  
  - 객체들이 공통적으로 가지고 있는 개념을 추출  
  - 공통 개념이 추출되면, 최소한의 기능을 가진 상위 개념의 객체를 가짐  
  - 나머지 객체는 상위 개념의 객체를 상속받아 구현하는 형태로 변경.  
    
### <font color="#04635b"> 다형성 (Polymorphism) </font>   
* 다형성이란 말그래도 "객체가 여러가지 형태를 가질 수 있다는 뜻"  
* 객체간의 결합도를 줄이기 위해 사용된 개념. 다형성을 이용하면 객체간의 연결을 유연하게 할 수 있다.  
* 예를 들어, 상속 관계의 경우 부모는 모든 자식을 포함하는 큰 개념이므로 상위 클래스 타입의 변수로 하위 클래스 타입의 모든 객체를 참조할 수 있다.  
  다형성을 이용해 코드를 작성하면, 새로운 하위 클래스를 추가하더라도, 기존의 코드를 변경할 필요가 없음.  
   
- - -  
   
  
##  <font color = "#0E4D92"> 자바의 접근제어자(Acess Modifier) </font>  
  
#### <font color="#04635b"> private </font>  
* 외부 객체에서 접근이 불가  
   
#### <font color="#04635b"> default </font>  
* 같은 패키지의 객체에서만 접근이 가능  
  
#### <font color="#04635b"> protected </font>  
* 상속 관계의 관계만 접근 가능, 일반 객체는 접근이 불가  
  
#### <font color="#04635b"> public </font>  
* 모든 객체에서 접근이 가능  
   
　  
private → default → protected → public 으로 갈수록 접근 가능한 범위가 커짐!  
   
     
   
- - - 
  
  
##  <font color = "#0E4D92"> 오버로딩(Overloading), 오버라이딩(Overriding) </font>  
  
### <font color="#04635b"> 오버로딩(Overloading) </font>  
* 같은 메소드 명을 가지지만 매개변수 갯수, 타입을 다르게 지정하는 방식.  
   
  
### <font color="#04635b"> 오버라이딩(Overriding) </font>  
* 상위 클래스의 메소드를 하위 클래스가 재정의하여 사용하는 방식.   
   
   
    
　  
