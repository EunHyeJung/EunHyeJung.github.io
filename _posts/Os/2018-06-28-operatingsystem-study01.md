---
layout: post
title:  "운영체제 개요"
date:   2018-06-28
author: EunHye Jung
categories: os
comment : true
tags:	운영체제 OpeartingSystem OS
cover:  "/assets/instacode.png"
---
   
### 컴퓨터 시스템의 구조       
* 컴퓨터 내부 장치 : CPU, 메모리    
  컴퓨터 외부 장치 : 디스크, 키보드, 마우스, 모니터, 네트워크 장치 등    
     
* 컴퓨터의 업무처리 방식  
  컴퓨터 외부장치에서 컴퓨터 내부로 데이터를 읽어들어옴. (입력(input))    
  ->  각종 연산을 수행한 후 그 결과를 컴퓨터 외부장치로 내보냄. (출력(output))    
  우리가 카톡으로 보낼 메시지를 입력하고 전송한다음, 그 내용을 모니터로 확인하는것도 일종의 입출력이라고 할 수 있다.   
    
* 컴퓨터 내의 각 하드웨어 장치에는 `컨트롤러(Controller:제어기)`라는 것이 붙어있다.    
  컨트롤러는 일종의 작은 CPU라고도 불림, 각 하드웨어 장치마다 존재하면서 이들을 제어.    
  메모리를 제어하는 컨트롤러는 메모리 컨트롤러, 디스크를 제어하는 컨트롤러는 디스크컨트롤러!    


    
- - -
   
## 운영체제(Operation System)			      
### 운영체제 개념 및 정의    
* 하드웨어와 사용자 및 다른 소프트웨어를 연결해주는 것!		     
  우리가 컴퓨터를 켰을때 운영체제가 없으면 컴퓨터는 고철덩어리에 불과하며, 고철 덩어리를 최소한 동작시켜 주기 위해서 필요한 소프트웨어가 바로 운영체제!      
* 운영체제도 하나의 소프트웨어이기 때문에 컴퓨터의 전원이 켜지면 동시에 메모리에 올라가야 동작한다.    
  그런데 운영체제는 너무 크고 거대하기 때문에, 꼭 필요한 핵심적인 부분만 컴퓨터 전원이 켜질때 메모리에 올려놓고, 이외의 부분은 필요할때 그때그때 메모리에 올려놓고 사용함.      
  이 때, 핵심적인 부분을 **커널(Kernel)**이라고 부른다!    
     
        
          
  
- - -
    
### 운영체제의 기능    
* 운영체제가 컴퓨터 하드웨어와 사용자 사이에 존재하므로, 운영체제의 역할은 크게 다음 두가지로 나뉜다.   
  1) `하드웨어에 대한 역할`  : 하드웨어를 운영체제가 직접 관리  -> 시스템내의 자원(resource)들을 효율적으로 관리         
  2) `사용자에 대한 역할`  : 편리한 인터페이스 제공  -> 컴퓨터 시스템을 편리하게 사용할 수 있는 환경 제공    
   
   cf) 자원(resource) : CPU, 메모리, 하드디스크등 하드웨어 자원뿐만 아니라 소프트웨어 자원까지 통칭.    
    
  이 밖에도 운영체제는 사용자와 운영체제 자신을 보호하는 역할도 담당한다. (보안 및 보호)   
     
    
- - -
   
### 운영체제의 자원관리 기능
* 운영체제의 자원관리 기능은 운영체제의 핵심적인 기능이다.  
  이 때, 자원은 하드웨어 자원과 소프트웨어 자원으로 나뉜다.   
* 하드웨어 자원으로는 CPU, 메모리(memory), 주변장치 및 입출력 장치 등이 있음.   
  
- - -
   
#### CPU 관리    
* 일반적인 컴퓨터에는 CPU가 하나밖에 없지만 프로세스는 여러개가 동시에 실행됨.  
  -> 매 시점 어떤 프로세스에 CPU를 할당해 작업을 처리할것인지 결정해야함  -> 이것을 `CPU 스케줄링(CPU Scheduling)`이라고함.   
      
* CPU 스케줄링의 목표 : CPU를 가장 효율적으로 사용, 특정 프로세스가 불이익을 당하지 않도록 공정함 유지   
* CPU 스케줄링 기법     
  **1) 선입선출(FCFS, First Come First Service)**   
　      먼저 CPU를 사용하기위해 도착한 프로세스를 먼저 처리.  
　    공평성은 유지되지만, 짧은 작업이 긴작업을, 중요한 작업이 중요하지 않은 작업을 기다리는 현상 발생.          
  **2) 라운드 로빈(Round Robin)**    
　     CPU를 할당받아 사용할 수 있는 시간을 일정한 고정된 시간으로 제한.   
　     할당되는 시간이 커지면 FCFS기법과 같아지고, 할당되는 작으면 context-switching이 자주발생하여 효율성이 떨어짐.   
  **3) 우선순위(Priority)**     
　     대기중인 프로세스들에게 우선순위를 부여하고, 우선순위가 높은 프로세스에게 CPU를 먼저 할당.   
　     또한, 기다리는 시간이 늘어날수록 우선순위를 점차 높여주는것도 우선순위 스케줄링에 활용가능.  
    
- - -
   
#### 메모리 관리
* 물리적 메모리를 관리하는 방식에는 고정 분할 방식, 가변 분할 방식, 가상 메모리(virtual memory) 방식이 있음.   
       
   **1) 고정 분할(fixed partition) 방식**
