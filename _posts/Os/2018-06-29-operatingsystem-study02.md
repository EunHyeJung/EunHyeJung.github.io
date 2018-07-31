---
layout: post
title:  "컴퓨터 시스템의 동작원리-1"
date:   2018-06-29
author: EunHye Jung
categories: os
comment : true
tags:	운영체제 OpeartingSystem OS
cover:  "/assets/instacode.png"
---
   

### 컴퓨터 시스템의 구조  
  
* 컴퓨터 내부 장치 : CPU, 메모리  
  컴퓨터 외부 장치 : 디스크, 키보드, 마우스, 모니터, 네트워크 장치 등   
  
* 컴퓨터의 업무 처리방식  
  컴퓨터 외부 장치에서 컴퓨터 내부로 데이터를 읽어옴 : 입력(input)  
  -> 각종 연산을 수행한 후 그 결과를 컴퓨터 외부장치로 내보냄 : 출력(output)  
  우리가 카톡으로 보낼 메시지를 입력하고, 우리가 입력한 내용을 모니터를 통해 확인하는것도 일종의 입출력임!  
    
* 컴퓨터내의 각 하드웨어 장치에는 `컨트롤러(Controller:제어기)`라는것이 붙어있다.  
  컨트롤러는 일종의 작은 CPU라고도 하며, 각 하드웨어마다 존재하면서 이들을 제어한다.  
  
  
_ _ _
  
## CPU와 I/O연산  
   
![content01](/assets/contents/content02.PNG)  
  
* 컴퓨터 전체에 CPU라는 중앙처리장치가 있듯이, 컨트롤러는 각 하드웨어 장치마다 존재하면서, 이들을 제어하는 작은 CPU라고 할 수 있다.  
* 각 장치마다 설치된 컨트롤러에는 장치로부터 들어오고 나가는 데이터를 임시로 저장하기 위한 작은 메모리를 가지고 있다. 이것을 `로컬버퍼(local buffer)`라고 한다.   
* 예를 들어, 나는 요즘 왕자의 게임 미드를 메우 즐겨보고있다. 오늘도 어김없이 아침을 먹으면서 컴퓨터에 다운받아 놓은 왕좌의 게임을 보려고, 플레이어를 통해 왕좌의 게임 파일을 불러와서 재생시키려고 한다. 파일을 열려고 하는 이벤트가 발생하게 되면, 디스크 컨트롤러가 물리적인 디스크에서 내용을 읽어서, 이를 로컬버퍼에 저장하게 된다.  
   디스크에서 로컬버퍼로 내용을 다 읽어들어왔다면, 이것은 CPU에게 알려야 하는데, 이 알리는 행위를 `인터럽트(interrupt)`라고 한다.  
   ->  CPU가 데이터를 다 가져왔는지 확인하는 것이 아니라, 장치에 있는 컨트롤러가 체크하는 것이다!    
* CPU는 옆에 인터럽트 라인(interrupt line)이라는걸 가지고 있는데, 자신의 일을 하다가, 인터럽트 라인에 신호가 들어오면, 하던일을 멈추고, 인터럽트와 관련된 일을 처리하게 된다.    
  
* `인터럽트는 키보드 입력 혹은 디스크에서 데이터를 다 읽어왔다는 등의 이벤트를 CPU에게 알려줄 필요가 있을때 컨트롤러가 발생시키는 것이다.`  
    
  
_ _ _
  
## 인터럽트의 일반적인 기능  
  
* 운영체제 커널에는 인터럽트가 들어왔을때 해야할 일을 미리 다 프로그래밍해서 보관하고 있다.  
    이렇게 다양한 인터럽트에 대해 각각 처리해야할 업무들을 정의한것을 `인터럽트 처리 루틴`이라고 한다.  
* 앞의 예와 같이 디스크 컨트롤러가 인터럽트를 발생시키면, CPU는 하던일을 잠시 멈추고, 이 인터럽트가 발생했을때, 수행해야할 코드 영역(인터럽트 처리 루틴)으로 가서 정의된 일을 수행하게 된다.  
  이때, 수행하는 구체적인 일들은 다음과 같다.  
  먼저, 로컬 버퍼에 있는 내용을 플레이어 프로그램이 사용할 수 있도록, 메모리로 전달하고, 이제 플레이어가 CPU를 할당받을 경우 다음 명령(instruction)을 수행할 수 있음을 표시해둔다.  
* 운영체제는 할 일을 쉽게 찾아가기 위해 `인터럽트 벡터(vector)`를 가지고 있다.  
  인터럽트 벡터란, 인터럽트 종류마다 번호를 정해서, 번호에 따라 처리해야할 코드가 위치한 부분을 포인터로 가리키고 있는 자료구조를 말한다.   
* 실제 처리해야할 내용은 `인터럽트 서비스 루틴(interrupt service routine)`이라는 다른곳에 정의된다.
  인터럽트 서비스 루틴을 통해 해당하는 인터럽트 처리를 완료하고 나면, 원래 하고있던 작업으로 돌아가서 계속 하던일을 해야한다.  
  그래서 인터럽트 처리 전에 하고 있던 작업에 대한 정보를 반드시 저장해두어야 하고, 이런 정보를 저장하는 별도의 장소를 운영체제는 가지고 있다.  
    
#### 인터럽트 종류  
  
* 인터럽트에는 하드웨어 인터럽트와 소프트웨어 인터럽트가 있다.   
* CPU의 서비스가 필요한 경우, CPU옆에 있는 인터럽트 라인에 신호를 보내어서 인터럽트가 발생했다는것을 알려주는 방식을 동일하다.  
* `하드웨어 인터럽트`는 컨트롤러 등 하드웨어 장치가 CPU의 인터럽트 라인을 세팅하는 반면, `소프트웨어 인터럽트`는 소프트웨어가 그 일을 수행한다는 차이점이 있다.  

