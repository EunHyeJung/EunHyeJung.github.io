---
layout: post
title:  "Singleton Pattern - Design Pattern"
date:   2018-06-09 12:59:00
author: EunHye Jung
categories: java
tags:	DesignPattern Java
cover:  "/assets/instacode.png"
---
   
   
   
# Java Singleton
   
   
* 싱글톤 패턴은 클래스의 인스턴스 생성을 제한하고 자바 가상머신에서 오직 하나의 클래스인스턴스만 존재하도록 한다.
* 싱글톤 패턴은 클래스의 인스턴스를 얻기 위해 반드시 전역 접근점(global access point)을 제공해야만 한다.
* 싱글톤 패턴은 로깅, 들이버 객체, 캐싱 및 스레드풀에서 주로 사용된다.
* 싱글톤 패턴은 또한, 추상팩토리 패턴, 빌더, 프로토타입, 퍼사드 패턴에서도 사용된다.
* 싱글톤 패턴은 코어 자바 클래스에서 또한 사용된다. 
  (ex) java.lng.Runtime, java.awt.Desktop )
  
  
  

- - -



## Java Singleton Pattern
   
   싱글톤 패턴을 구현하기 위해서, 우리는 다른 접근법들을 이용하지만 모두가 다음의 일반적인 개념을 따라 구현하게 된다.

* 다른 클래스에서 객체생성을 제한하기 위한 private 생성자.
* 클래스의 유일한 인스턴스인 동일한 클래스의 클래스의 private static 변수.
* 클래스의 인스턴스를 반환하는 공용 정적 메소드(public satic method). 이것은 외부에서 싱글톤클래스의 인스턴스를 얻기 위한전역 접근점이다.
    

    
   우리는 싱글톤 패턴 구현함에 있어 다양한 접근법들을 배울것이다.    
   
     
     
### 1. Eager initialization (이른 초기화 방식)
  이른 초기화 방식에서, 싱글톤 클래스의 객체는 클래스의 로딩시간에 생성된다.    
  이것은 싱글톤을 만드는 가장 쉬운 방법이지만, 클라이언트 애플리케이션이 이것을 사용하지 않더라도, 객체가 생성되는 단점을 가지고 있다.    
  
  ** 예제 코드 **
```
public class EagerInitializedSingleton {
	private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();

	// 클라이언트 애플리케이션의 생성자 사용을 막기위해 private으로 선언.
	private EagerInitializedSingleton() {
	}
	
	public static EagerInitializedSingleton getInstance() {
		return instance;
	}
}
```
   
 만약 사용하는 싱글톤 클래스가 많은 자원을 이용하지 않는다면, 이 접근방법은 유용하다.   
 하지만 대부분 싱글톤 클래스들은 DB 접속, 파일 시스템과 같은 자원들을 위해 만들어진다.     
 그리고 우리고 우리는 클라이언트가 ==getInstance== 메소드를 호출하지 않는다면, 객체생성할 필요가 없다.   
 또한, 이 메소드는 어떠한 예외처리를 위한 옵션을 제공하지 않는다.
  
   
   
_ _ _

   
   
   
   
### 2. Static block initialization
  정적 블록 초기화는 이른 초기화와 비슷한 구현방법이다. 하지만, 예외처리 옵션을 제공하는 정적 블록에서 