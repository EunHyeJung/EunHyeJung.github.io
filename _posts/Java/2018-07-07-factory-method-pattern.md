---
layout: post
title:  "디자인 패턴 : 팩토리 메소드 패턴(Factory Method Pattern)"
date:   2018-07-07
author: EunHye Jung
categories: java
tags:	designpattern factorymethodpattern factory-pattern java
comment : true
cover:  "/assets/instacode.png"
---

##  자바 디자인 패턴 - <font color = "#0E4D92">  팩토리 메소드 패턴(Factory Method Pattern) </font>
  
* `인스턴스 생성을 하위 클래스에 위임`  
* 템플릿 메소드 패턴을 변경한 패턴으로  
  인스턴스를 만드는 방법은 상위 클래스에서 결정하고,  
  인스턴스를 실제로 생성하는 일을 하위클래스에서 결정한다.  
* `구제적인 제품 생성`을 `공장`을 통해서 한다.   
* 팩토리 패턴은 수퍼클래스와 여러개의 서브클래스가 있는 상황에서 입력값에 따라서 하나의 서브클래스를 반환하는 상황일때 주로 사용한다.  
  클라이언트 클래스는 팩토리클래스에게 인스턴스를 생성하는 책임을 위임한다.   
  
#### 팩토리 메소드 패턴의 일반적인 클래스 다이어그램   
  
  
  ![content01](/assets/contents/content05.PNG)  
    
* Product(제품)의 역할  
  생성된 제품(인스턴스)이 가지고 있어야할 인터페이스(API)를 결정하는 추상클래스.   
  구체적인 역할은 하위클래스인 ConcreteProduct이 결정함.   
  
* Creator(생산자)의 역할  
  Product클래스를 생성하는 추상클래스  
  Creator는 실제 제품을 생성하는 일을 ConcreteCreator의 역할에 대해서 아무것도 모름!  
  
* ConcreteProduct(구체적인 제품)의 역할  
  구체적인 제품을 나타내는 클래스  
  
* ConcreteCreator(구체적 생산자)의 역할   
  구체적인 제품을 만드는 클래스   
    
- - -  	
  
##### Example     
   
**화장품을 만드는 공장을 생각해보자.**   
립스틱, 아이섀도우, 파우더팩트 등 다양한 화장품들이 존재하고,   
고객이 요청한 제품에 따라서, 공장에서 적합한 화장품을 만들어주는것이다.   
  
  ![content01](/assets/contents/content06.PNG)    
   
* 위 그림을 보면, 공장은 제품을 생성하는 역할을 담당하고, 화장품공장은 공장이 정의해놓은 틀을 가져와 화장품을 생산하는 로직을 구체적으로 구현하게 된다. 
* Product클래스는 '제품'을 표현한 추상클래스이며, use()와 haveFunction()는 하위클래스에 맡겨진다.  
  
```  
public abstract class Product {
	public abstract void use();
    public abstract void haveFunction();
}
```  
   
* Factory 추상 클래스는 다음과 같으며, create()는 큰 틀을 제공하는 `템플릿메소드`이며, 제품을 생산하고  
  생산된 제품을 반환한다.  
  createProduct()는 어떤 제품을 생성하는 것인지 구체적으로 하위클래스에서 구현하게 되며, `팩토리메소드` 역할을 담당한다.  
   
```   
public abstract class Factory {

	public final Product create(String category) {
		Product p = createProdcut(category);
		return p;
	}

	protected abstract Product createProdcut(String category);
}

```   
   
* 이제 제품(Product)이 가진 기본적인 기능들을 구체적으로 기술하는 하위클래스인 립스틱, 아이섀도우, 파우더 클래스를 만들어보자.   
   
립스틱 클래스   
  
```
public class Lipstick extends Product {
	private String category;

	public Lipstick(String cateogry) {
		System.out.println("이 제품은 " + category + "입니다.");
		this.category = category;
	}

	public Lipstick() {
		System.out.println("이 제품은 " + category + "입니다.");
	}

	@Override
	public void use() {
		System.out.println(category + "를 입술에 바릅니다.");
	}

	@Override
	public void haveFunction() {
		System.out.println(category + "는 입술을 생기있게 보이도록 합니다.");
	}

}
```
   
아이섀도우 클래스  
   
```
public class EyeShadow extends Product {
	private String category;

	public EyeShadow(String category) {
		System.out.println("이 제품은 " + category + "입니다.");
		this.category = category;
	}


	@Override
	public void use() {
		System.out.println(category + "를 눈두덩이에 바릅니다.");
	}

	@Override
	public void haveFunction() {
		System.out.println(category + "는 눈에 음영효과를 줍니다.");
	}
}
```
   
파우드 클래스(생략)   
  
* 이제 화장품 공장에서, 고객의 주문(화장품 종류)를 입력받으면, 해당하는 화장품을 생산해주도록 하자.  
  
```
public class CosmesticFactory extends Factory {

	@Override
	protected Product createProdcut(String category) {
		switch (category) {
		case CATEGORY.LIP_STICK:
			return new Lipstick(category);
		case CATEGORY.EYE_SHADOW:
			return new EyeShadow(category);
		}
		return null;
	}
}
```
   
   
* 테스트 
  
```
public class Main {
	public static void main(String[] args) {
		// 공장을 세움
		Factory factory = new CosmesticFactory();

		// 공장을 이용해서 화장품을 생성
		Product libStick = factory.create("립스틱");
		libStick.use();
		libStick.haveFunction();

		Product eyeShadow = factory.create("아이섀도우");
		eyeShadow.use();
		eyeShadow.haveFunction();
	}
}
```  
   
출력내용   
   
```
이 제품은 립스틱입니다.
립스틱를 입술에 바릅니다.
립스틱는 입술을 생기있게 보이도록 합니다.
이 제품은 아이섀도우입니다.
아이섀도우를 눈두덩이에 바릅니다.
아이섀도우는 눈에 음영효과를 줍니다.

```
    
       
- - -  
  
    
* 팩토리메소드 패턴과 관련된 패턴  
  * 템플릿 메소드 패턴 (Template Method Pattern)  
  * 싱글톤 패턴 (Singleton Pattern)   
  * 컴포지트 패턴 (Composite Pattern)   
  * 이터레이터 패턴 (Iterator Pattern)    
  
  
      
        
