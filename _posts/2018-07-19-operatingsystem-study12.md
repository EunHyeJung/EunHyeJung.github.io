---
layout: post
title:  "메모리 관리-02"
date:   2018-07-19
author: EunHye Jung
categories: os
comment : true
tags:	운영체제 OpeartingSystem OS
cover:  "/assets/instacode.png"
---
   
   
### 물리적 메모리의 할당 방식   
   
물리적 메모리는 `운영체제 상주영역`과 `사용자 프로세스 영역`으로 나뉘어 사용된다.  
운영체제 상주영역은 물리적 메모리의 낮은 주소 영역을 사용하며, 운영체제 커널이 이곳에 위치하게 된다.  
사용자 프로세스 영역은 물리적 메모리의 높은 영역을 사용하며, 여러 사용자 프로세스들이 적재되어 실행된다.  
  
사용자 프로세스 영역의 관리 방법은 프로세스를 메모리에 올리는 방식에 따라 `연속할당`과 `불연속 할당` 방식으로 나누어 볼 수 있다.  
  
####  연속할당(contiguous allocation)    
각각의 프로세스를 물리적 메모리의 연속적인 공간이 올리는 방식.   
물리적 메모리를 다수의 분할로 나누어 하나의 분할에 하나의 프로세스가 적재되도록 한다.  
분할을 관리하는 방식에 따라 `고정 분할 방식`과 `가변 분할 방식`으로 나누어 볼 수 있다.  
  * <b>고정 분할 방식(fixed partition allocation)   </b>   
   물리적 메모리를 고정된 크기의 분할로 미리 나누어 두는 방식  
   동시에 올릴 수 있는 프로그램의 수가 고정되어 있으며, 수행가능한 프로그램의 최대 크기 또한 제한됨.  
   외부조각과 내부 조각이 발생할 수 있음.  
   cf) 외부조각 : 프로그램의 크기보다 분할의 크기가 작아 해당 분할이 비어있음에도 프로그램을 적재하지 못해 발생하는 메모리 공간   
      내부 조각 : 프로그램의 크기보다 분할의 크기가 큰 경우 해당 분할에 프로그램을 적재하고 남은 메모리 공간  
  * <b> 가변 분할 방식(variable partition allocation)   </b>    
   메모리에 적재되는 프로그램의 크기에 따라 분할의 크기, 개수가 동적으로 변하는 방식.  
   프로그램의 크기를 고려해서 메모리를 할당하고 이를 기술적으로 관리할 수 있는 기법이 피료함.  
   이미 메모리에 존재하는 프로그램이 종료될 경우, 중간에 빈 공간이 발생하게 되며, 이 공간이 새롭게 시작되는 프로그램의 크기보다 작을 경우 외부조각이 발생할 가능성이 있음.  
  가변부할 방식에서 중요하게 다루는 쟁점 중 하나는 프로세스를 메모리에 올릴때, 물리적 메모리 내의 가용 공간 중 어디에 올릴 것인지를 결정하는 문제이다. 이를 `동적 메모리 할당 문제(dynamic storage-allocation problem)   `이라고 부른다.  
  동적메모리 할당문제를 해결하는 대표적인 방법으로는 `최초적합(first-fit)`, `최적적합(best-fit)`, `최악 적합(worst-fit)` 3가지 방법이 있다.  
   
#### 불연속 할당방식(noncontiguous allocation) 
  하나의 프로세스를 물리적 메모리의 여러 영역에 분산해 적재하는 방식.  
  하나의 프로그램을 분할하는 기준에 따라 동알한 크기로 나누어 메모리에 올리는 `페이징 기법`, 크기는 일정하지 않지만, 의미 단위로 나누어 올리는 `세그멘테이션 기법`, 그리고 세그멘테이션 내에서 동일한 크기의 페이지로 나누어 메모리에 올리는 `페이지드 세그멘테이션` 기법이 있다.  
  
   * <b>페이징(paging) 기법   </b>    
     프로세스의 주소공간을 동알한 크기의 페이지로 잘라서 메모리에 페이지 단위로 적재.   
   *  <b>세그먼테이션(segmentation) 기법   </b>   
    프로그램의 주소공간을 코드, 데이터, 스택 등 의미있는 단위인 세그먼트로 나누어 세그먼트 단위로 적재하는 방법  
   *  <b>페이지드 세그먼테이션(paged segmentation) 기법   </b>     
    세그먼트 하나를 다수의 페이지로 구성하는 방법.  


     
- - -  
    
[출저](https://book.naver.com/bookdb/book_detail.nhn?bid=4392911)  
   
     
     