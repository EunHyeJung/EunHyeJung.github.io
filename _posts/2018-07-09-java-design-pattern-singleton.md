---
layout: post
title:  싱글톤 패턴(Singleton Pattern)"
date:   2018-07-09
author: EunHye Jung
categories: java
tags:	DesignPattern Java
cover:  "/assets/instacode.png"
---  
   
   
### 디자인 패턴 종류 살펴보기   
  
* 생성 패턴 (추상 객체 인스턴스화)   
  추상팩토리, 팩토리, 빌더, 프로토타입, 싱글톤  
* 구조 패턴 (객체 결합)   
  어댑터, 브리지, 컴포넌트, 데코레이트, 퍼싸드, 플라이웨이트, 프록시  
* 행위 패턴 (객체 간 커뮤니케이션)  
  책임 체인, 커맨드, 인터프리터, 반복자(iterator), 중재자, 메멘토, 옵서버, 상태, 전략(startegy), 템플릿 메소드, 비지터  
  
- - -    
   
이글은 [참조](https://www.journaldev.com/1377/java-singleton-design-pattern-best-practices-examples)를 번역한 것이며, 개인 공부목적으로 정리되었기에, 오역이나 잘못된 부분이 있을 수 있습니다.
  　
   
## Singleton Pattern   
  
  
- - -  
  

싱글톤을 구현하는데는 다양한 접근법들이 있지만, 모든 접근법들은 다음의 공통 개념들을 따르게 된다.  
* `private 생성자` : 외부에서 객체의 생성을 제한함!  
* `public static 메소드` : 클래스의 인스턴스를 반환, 다른곳에서 싱글톤 클래스의 객체를 얻을 수 있는 접근점!  
   
- - -   
   
### Eager initilization   
  
이른 초기화에서는, 싱글톤 클래스의 객체는 클래스가 로딩되는 시점에 생성된다.  
싱글톤 클래스를 만드는 가장 간단한 방법이지만, 클라이언트 애플리케이션이 사용하지 않을 경우에도 인스턴스가 생성되는 단점이 있다.  
  
```
	public class EagerInitializedSingleton {
    	private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();
        
        // 다른곳에서 생성자에 접근하는것을 막도록 하는 private 생성자
        private EagerInitializedSingleton();
    }
    
    public static EagerInitializedSingleton getInstance() {
    	return instance;
    }
    
```   
   
만약, 많은 자원을 사용하지 않는 싱글톤 클래스라면, 이른초기화 방법을 이용하면 된다. 하지만, 대부분의 경우 싱글톤 클래스들은 파일시스템이나 DB연결과 같은 자원들을 위해 만들어진다.   
그리고 만약에 클라이언트가 `getInstacne` 메소드를 호출하지 않는다면, 우리는 객체 생성하는것을 피해야한다! (사용하지도 않는것을 만드는건 자원낭비)  
또한, 이 메소드는 어떠한 예외처리도 하지않는다.  
   
- - -   
   
### static block initialization  
    
* 정적초기화블록 구현은 이른 초기화방법과 비슷하다. 하지만, 정적블록초기화는 클래스의 객체가 예외처리를 하는 static 블록에서 만들어진다.  
* 이른초기화와 정적블록초기화 둘다 사용되기 전에 만들어지기 떄문에, 그다지 좋은방법은 아니다.   
   
```
	public class StaticBlockSingleton {
      private static StaticBlocSingleton instance;
      
      private StaticBlockSingleton() {}
      
      static {
      	try {
        	instnace = new StaticBlockSingleton();
        } catch(Exception e) {
        	throws new RuntimeException("Exception occurred in creating singleton instance");
        }
      }
      
      public static StaticBlockSingleton getInstance() {
      	return instance;
      }
    }
```   
   
　  
- - -   
　  
### Lazy Initialization   
   
* 싱글톤 패턴을 구현하는 게으른 초기화 메소드는 인스턴스를 전역 접근 메소드(global access method)에서 만든다.  
* 이 방법은 단일 스레드 환경에서는 잘 작동한다. 하지만, 멀티 스레드 환경에서 만약 멀티 스레드들이 동시에 if조건절에 접근하게 된다면(instance가 null인지 체크하여, 인스턴스 생성) 문제가 될 수 있다.  
 동시에 if조건절에 스레드들이 접근하게 되면, 여러개의 객체가 생성되므로 싱글톤의 법칙에 위배된다.  

   
```
public class LazyInitializedSingleton {
	private static LazyInitializedSingleton instance;
    
    private LazyInitializedSingleton() {}
    
    public static LazyInitializedSingleton getInstance() {
    	if(instance == null) {
        	instnace = new LazyInitializedSingleton();
        }
        return instance;
    }
} 
```    
　  
- - -   
   
### Thread Safe Singleton   
   
* thread-safe한 싱글톤을 만드는 더 쉬운 방법은, 한번에 오직 한 스레드만 메소드에 접근가능하도록, 전역 접근 메소드를 synchronized 키워드를 이용해서 만드는 것이다.   
* 이 방법은 thread-safe한 방법이지만, synchronized 메소드를 사용하는 것은 프로그램의 성능을 저하시킨다.  
  ([synchronization 참조] (https://www.journaldev.com/1061/thread-safety-in-java))   
   
```
public class ThreadSafeSingleton {
	private static ThreadSafeSingleton instance;
    
    private ThreadSafeSingleton() {} 
    
    public static synchronized ThreadSafeSingleton getInstnace() {
    	if(instance == null) {
        	instnace = new ThreadSafeSingleton();
        }
        return instance;
    }
}
```    
   
* 매번 동기화를 체크하는 오버헤드를 줄이기 위해, `double checked locking` 방법을 이용한다.  
  이 접근에서는, synchronized 블록을 조건절 내에 추가하여, 인스턴스가 null일 경우에만 동기화 체크를 하도록 한다.  
    
```
public static ThreadSafeSingleton getInstnaceUsingDoubleLocking() {
	if(instance == null) {
    	synchronized(ThreadSafeSingleton.class) {
        	if(instance == null) {
            	instance = new ThreadSafeSingleton();
            }
        }
    }
}
```     
[Thread-Safe 싱글톤 좀 더 알아보기](https://www.journaldev.com/171/thread-safety-in-java-singleton-classes-with-example-code#comments)    
    
    
- - -
   
### Bill Pugh Singleton Implementation  
   
Java5 이전에 메모리 모델은 많은 이슈가 있었다. 그리고 위의 접근법들은 너무 많은 스레드들이 싱글톤 클래스의 인스턴스를 얻어가려할때 실패하곤 했다. 그래서 Bill Pugh는 `inner static helper class`를 사용하는 다른 싱글톤 클래스를 만들어 냈다.  
  
```
public class BillPughSingleton {
	private BillPughSingleton() {}
    
    private static class SingletonHelper {
    	private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }
    
    public static BillPughSingleton getInstance() {
    	return SingletonHelper.INSTANCE;
    }
}
```   
   
* `private inner static class`가 싱글톤 클래스의 객체를 포함하고 있는 사실에 주목하자!  
  싱글톤 클래스가 로드될때, `SingletonHelper` 클래스는 메모리에 로드되지 않고, 오직 누군가가 getInstance 메소드를 호출할때, 이 클래스가 로드되고, 싱글톤 클래스의 인스턴스가 만들어진다.  
* 이것은 싱글톤 클래스에 대해 널리 이용되는 방법이고, synchronization 키워드를 사용하지 않는다.  

   
- - -   
   
    
### Using Reflection to destory Singleton Pattern   
   
* Reflection은 위에서 언급된 모든 싱글턴 구현 접근법을 파괴할 수 있따.  
   
```   
public class RefelctionSingletonTest {
	public static void main(String[] args) {
    	EagerInitializedSingleton instanceOne = EagerInitializedSingleton.getInstance();
        EagerInitializedSingleton instanceTwo = null;
        
        try {
        	Contructor[] constructors = EagerInitializedSingleton.class.getDeclaredContructors();
            for(Constructor constructor : constructors) {
            	// 아래 코드는 싱글톤 패턴을 파괴할 것임.  
                constructor.setAccessible(true);
                instanceTwo = (EagerInitializedSingleton) constructor.newInstance();
                break;
            }
        } catch(Exception e) {
        	e.printStackTrace();
        }
        
        System.out.println(instanceOne.hashCode());
        System.out.println(instanceTwo.hashCode());
    
    }
}
```   
   
   
* 위의 테스트 클래스를 실행시켜보면, 인스턴스들의 해시코드가 다르다는것을 확인할 수 있을것이다.  
  Reflection은 매우 강력하며, 스프링과 하이버네이트와 같은 많은 프레임워크들에서도 사용된다.   
　  
*[Java Reflection 튜토리얼](https://www.journaldev.com/1789/java-reflection-example-tutorial)*
   
   
- - -   
   
　  
### Enum Singleton   
    
* Reflection과 같은 상황을 극복하기 위해, Joshua Bloch는 싱글톤 디자인 패턴을 구현할때, Enum을 사용할 것을 제안했다.   
  자바는 자바프로그램에서 enum 값이 단지 한번만 초기화되는것을 보장하기 때문이다.   
  싱글톤과 마찬가지로 Java Enum 값들은 전역적으로 접근이 가능하다.   
  Enum 타입의 단점은 유연하지 않다는 것이다. 예를 들면, 게으른 초기화(lazy initialization)을 허용하지 않는다!   
    
```  
public enum EnumSingleton {
	INSTANCE;
    
    public static void doSomething() {
    
    }
}
```   
      
　
