---
layout: post
title:  "Factory Pattern - Design Pattern"
date:   2018-06-09 15:00:00
author: EunHye Jung
categories: java
tags:	DesignPattern FactoryPattern Java
cover:  "/assets/instacode.png"
---
   
출저 : [https://www.journaldev.com/1392/factory-design-pattern-in-java
][java-designpattern-factory] 
(학습용으로 번역한것이며, 오역 많을 수 있음.)
   
   
# Factory Design Pattern    

  팩토리 패턴은 다수의 하위클래스들을 가진 수퍼클래스가 있고, 입력에 따라 하위클래스 중 하나를 반환해야 할 때 사용된다.  
  이 패턴은 클라이언트 프로그램에서 팩토리클래스로 클래스의 객체생성을 담당한다.

   
  
  

- - -
   
   
  
### Factory Design Pattern Super Class    
   
   팩토리 디자인 패턴에서 수퍼클래스는 인터페이스(interface), 추상클래스(abstract class) 또는 일반적인 자바클래스가 될수있다.   
   이 포스팅의 예제에서는, toString()메소드를 오버라이드한 추상 수퍼 클래스를 사용할것이다.
   
   
   ```
public abstract class Computer {
	public abstract String getRAM();
	public abstract String getHDD();
	public abstract String getCPU();

	@Override
	public String toString() {
		return "RAM= " + this.getRAM() + ", HDD=" + this.getHDD() + ", CPU=" + this.getCPU();
	}
}
```
   
  
_ _ _
  
    
### Factory Design Pattern Sub Classes    
   
   아래 구현된 코드와 같이 PC와 Server 2개의 서브클래스가 있다. 그리고 이 클래스들은 둘다 Computer 수퍼클래스를 상속한다.
    
    
   ```
   public class PC extends Computer {
	private String ram;
	private String hdd;
	private String cpu;

	public PC(String ram, String hdd, String cpu) {
		this.ram = ram;
		this.hdd = hdd;
		this.cpu = cpu;
	}

	@Override
	public String getRAM() {
		return this.ram;
	}

	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}

}
   ```
   
   
```
public class Server extends Computer {

	private String ram;
	private String hdd;
	private String cpu;
    
    public Server(String ram, String hdd, String cpu) {
		this.ram = ram;
		this.hdd = hdd;
		this.cpu = cpu;
	}

	@Override
	public String getRAM() {
		return this.ram;
	}

	@Override
	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}
}
```
    

_ _ _
    
    
### Factory Class    
   
   수퍼클래스와 서브클래스가 준비되었으니, 이제 팩토리 클래스를 작성할 수 있다.
   기본적인 구현은 다음과 같다.
   
   
   
```
public class ComputerFactory {
	public static Computer getComputer(String type, String ram, String hdd, String cpu) {
		if("PC".equalsIgnoreCase(type)) {
			return new PC(ram, hdd, cpu);
		} else if("Server".equalsIgnoreCase(type)) {
			return new Server(ram, hdd, cpu);
		}
		
		return null;
	}
}
```
   
    
팩토리 디자인 패턴 메소드에서 중요한점들은 다음과 같다.
1. 우리는 팩토리 클래스를 싱글톤으로 유지하거나 상위클래스를 static으로 반환하는 메소드로 만들수있다.
2. 입력값에 따라서, 다른 하위클래스(subclass)가 생성되고 반환된다.
   getComputer는 팩토리 메소드인것이다.

    
    
위의 팩토리 디자인 패턴 구현을 사용한 테스트 코드는 다음과 같다.     
     
     
```
public class TestFactory {
	public static void main(String[] args) {
		Computer pc = ComputerFactory.getComputer("pc", "2 GB", "500 GB", "2.4 GHz");
		Computer server = ComputerFactory.getComputer("server", "16 GB", "1 TB", "2.9 GHz");

		System.out.println("Factory PC Config :: + " + pc);
		System.out.println("Facotry Server Config :: + " + server);
	}
}

```     
     
     
_ _ _
    
    
### Factory Design Pattern 장점   
   
   1. 팩토리 디자인 패턴은 구현보다 인터페이스에 대한 코드 접근 방식을 제공한다.  
   2. 팩토리 패턴은 클라이언트 코드에서 실제 구현 클래스의 인스턴스를 제거한다.   
      팩토리 패턴은 코드를 견고하게 만들고, 결합성을 낮추고 확장을 쉽게하도록 한다.    
      예를 들면, 클라이언트 프로그램이 인식하지 못하기 때문에, 우리는 쉽게 PC 클래스 구현을 변경할 수 있다.    
   3. 팩토리 패턴은 상속을 통해서 구현클래스와 클라이언트 클래스 사이에 추상화를 제공한다.
   
   

     
     
_ _ _
    
    
### Factory Design Pattern Example in JDK   
   1. java.util.Calendar, ResourceBundle 그리고 NomberFormat의 getIncance() 메소드는 팩토리패턴을 사용한다.  
   2. Boolean, Integer와 같은 wrapper 클래스에 있는 valueOf() 메소드
   
   
   
   
[java-designpattern-factory]:  https://www.journaldev.com/1392/factory-design-pattern-in-java
