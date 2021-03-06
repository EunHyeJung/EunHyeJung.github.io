---
layout: post
title:  "가상메모리-03 (페이지프레임할당, 스레싱)"
date:   2018-07-24
author: EunHye Jung
categories: os
comment : true
tags:	운영체제 OpeartingSystem OS
cover:  "/assets/instacode.png"
---

   

   

### 페이지 프레임의 할당       
   

* 프로세스 여러개가 동시에 수행되는 상황에서 각 프로세스에게 얼마만큼의 메모리 공간을 할당할것인지를 결정해야 한다.  
* 기본적인 메모리 할당 알고리즘으로는 균둥할당방식, 비례할당방식, 우선순위 할당 3가지 방식이 있다.  
  * <b>균등할당(equal allocation) 방식 </b>  
   페이지 프레임은 균일하게 할당  
  * <b>비례할당(propotional allocation) 방식 </b>  
   프로세스의 크기에 비례해 페이지 프레임 할당  
  * <b>우선순위(priority allocation) 방식 </b>  
   프로세스의 우선순위에 따라 페이지 프레임을 다르게 할당   
   프로세스 중에 당장 CPU에서 실행될 프로세스에게 더 많은 페이지 프레임 할당
   
* 하지만 위에서 언급된 3가지 페이지 프레임 할당 알고리즘만으로는 프로세스의 페이지 참조 특성을 제대로 반영하지 못할 우려가 있다.  
  예를 들어, 현재 수행중인 프로세스의 수가 지나치게 많을 경우 프로레스당 할당되는 메모리량이 과도하게 적어질 수 있기 때문이다.  
  프로세스를 정상적으로 수행하기 위해서는 적어도 일정 수준 이상의 페이지 프레임을 각 프로세스에 할당해야 한다.  
* 예를 들어 반복문(loop)을 실행중인 프로세스의 경우 반복문을 구성하는 페이지들을 한꺼번에 메모리에 올려놓는 것이 유리하다.  
  만약, 반복문을 구성하는 페이지의 수보다 적은 양의 프레임을 할당한다면, 매반복마다 적어도 한번 이상의 페이지 부재가 발생해 결과적으로 시스템의 성능이 현저히 떨어질것이기 때문이다.   
* 프로세스에게 최소한으로 필요한 메모리의 양은 시간에 따라 다를 수 있다.   
  이와 같은 종합적인 상황을 고려해서 각 프로세스에게 할당되는 페이지 프레임의 수를 결정할 필요가 있으며, 경우에 따라서는 일부 프로세스에게 메모리를 할당하지 않은 방식으로 나머지 프로세스들에게 최소한의 메모리 요구량을 충족시킬 수 있어야 한다.  
    
   
- - -   
    
    
### 전역교체와 지역교체    
    
* 교체할 페이지를 선정할때, 교체 대상이 될 프레임의 범위를 어떻게 정할지에 따라 교체 방법을 `전역 교체(global replacement)`와 `지역 교체(local replacement)`로 구분할 수 있다.  
* 전역교체 방법은 모든 페이지 프레임이 교체 대상이 될 수 있는 방법이다.  
  지역교체 방법은 현재 수행중인 프로세스에게 할당된 프레임 내에서만 교체 대상을 선정할 수 있는 방법이다.  
* 지역교체 방법은 프로세스마다 페이지 프레임을 미리 할당하는 것을 전재로 한다.  
  반면, 전역교체 방법은 프로세스마다 메모리를 할당하는 것이 아니라 전체 메모리를 각 프로세스가 공유해서 사용하고, 교체 알고리즘에 근거해서 할당되는 메모리량이 가변적으로 변하는 방법이다.  
  예를 들어, LRU 알고리즘으로 전역교체를 한다면, 물리적 메모리 전체에 올라와있는 페이지 중 가장 오래전에 참조가 된 페이지를 교체한다.  
  그 페이지가 어떠한 프로세스에 속한것인지는 고려하지 않는다.  
  즉, 페이지 교체시 다른 프로세스에 할당된 프레임을 빼앗아 올릴 수 있는 방식인것이다.   
