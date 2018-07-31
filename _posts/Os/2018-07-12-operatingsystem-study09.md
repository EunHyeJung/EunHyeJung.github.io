---
layout: post
title:  "CPU 스케줄링-02"
date:   2018-07-12
author: EunHye Jung
categories: os
comment : true
tags:	운영체제 OpeartingSystem OS
cover:  "/assets/instacode.png"
---
   
* `CPU` : 프로그램의 기계어 명령을 실제로 수행하는 컴퓨터내의 중앙처리장치.
* CPU는 일반적으로 시스템 내에 하나밖에 없으므로, 여러 프로그램이 동시에 수행되는 사용자 환경에서는 매우 효율적으로 관리되어야 하는 자원이다.  
   
   
### 스케줄링의 성능평가
    
* 스케줄링 기법의 성능을 평가하는 지표는 크게 `사용자 관점의 지표`와 `시스템 관점의지표`로 나누어 볼 수있다.  
* 시스템 관점의 지표 : `CPU 활용도`, `처리량`   
* 사용자 관점의 지표 : `소요시간`, `대기시간`, `응답시간`    
    
   
- - -
   
<b> CPU 활용도(CPU utilization) </b>    
   
CPU 활용도는 시스템의 전체 성능과 밀접한 관련이 있다. (CPU는 일반적으로 시스템당 하나이니깐)  
CPU가 일을 하지 않고 휴먼(idle)상태에 있는 시간을 최대한 줄이는 것이 스케줄링의 주요한 목표다.  
    
<b> 처리량 (throughtput)</b>    
   
처리량은 주어진 시간동안 준비큐에 기다리고 있는 프로세스중 몇개를 끝마쳤는지를 의미한다.  
여러 프로세스가 CPU를 기다리고 있는 상황에서 주어진 시간에 더 많은 프로세스들이 CPU 작업을 완료하기 위해서는, CPU 버스트가 짧은 프로세스에게 우선적으로 CPU를 할당하는것이 유리하다.  
  
<b> 소요시간 (trunaround time) </b>   
소요시간은 프로세스가 CPU를 요청한 시점부터 자신이 원하는 만큼 CPU를 다쓰고 CPU 버스트가 끝날때까지 걸리는 시간. 
-> 준비큐에서 기다린 시간 + 실제로 CPU를 사용한 시간  
프로그램이 시작해서 종료까지 걸린 시간을 의미하는것이 아님!  
  
<b> 대기시간 (waiting time) </b>  
대기시간은 프로세스가 준비큐에서 CPU를 얻는데까지 걸린 시간.  
한번의 CPU 버스트중에도 준비큐에서 기다린 시간이 여러번 발생할 수 있다.  
-> 대기시간이란 이번의 CPU버스트가 끝날때까지 준비큐에서 기다린 시간들의 합으로 볼 수 있다.  
   
<b> 응답시간 (response time) </b>   
응답시간은 준비큐에 들어온 후 첫번째 CPU를 획득하기 까지 기다린 시간을 의미한다.  
응답시간은 대화형 시스템에 적합한 성능척도!  

- - -   
   
CPU 성능평가의 지표들을 중국집을 예로 들어 비유해보면,  
`활용도`는 전체시간중 주방장이 일한 비율이되며, `처리량`은 주방장이 주어진 시간동안 몇명의 손님에게 요리를 제공했는지를 의미한다.  
`소요시간`은 손님이 중국집에 들어와서 주문함 음식을 먹고 나가는데까지 걸린 총 시간을 의미하며, `대기시간`은 음식을 먹는 시간을 제외하고, 순수하게 기다린 시간을 의미한다.  
`응답시간`은 최초의 음식이 나올때까지 기다린 시간을 생각하면 된다!  
   
　  
- - -   
   
### 스케줄링 알고리즘 (Scheduling Algorithm ) 
   
<b> FCFS (First-Come, First-Served) </b>     
* 프로세스가 준비큐에 도착한 시간 순서대로 CPU를 할당하는 방식.  
* 프로세스가 자발적으로 CPU를 반납할떄까지 CPU를 선점하지 않는다.  
* 먼저 도착한 프로세스의 성격에 따라 평균 대기시간이 크게 달라진다.   
  CPU 버스트가 긴 프로세스가 먼저 도착할 경우, 평균 대기시간이 길어지는 반면,  
  CPU 버스트가 짧은 프로세스가 먼저 도착하게 되면 평균 대기시간은 짧아지게 된다.  