_ _ _
#### 프로그램  
  
* 통상적으로 프로그램은 여러 개의 함수로 구성된다. 
* 프로그램의 메모리 구조를 나눠보면 크게 코드(code), 스택(stack), 데이터(data) 등의 영역으로 나뉜다.  
1) **스택**  
A라는 함수를 실행 도중 B라는 함수 호출했을때, B함수가 종료되고 다시 A함수가 실행중이던 위치로 돌아가야 하는데, 이를 위한 복귀 주소를 저장하는 영역이 스택이다. 
2) **데이터**  
전역 변수 등 프로그램에서 사용하는 각종 데이터가 저장되는 공간.  
3) **코드**  
프로그래머가 작성한 코드가 기계어 명령(machine instruction) 형태로 저장되는 영역, CPU는 매 시점 코드 부분에 있는 명령을 하나씩 읽어와서 수행하게된다.  
  
- - -
  
## 인터럽트 핸들링  
  
* `인터럽트 핸들링(interrupt handling)`이란 인터럽트가 발생한 경우에 처리해야할 일의 절차를 의미한다.   
* 인터럽트는 함수호출과 유사한 메커니즘으로 처리되는데, 위에서 설명했듯이 다른 함수 실행 후 기존 함수가 처리하던 부분을 기억하고 있어야하듯이, CPU역시 인터럽트가 처리되고 난 다음에 기존에 하던 작업에 대한 정보를 먼저 저장해둔 다음에 인터럽트를 처리해야한다.  
* 운영체제 커널 영역에는 현재 시스템 내에서 수행되는 프로그램들을 관리하기 위한 자료구조인 `프로세스 제어  블록(PCB : Process Control Blcok)`을 가지고 있다. 
  인터럽트 수행이 끝나면, 프로세스 제어 블록에 저장된 값을 CPU다시 상에 복원해, 인터럽트 처리 전에 수행하던 작업을 계속할 수 있는것이다.  
* 인터럽트 처리루틴은 운영체제 커널 프로그램의 일부이고, 커널 역시 함수구조로 이루어져 있으므로 인터럽트 처리 코드가 수행되는 도중에도 함수 호출이 이루어질 수 있으므로 스택이 필요하다.   
인터럽트의 처리는 커널의 코드를 수행하는 것이므로, 인터럽트 처리 중 함수호출이 발생했을때 운영체제 커널의 주소 공간 중 `스택 영역`을 사용한다.    
* 현재 N개의 프로그램이 실행중일때, 커널 스택은 현재 실행중인 프로그램 수만큼 N만큼의 독립적인 공간을 둔다.  
  이는 비록 커널이 하나의 프로그램이지만, 여러 사용자 프로그램이 수행되는 도중에 인터럽트 등에 커널 코드가 수행될 수 있으므로, 커널은 일종의 공유코드라고 볼 수 있기 때문이다.  
  -> 인터럽트 처리 루틴으로 넘어와서 함수호출이 이루어질 경우에 각 프로세스별로 독자적인 커널 스택을 사용하게 된다.  
   
- - -
  
### 소프트웨어 인터럽트  
  
* 통상적으로 인터럽트라고 하면, 하드웨어 인터럽트를 의미하고, 소프트웨어 인터럽트는 `트랩(trap)`이라는 용어로 주로 불린다.  
* 소프트웨어 인터럽트의 예로는 `예외 상황(exception)`, `시스템 콜(system call)`등이 있다.  
  * `예외 상황`이란 프로세스가 0으로 나누는 연산 등 불가능한 작업을 시도하거나, 메모리 영역을 벗어난 잡근을 시도하려 할때 발생시키는 인터럽트를 말한다.  
  * `시스템 콜`은 프로그램이 자신이 작성하지 않은 코드를 운영체제로부터 서비스 받기위해 발생시키는 것이다.  
   예를 들어 우리는 printf()라는 함수를 이용해 화면에 원하는 내용을 출력할 수 있지만, 실제 printf() 함수를 직접 작성하지는 않는다. 이것은 printf() 내용을 이미 라이브러리 함수로 작성해두었고, 이 라이브러리 궁극적으로 운영체제 내에 정의된 write()라는 시스템 콜을 호출하기 때문이다.  
   - 시스템 콜과 일반적인 함수호출(function call)의 차이를 설명하자면,  
     시스템 콜은 운영체제에 정의된 함수를 호출하는 것을 말하며, 함수 호출은 자신이 작성한 함수 또는 라이브러리에 정의된 함수를 호출하는 것을 말한다.   
* 소프트웨어 인터럽트는 하드웨어 인터럽트처럼 컨트롤러가 발생시키는 인터럽트가 아니라, 프로그램 수행 도중 직접 CPU에 인터럽트 라인을 세팅하여 발생시키게 된다.  

_ _ _
  
-> **하드웨어 인터럽트**란 각종 하드웨어 장치들이 CPU에게 서비스를 받아야 하는 경우에만 발생시키게 되며, 이는 인터럽트 라인을 통해 CPU에게 전달된다.  
-> **소프트웨어 인터럽트**란 트랩이라고도 하며, 메모리영역 침범이나 불가능한 연산(ex)0으로 나누기)을 시도하는 예외 상황이나 시스템 콜시에 발생된다.  
  
- - -
  
[출저](https://book.naver.com/bookdb/book_detail.nhn?bid=4392911)  
  
    
      