* LRU, LFU, 클럭 등의 알고리즘을 물리적 메모리 내에 존재하는 전체 페이지 프레임을 대상으로 적용할 경우, `전역 교체 방법`이 된다.  
* `지역교체` 방법에서는 해당 프로세스에게 할당된 프레임 내에서만 페이지를 교체할 수 있다.  
  프로세스별로 페이지 프레임을 할당하고, 교체할 페이지도 그 프로세스에게 할당된 프레임 내에서 선정하게 되는 것이다.   
  LRU, LFU 등의 알고리즘을 프로세스 별로 독자적으로 운영할때는 지역교체 방법이 있다.   
    
    
- - -   
     
     
### 스레싱(Trashing)   
    
    
* 프로세스가 원활하게 수행되기 위해서는 일정수준 이상의 페이지 프레임을 할당받아야 한다.  
* 집중적으로 참조되는 페이지들의 집합을 메모리에 한꺼번에 적재하지 못하면, 페이지 부재율(page fault rate)이 크게 상승해 CPU 이용율(CPU Utilization)이 급격히 떨어질 수 있다.  
  이와 같은 형상은 `스레싱`이라고 한다.   
* 운영체제는 CPU의 이용율이 낮을 경우, 메모리에 올라와있는 프로세스가 적기때문이라도 판단하게 된다.  
  준비큐에 프로세스가 단 하나라도 있으면, CPU는 그 프로세스를 실행하게 되므로 쉬지않고 일하게 된다.  
  그런데, CPU 이용율이 낮다는 것은 준비큐가 비는 경우가 발생한다는 뜻이다!   
  따라서 CPU 이용율이 낮으면 운영체제는 메모리에 올라와 있는 프로세스의 수를 늘리게 된다.  
  -> 메모리에 동시에 올라와 있는 프로세스의 수를 `다중 프로그래밍 정도(MPD : Multi-Programming Degree)`라고 부른다.   
  즉, MPD가 과도하게 높아지게 되면, 각 프로세스에게 할당되는 메모리양이 지나치게 감소하게 된다. 그렇게 되면 필요한 최소한의 페이지 프레임도 할당받지 못하는 상태가 되어, 페이지 부재가 빈번히 발생하게 된다.   
* 페이지 부재가 발생하면 디스트 I/O 작업을 수반하므로 문맥 교환을 통해 다른 프로세스에게 CPU가 이양된다.  
  하지만, 다른 프로세스 역시 할당받은 메모리의 양이 지나치게 적으면 페이지 부재가 발생할 수 밖에 없다. 그러면 또 다른 프로세스에게 CPU가 할당되게 된다. 이 같은 과정이 반복되면 시스템은 페이지 부재를 처리하느라 매우 분주해지고 CPU 이용율을 급격히 떨어지게 된다.  
  이 상황에서 OS는 메모리에 올라와 있는 프로세스 수가 적어 이러한 현상이 발생했다고 판단해, MPD를 높이기 위해 또 다른 프로세스를 메모리에 추가하게 된다.  
  이로 인해, 프로세스당 할당된 프레임의 수가 더욱 감소하고, 페이지 부재는 더욱 빈번히 발생하게 된다.  
* 프로세스들은 서로의 페이지를 교체하며 스왑인과 스왑아웃을 지속적으로 발생시키고, CPU는 대부분의 시간에 일을 하지 않게 된다.  
  이러한 현상을 `스레싱`이라고 한다.  
  (즉, 스레싱이란 프로세스의 처리 시간보다 페이지 교체에 소요되는 시간이 더 많아지는 현상을 뜻한다.)   
    
* 메모리내에 존재하는 프로세스의 수를 증가시키면 CPU 이용율은 이에 비례해서 증가하게 된다.   
 그러나 어느 한계치를 넘어서게 되면 CPU 이용율이 급격히 떨어지는것을 알 수 있다. (스레싱이 발생했기 때문이다.)  
 따라서, 스레싱이 발생하지 않도록 하면서 CPU 이용율을 최대한 높일 수 있도록 MPD를 조절하는것이 중요하다.  
* MPD를 적절히 조절해 CPU이용율을 높이는 동시에, 스레싱을 방지하는 방법에는 `워킹셋 알고리즘`과 `페이지빈도 알고리즘`이 있다.  
    
- - -  
   
   
### 워킹셋(working-set) 알고리즘   
   