* CPU 버스트가 짧은 프로세스가 긴 프로세스보다 나중에 도착해 오랜시간을 기다려야 하는 현상을 `콘보이 현상(convey effect)`이라 하며, 이는 FCFS 스케줄링의 대표적인 단점이다.  
   
<b> SFC (Shortest-Job First) </b>  
* CPU 버스트가 가장 짧은 프로세스에게 제일 먼저 CPU를 할당하는 방식  
* 평균대기 시간을 짧게 하는 최적의 알고리즘이다.  
* SJF 알고리즘은 비선점형 방식과 선점형 방식 두가지로 구현될 수 있다. 
  SJF의 선점형 구현 방식에서는 현재 CPU에서 실행중인 프로세스의 남은 CPU 버스트 시간보다 더 짧은 CPU 버스트 시간을 가지는 프로세스가 도착하면, CPU를 빼앗게 된다.  
  -> SFJ의 선점형 구현 방식을 `SRTF(Shortest Remaining Time First)`라고도 부른다.    
* 일반적으로 CPU를 기다리는 프로세스들이 준비큐에 동시에 도착하지는 않는다.  
 프로세스들이 준비큐에 도착하는 시간이 불규칙한 환경에서는 선점형 방식이 프로세스들의 평균 대기 시간을 최소화하는 최적의 알고리즘이 된다.  
 일반적으로 시분할 환경에서는 중간중간에 새로운 프로세스가 발생하므로 선점형 방식이 평균 대기 시간을 가장 많이 줄일 수 있는 방식이 된다.  
   
|<center> 프로세스 </center>| <center>도착 시간</center> |  <center>CPU 버스트 시간</center>
|--------|--------|--------|
| <center>P1</center>| <center>0</center>|<center>14</center>|
|<center>P2</center>|<center>4</center>|<center>8</center>|
|<center>P3</center>|<center>8</center>|<center>2</center>|
|<center>P4</center>|<center>10</center>|<center>8</center>|   
   
* 위 표에서 네개의 프로세스 P1, P2, P3, P4가 각각 위와 같은 도착시간과 CPU 버스트 시간을 가진다고 할때, SFJ 알고리즘의 평균대기 시간은 다음과 같다.  
   
 * SJF 비선점형 스케줄링  : (0 + 6 + 3 + 7) / 4 = 4   
 * SJF 선점형 스케줄링  : (9 + 1 + 0 + 2 ) / 4 = 3  
   
* SJF 스케줄링 기법의 구현에서 현실적으로 어려운 부분은 CPU 버스트 시간을 미리 알 수 없다는 점이다. 그래서  예측을 통해 CPU 버스트 시간을 구한 후 예측치가 가장 짧은 프로세스에게 CPU를 할당하게 된다.  
* SJF 알고리즘이 평균 대기 시간을 최소화하는 알고리즘이기는 하지만, 시스템에서 평균 대기 시간을 줄이는 것이 항상 좋은 방법이라고는 할 수 없다.  
  계속 CPU 버스트가 짧은 프로세스에게만 CPU를 할당하는 경우, CPU 버스트가 긴 프로세스는 준비큐에 줄서서 무한정 기다려야 하는 문제가 발생할 수 있기 때문이다.  
  이러한 현상을 `기아 현상(starvation)`이라고 하고, 이것은 SFJ 알고리즘의 심각한 문제점이 된다.   
    
    
   
<b> 우선순위 스케줄링(priority scheduling)</b>   
    
* `우선순위 스케줄링(prioirty scheduling)`이란, 준비큐에서 기다리는 프로세스들 중에서 우선순위가 가장 높은 프로세스에게 제일 먼저 CPU를 할당하는 방식이다.  
  이때, 우선순위는 우선순위 값(prioirty number)을 통해 표시하며 우선순위 값이 작을수록 높은 우선순위를 가지는 것으로 가정한다.  
* 우선순위를 결정하는 방식에는 여러가지가 있을 수 있다.  
  CPU 버스트 시간을 우선순위 값으로 정의하면, 우선순위 스케줄링은 SJF 알고리즘과 동일한 의미를 가지게 된다.  
  시스템과 관련된 중요한 작업을 수행하는 프로세스의 우선순위를 높게 부여하면, 이러한 프로세스가 CPU를 빨리 할당받을 수 있게 할 수도 있다.  
* 우선순위 스케줄링 방식에서의 문제점 중 하나는 `기아 현상`이 발생할 수도 있다는 점이다. 우선순위가 높은 프로세스가 계속 도착할 경우 우선순위가 낮은 프로세스는 CPU를 얻지 못한채 계속 기다려야 하는 상황이 발생할 수 있기 때문이다.  
  이러한 문제점을 해결하기 위해 `노화(aging) 기법`을 사용할 수 있다.  
  `노화 기법`이란 기다리는 시간이 길어지면 우선순위를 조금씩 높여 언젠가는 가장 높은 우선순위가 되어 CPU를 할당받을 수 있게 해주는 방법이다.    
    
    
   
   
