---
layout: post
title:  "BOJ-11729-하노이탑이동순서"
date:   2018-08-06
author: EunHye Jung
categories: algorithm
tags:	algorithm divideandconquer java boj acmicpc
comment : true
cover:  "/assets/instacode.png"
---
   
### BOJ 11729 하노이 탑 이동순서   
  
  
[문제출저](https://www.acmicpc.net/problem/11729)   
   
   
- - -   
   
   
### 풀이  
   
* n = 5일경우를 생각해보면,  
  3번 장대에 가장 먼저 5번 원판을 옮겨놓아야한다. 그러기 위해선 우선, 1~4번까지의 원판을 2번 장대에 옮겨놓아야 1번 장대에 있는 5번 원판을 3번 장대로 옮길 수 있다.  
  `move(n, x, y)`를 1~n개의 원판을 x에서 y로 이동하는 함수라고 할 경우, 
  1~n-1개의 원판을 x에서 z로 이동시켜야 한다. (위에 설명에 빗대면 x는 1, y를3, z를 2라고 볼 수있음)   
  그 다음, n번 원판을 x에서 y로 이동시키고,  
  1~n-1개의 원판을 z에서 y로 이동시킨다.     
  
* 총 3개의 스텝이 나오는데,  
  1) 1~n-1개의 원판을 x에서 z로 이동시킴 : `move(n-1, x, z)`  
  2) n번 원판을 x에서 y로 이동시킴    
  3) 1~n-1개의 원판을 z에서 y로 이동시킴 : `move(n-1, z, y)`   
  
  
<b> 코드 </b>  
    
```java   
    // 1~n개의 원판을 x에서 y로 이동시킴
    public void move(int n, int x, int y) {
    	if(n == 0) {	// 이동시킬 원판이 없으면 종료
        	return;
        }
        solve(n-1, x, 6-x-y);  # 장대의 번호가 1,2,3 총 3개이므로 z = 6 - x- y가 됨
        print(x + " " + y);
        solve(n-1, 6-x-y, y);
    }
```     
           

          
          
          
          