* 프로세스는 일정 시간동안 특정 주소 영역을 집중적으로 참조하는 경향이 있다.  
  이렇게 집중적으로 참조되는 페이지들의 집합을 `지역성 집합(locality set)`이라고 한다.  
* 워킹셋 알고리즘은 이러한 지역성 집합이 메모리에 올라갈 수 있도록 보장하는 메모리 관리 알고리즘을 뜻한다.  
  프로세스가 일정시간동안 원할히 수행되기 위해서 메모리에 한꺼번에 올라가 있어야하는 페이지들의 집합을 `워킹셋(working set)`이라고 정의하고, 프로세스의 워킹셋을 구성하는 페이지들이 한꺼번에 메모리에 올라가 수 있는 경우에만 그 프로세스에게 메모리를 할당한다.  
  만약 그렇지 않은 경우에는 프로세스에게 할당된 페이지 프레임들을 모두 반납시킨 후 그 프로세스의 주소 공간 전체를 디스크로 스왑아웃 시킨다.   
* 한꺼번에 메모리에 올라가야할 페이즈들의 집합을 결정하기 위해 워킹셋 알고리즘은 `워킹셋 윈도(working-set window)`를 이용한다.     
  윈도우의 크기가 △인 경우, 워킹셋 알고리즘은 시각 Ti에서의 워킹셋 Ws(Ti)를 시간간격 [Ti-△, Ti]사이에 참조된 서로 다른 페이즈들의 집합으로 정의한다.  
  Ti시점에 워킹셋에 포함된 페이지들은 메모리를 유지하고, 그렇지 않은 페이지들은 메모리에서 내쫓기게 된다.  
* 워킹셋 알고리즘은 메모리에 올라와있는 프로세스들의 워킹셋 크기의 합이 프레임의 수보다 클 경우, 일부 프로세스를 스왑아웃시켜서 남은 프로세스의 워킹셋이 메모리에 모두 올라가는것을 보장한다.  
  (이는 MPD를 줄이는 효과가 있음.)  
   반면, 프로세스들의 워킹셋을 모두 할당한 후에도 프레임이 남아있는 경우, 스왑아웃되었던 프로세스를 다시 메모리에 올려서 워킹셋을 할당함으로써 MPD를 증가시킨다.  
  -> 워킹셋 알고리즘은 CPU 이용율을 높게 유지하면서 MPD를 적절히 조절해서 스페싱을 방지한다.   
* 윈도우 △크기가 너무 작으면 지역성 집합을 모두 수용하지 못할 우려가 있고, 반대로 윈도우 △크기가 너무 크면 여러 규모의 지역성 집합을 수용할 수 있는 반면 MPD가 감소해 CPU이용율이 낮아질 우려가 있다.  
  따라서 워킹셋 알고리즘에서 시스템의 성능을 향상시키기 위해서는 프로세스들의 지역성 집합을 효과적으로 탐지할 수 있는 윈도우 크기를 결정하는 것이 중요하다.  
  
  
_ _ _   
  
   
#### 페이지 부재 빈도 (PDFF : Page Fault Frequency) 알고리즘   
  
* 페이지 부재 빈도 알고리즘에서는 페이지 부재율을 주기적으로 조사하고, 이 값에 근거해서 각 프로세스에 할당할 메모리량을 조절한다.  
* 어떤 프로세스의 페이지 부재율이 시스템에 미리 정해놓은 상한값(upper bound)을 넘게 되면, 이 프로세스에 할당된 프레임의 수가 부족하다는 것을 의미하므로 이 프로세스에게 프레임을 추가로 더 할당한다.  
  이때, 추가로 할당할 빈 프레임이 없다면 일부 프로세스를 스왑아웃시켜 메모리에 올라가 있는 프로세스의 수를 조절한다.   
  반면, 프로세스의 부재율이 하한값(lower bound) 이하로 떨어지면, 이 프로세스에게 필요 이상으로 많은 프레임이 할당된것으로 간주해 프레임 수를 줄인다.  
  이런 방식으로 메모리 내에 존재하는 모든 프로세스에게 필요한 프레임을 다 할당한 후에도 프레임이 남은 경우, 스왑아웃 되었던 프로세스에게 프레임을 할당함으로써 MPD를 높이낟.   
   
   
- - -
    
[출저](https://book.naver.com/bookdb/book_detail.nhn?bid=4392911)  
   
    