<b> 라운드 로빈 스케줄링(round robin scheduling)</b>   
    
* 라운드 로빈(Round Robin) 스케줄링은 각각 프로세스가 CPU를 사용할 수 있는 시간이 특정 시간으로 제한하여, 이 시간을 경과하면 CPU를 회수해 준비큐에 줄 서 있는 다른 CPU에게 프로세스를 할당하는 기법이다.  
* 각 프로세스마다 한번에 CPU를 사용할 수 있는 최대 시간을 `할당 시간(time quantum)`이라고 부른다.   
  할당 시간이 너무 길면 라운드 로빈 스케줄링은 FCFS와 같은 결과를 나타내게 되며, 할당 시간이 너무 짧으면 CPU를 사용하는 프로세스가 너무 빈번하게 교체되어 문맥 교환의 오버헤드가 커지게 된다.  
* 라운드 로빈 스케줄링은 여러 종류의 이질적인 프로세스가 같이 실행되는 환경에서 효과적이며, 대화형 프로세스의 빠른 응답시간을 보장하는 장점을 가진다.  
* 할당 시간이 만료되어 CPU를 회수하는 방법으로는 `타이머 인터럽트`를 사용하게 된다.  
  만약 CPU 버스트 시간이 할당 시간보다 짧으면, CPU를 자신의 버스트만큼 사용한 후 스스로 반납하게 된다.  
* 라운드 로빈 스케줄링의 기본적인 목적은 CPU 버스트 시간이 짧은 프로세스가 빨리 CPU를 얻을 수 있도록 하는 동시에, CPU 버스트 시간이 긴 프로세스가 불이익을 당하지 않도록 하는 것이다. (공정한 스케줄링 방식)    
    
    
<b> 멀티 레벨 큐 (milti-level-queue) </b>  
* 준비 큐를 여러개로 분할해 관리하는 스케줄링 기법.  
  프로세스들이 CPU를 기다리기 위해 한 줄로 서는 것이 아니라 여러줄로 서는것을 말함.  
* 멀티 레벨 큐는 일반적으로 성격이 다른 프로세스들을 별도로 관리하고 프로세스의 성격에 맞는 스케줄링을 적용하기 위해 준비 큐를 별도로 두게 된다.  
* 멀티 레벨 큐에서 준비 큐는 보통 대화형 작업을 담기 위한 `전위 큐(foreground queue)`와 계산 위주의 작업을 담기 위한 `후위 큐(back-ground queue)`로 분할하여 운영한다.   
  전위 큐에서는 응답 시간을 짧게 하기 위해 라운드 로빈 스케줄링을 사용하며, 계산 위주의 작업을 위한 후위 큐에서는 응답 시간이 큰 의미를 가지지 않기 때문에, FCFS 스케줄링 기법을 사용해 문맥 교환 오버헤드를 줄이도록 한다.  
    
- - -   
   
###   스케줄링 알고리즘 평가  
   
* 스케줄링 알고리즘의 성능을 평가하는 방법으로는 다음과 같은 것들이 있다.  
  * 큐잉 모델 (queuing model)  
    주로 이론가들이 수행하는 방식, 확률 분포를 통해 프로세스들의 도착률과 CPU의 처리율을 입력값올 주면 복잡한 수학적 계산을 통해 각종 성능지표인 CPU 처리량, 프로세스의 평균 대기 시간 등을 구하게됨.  
  * 시뮬레이션 (simulation)  
    실제 시스템에서 구현해 수행시켜 보는 것이 아니라, 가상으로 CPU 스케줄링 프로그램을 작성한 후 프로그램의 CPU 요청값을 입력값으로 넣어 어떠한 결과가 나오는지 확인하는 방법  
  * 구현 및 실측 (implementation & measurement)  
    운영 체제 커널의 소스코드 중에서 CPU 스케줄링을 수행하는 코드를 수정해서 커널을 컴파일 한 후 시스템에 설치 한 후, 동일한 프로그램을 원래 커널과 CPU 스케줄러를 수정한 커널에서 수행시켜보며 실행 시간을 측정하여 알고리즘의 성능을 평가   
       
   
- - -
    
[출저](https://book.naver.com/bookdb/book_detail.nhn?bid=4392911)  
   
     
  　   
      　  
         