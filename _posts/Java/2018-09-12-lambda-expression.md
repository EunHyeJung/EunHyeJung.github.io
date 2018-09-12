---
layout: post
title:  "람다 표현식(Lambda Expression)"
date:   2018-09-12
author: EunHye Jung
categories: java
comment : true
tags:	 java static exception
cover:  "/assets/instacode.png"
---  
   
     
### <font color="006498"> 람다 표현식 </font>       
      
      
* 람다 표현식은 간단히 말해 `메소드를 하나의 식으로 간단히 표현한 것` 이다.     
   

* 인터페이스 중에서 메소드를 하나만 가지고 있는 인터페이스를 `함수형 인터페이스`라고 한다.  
  예를 들어 쓰레드를 만들때 사용하는 Runnable 인터페이스는 run() 메소드 하나만 가지고 있다.  
   
   <b> Runnable를 이용해서 쓰레드를 만드는 방법 </b>  
  ```java  
  public static void main(String[] args) {
      new Thread(new Runnable() {
          @override
          public void run() {
              System.out.println("Hello");
          }
      }).start();
  }
  ```    
  
  쓰레드가 생성될때, 쓰레드 생성자 안에 넣은 run() 메소드가 실행된다.  
  자바는 메소드를 매개변수로 전달하는것이 아닌 인스턴스를 전달하기 때문이 run() 메소드를 가지고 있는 Runnable 객체를 만들어 전달하는것이다.  
  
  매번 객체를 생성하는것이 아닌 메소드를 매개변수로 전달하면서 더 편리하게 프로그래밍을 하기 위해 람다표현식을 사용!     
  
  
* 람다표현식에서는 객체를 직접 생성할 필요가 없음.  
    
  <b>람다식을 사용하여 쓰레드를 만드는 방법</b>    
  ```java   
  public void static main(String[] args) {
    new Thread(() -> {
        for(int i = 0; i < 10; i++) {
            System.out.println("Hello");
        }
    }).start();
  }
  ```   
    
  위 코드에서 `() > {...}` 부분이 람다식이 됨, 람다식은 다른 말로 `익명 메소드`라고도 함.       
  JVM은 쓰레드의 생성자를 보고 () -> {}이 무엇인지 대상을 추론한다. 그리고 Thread 생성자 api를 보면 Runnable 인터페이스를 받아들이는것을 알 수 있고, JVM은 THread 생성자가 Runable 인터페이스를 구현한 것에 와야 한다는 것을 알게 된다. 결과적으로 람다식을 unnable을 구현하는 객체로 자동으로 만들어서 매개변수로 넣어주게 된다.  
      
      
   
- - -   
   
     
### <font color="006498"> 람다식 문법 </font>       
      
        
`(매개변수 목록) -> { 실행문 }`   
           
* 람다식 작성예제   
  두개의 정수형 값을 입력으로 받아 큰 값을 반환하도록 하는 인터페이스를 정의하고, 이 인터페이스를 이용하는 클래스를 작성해보자.  
  
  ```java   
  # 
  public interface Compare {
      public int compareTo(int value1, int value2); 
  } 

  
  public class CompareExam {
      public static void exec(Compare compare) { // Compare인터페이스를 매개변수로 받아 이용하는 메소드
          int value1= 10, value2 = 20;
          int resValue = compare.compareTo(k, m); 
          System.out.println(resValue);
      }
      public static void main(String[] args) {
          exec((i, j)-> {
              return i - j;
          });
       }
  }
  ```    
  
  위에서 exec메소드는 compareTo메소드가 어떻게 구현되어 있느냐에 따라 다른 출력값을 가지게 된다.  
  자바는 메소드만 인자로 전달할 수 없고 반드시 객체를 생성해서 전달해주어야하는데, Java8부터 람다식이 생기면서, 마치 함수만 달하는것처럼 간편하게 문법을 사용할 수 있게 됨.  
  
  
- - -  
　
 　
[참고1_프로그래머스_자바중급](https://programmers.co.kr/learn/courses/9/lessons/280)
[참고2_TCPSCHOOL.com](http://tcpschool.com/java/java_lambda_concept)    
[참3_NaverD2](https://d2.naver.com/helloworld/4911107)   
   
     
        
   