　     물리적 메모리를 몇개의 영구적인 분할로 나눔. 나눠진 각각의 영역에 프로그램 하나씩 적재시킴 .    
　    최대 프로그램의 수가 분할 개수로 한정, 분할 크기보다 큰 프로그램은 적재가 불가능,   
　    분할 크기보다 작은 프로그램 적재시 남는 영역 발생 -> '내부조각(internal fragmentation)' 발생      
         
   **2) 가변 분할(variable partition) 방식**
　    매 시점 프로그램 크기에 맞게 메모리 분할.       
　    물리적 메모리보다 큰 프로그램 실행 불가능, 분할의 크기와 개수가 동적으로 변하므로 기술적 관리기법이 필요.       
　    필요한 크기만큼 메모리를 분할하므로 내부조각이 나오진 않지만,`외부 조각(external fragmentation)`이 발생할 수 있다.  
　    외부조각은 분할된 영역이 할당될 프로그램 크기보다 작기 때문에 프로그램이 할당될 수 없어 사용되지 않고 빈 공간으로      
　   남아있는 것을 말함.       
　   예를 들어, 크기가 100인 프로그램 A가 실행되어 메모리에 100만큼 영역을 할당받음,  
　   프로그램 A 실행중에 크기가 50인 프로그램 B가 실행되어 A 영역 바로 다음부터 메모리 50을 할당받음,  
　   이때, A의 작업이 끝나 A의 영역에 크기가 80인 프로그램 C가 적재됨, 이때, 20만큼의 빈공간이 생기게 되는데,     
 　  이후에 20보다 큰 프로그램들은 이 공간을 활용하지 못하게 되고, 계속 20만큼의 빈공간이 남음, 이것이 외부 조각!  
       
   **3) 가상 메모리(virtual memory) 기법**
　      용량이 작은 주기억장치를 마치 큰 용량을 가진것처럼 사용하는것! 물리적 메모리보다 큰 프로그램이 실행되는것을 지원.   
　      모든 프로그램은 물리적 메모리와는 독립적으로 주소가 0부터 시작하는 자신만의 가상 메모리를 가지게됨.  
　     운영체제는 가상 메모리의 주소를 물리적 메모리 주소로 매핑하는 기술을 이용해 주소를 변환 시킨 후 프로그램을   
　     물리적 메모리에 올림.  
　     간략히, 설명하자면, 물리적 메모리가 5만큼 있고, 프로그램의 크기가 20이라고 할때, 프로그램 전체는 항상 동시에  
　     사용되는것이 아니므로 현재 사용되고 있는 부분만 메모리에 올리고, 나머지는 하드디스크와 같은 보조기억장치에   
　     저장해두었다가 필요할때 적재하는 방식을 이용!  　
      
- - -
   
#### 주변 장치 및 입출력 장치 관리
* 주변 장치 및 입출력 자치는 CPU나 메모리와 달리 `인터럽트(interrupt)`라는 매커니즘을 이용해 관리됨.  
  주변 장치들은 CPU의 서비스가 필요한 경우에 신호를 발생시켜 서비스를 요청하게 되는데, 이 신호가 바로 인터럽트임.  
* 인터럽트는 요청하는 장치와 발생상황에 따라 다양한 종류가 있기 때문에 운영체제는 인터럽트 종류마다 서로 다른 인터럽트 처리 루틴을 가지고 있다.   
  `인터럽트 처리 루틴` : 인터럽츠가 발생했을 때 해주어야할 작업을 정의한 프로그램 코드. (운영체제 커널 내에 존재)   
  
  
      
- - -
   
### 운영체제의 분류
   
동시 작업을 지원하는 여부에 따라 단일작업용 운영체제와  다중작업용 운영체제로 나눠볼 수 있음.  
  
* **단일 작업(single tasking)용 운영체제 **    
  한번에 하나의 작업만 실행가능.     
  하나의 프로그램이 실행되는 동안, 다른 프로그램을 실행시킬 수 없음.  
    
* **다중 작업(multi tasking)용 운영체제**  
  동시에 여러개의 프로그램 처리 가능.   
  우리가 유툽으로 동영상보면서 카톡보내느것을 생각하면됨.  
  다중 작업(multi tasking)을 이해할 때 오해하면 안되는게 일반적으로 컴퓨터는 하나의 CPU를 가지고 있으므로,   
  결국은 CPU에서 매순간 하나의 프로그램을 실행시키는것임.   
  CPU의 처리 속도가 매우 빨라 여러 프로그램들이 번갈아가며 CPU에서 처리되고 있음에도, 사용자 입장에서 보면   
  동시에 여러개의 프로그램이 실행되는것처럼 보임.   
  
  
_ _ _
   
운영체제를 분류하는 또다른 기준으로는 작업을 처리하는 방식이 있음. 
   
* **일괄 처리(batch processing) 방식**  
  일정량 또는 일정 기간동안 작업들을 모아서 한꺼번에 처리하는 방식   
  사용자 입장에서는 응답시간이 길다는 단점이 존재, 급여 계산, 지불계산, 연결산등의 업무에 이용   
   
* **시분할(time sharing) 방식**  
  여러 작업을 처리할 때 일정된 시간단위로 작업을 번갈아 가며 수행, 라운드로빈방식이라고도 불림.   
    
* **실시간(real time) 처리 방식**  
  작업 처리 요구가 있는 즉시 처리하여 결과를 산출.   
  정해진 시간안에 반드시 종료되어야 하는 시스템에서 사용. 예로 공장제어 시스템, 미사일제어 시스템 등이 있음.  
  
  
  
_ _ _
  
[출저](https://book.naver.com/bookdb/book_detail.nhn?bid=4392911)
   