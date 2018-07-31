---
layout: post
title:  "템플릿 패턴(Template Pattern)"
date:   2018-07-06
author: EunHye Jung
categories: java
tags:	designpattern java
comment : true
cover:  "/assets/instacode.png"
---

### 템플릿 패턴(Template Pattern) 
  
* `상위클래스에서 처리의 흐름을 결정하고, 하위클래스에서 구체적인 내용을 결정하는 디자인패턴`
* 상위클래스에서 `템플릿 역할을 하는 메소드`가 정의되어 있음.  
  그리고 이 메소드가 추상메소드들을 호출함.  
* 상위클래스의 이 메소드만 보면, 추상메소드들이 어떻게 호출되는지 알 수 있으나 최종적으로 어떤 처리를 하는지는 모른다.  
* 하위클래스가 추상메소드들을 실제 구현하게 되는데,   
  하위클래스별로 구현 내용이 다를 수 있다. 하지만, 처리의 큰 흐름은 상위클래스가 결정한대로 이루어진다.  
  

- - -

  
##### Example
여행계획을 세운다고 해보자.  
일반적으로 여행을 간다고하면, 비행기표를 사고, 숙박을 정하고, 여행코스를 짜야한다.  
이건 유럽여행을 가든, 동남아 여행을 가든, 아프리카로 여행을 가든지 어딜가는지 해당되는 사항인것이다.  
여기서, 비행기표를 사고, 숙박을 정하고, 여행코스를 짜는게 `템플릿`이 되는 것이다!  
어디를 가느냐에 따라서 어디행 비행기표를 사고, 어디서 자고, 어떤 코스로 여행을 하는지 달라지니깐 그건 어디를 가는지 정해지고 난 다음에 일인것이다.  
  
이 템플릿을 코드로 작성하면 다음과 같이 된다.  
  
  
```
public abstract class TravelPlan {

    public final void performTrip() {
        buyAirlineTicket();
        decideLodging();
        makeTourCourse();
    }

    public abstract void buyAirlineTicket();

    public abstract void decideLodging();

    public abstract void makeTourCourse();
}
```   
  
  
일본여행과 유럽여행을 가게 될경우, 위에 작성한 여행계획 템플릿을 상속받아서 다음과 같이 작성할 수 있게된다.   

* 일본여행계획 클래스 : JapanTravelPlan  
    
```
public class JapanTravelPlan extends TravelPlan {

    public JapanTravelPlan() {
        System.out.println("===  일본 여행 계획 === ");
    }

    @Override
    public void buyAirlineTicket() {
        System.out.println("일본행 비행기 티켓을 끊는다.");
    }

    @Override
    public void decideLodging() {
        System.out.println("비즈니스 호텔에서 숙박한다.");
    }

    @Override
    public void makeTourCourse() {
        System.out.println("일본 유명 라멘집에서 라멘을 먹는다.");
        System.out.println("아사히 맥주공장을 방문한다");
        System.out.println("유카타를 입고 기념샷을 남긴다.");
    }
}

```   
   
* 유럽여행계획 클래스 : EuropeTravelPlan  
   
```
public class EuropeTravelPlan extends TravelPlan {

    public EuropeTravelPlan() {
        System.out.println("===  유럽 여행 계획 === ");
    }

    @Override
    public void buyAirlineTicket() {
        System.out.println("유럽행 비행기 티켓을 끊는다.");
    }

    @Override
    public void decideLodging() {
        System.out.println("게스트하우스나 한인민박에서 숙박한다.");
    }

    @Override
    public void makeTourCourse() {
        System.out.println("에펠탑앞에서 인생샷을 건진다.");
        System.out.println("이탈리아에서는 젤라또를 먹는다.");
        System.out.println("와인을 1일 1잔 한다.");
    }
}
```   
   
* 테스트 클래스   
   
```
public class Main {

    public static void main(String[] args) {
        TravelPlan japanTravelPlan = new JapanTravelPlan();
        japanTravelPlan.performTrip();

        System.out.println();

        TravelPlan europeTravelPlan = new EuropeTravelPlan();
        europeTravelPlan.performTrip();
    }
}
```  
   
테스트 클래스를 돌려보면 다음과 같은 결과를 확인할 수 있다.  
   
```
===  일본 여행 계획 === 
일본행 비행기 티켓을 끊는다.
비즈니스 호텔에서 숙박한다.
일본 유명 라멘집에서 라멘을 먹는다.
아사히 맥주공장을 방문한다
유카타를 입고 기념샷을 남긴다.

===  유럽 여행 계획 === 
유럽행 비행기 티켓을 끊는다.
게스트하우스나 한인민박에서 숙박한다.
에펠탑앞에서 인생샷을 건진다.
이탈리아에서는 젤라또를 먹는다.
와인을 1일 1잔 한다.
```   
      
     

 #### 템플릿 메서드를 이용하면 좋은점은 뭘까?!  
* 로직을 공통화 할 수 있다 !  
  일본여행계획이든, 유럽여행계획이든 새로운 객체를 만들때 세부적인 내용이 어찌되었든간에,  
  비행기 티켓을 끊고, 숙박을 정하고, 여행코스를 짜겠구나~ 하고 알 수 있다.  
  친구가 아프리카 여행계획을 짠다고하면, "비행기 티켓끊고 어디서 잘지정하고, 여행코스짜는 메소드를 작성해"라고 하는것이 아니라   
  "여행계획 클래스를 상속받아서 채워넣어줘~"라고 하면된다!    
  
 

* 템플릿 패턴과 관련된 패턴으로는 `팩토리 패턴(Factory Pattern)`과 `전략 패턴(Startegy Pattern)`이 있다.  
  
  
      
        
