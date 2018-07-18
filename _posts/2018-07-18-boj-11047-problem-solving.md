---
layout: post
title:  "BOJ-11047-동전"
date:   2018-07-18
author: EunHye Jung
categories: algorithm
tags:	algorithm greedyAlgorithm java boj acmicpc
comment : true
cover:  "/assets/instacode.png"
---
   
### BOJ 11047 동전-0    
  
  
[문제출저](https://www.acmicpc.net/problem/11047)   
   
   
- - -   
   
   
### 나의 풀이  
   
* 동전의 가치가 오름차순으로 주어진다. 이것을 배열 coin[]에 담는다.  
  무조건 동전의 개수를 최소화해야하므로 가장 큰돈의 단위로 거스름돈을 나눠주려한다.  
* 현재의 동전으로 최대한 많이 거스름돈을 나눠주고 (k / coin[i])  
  남은 금액(k % coin[i])과 그 다음으로 큰 거스름돈(coin[i-1])로 위와 같은 거스름돈은 나눠주는 행위를 반복한다. (k가 0원이될떄까지.)  
* 이렇게 현재 주어진 조건중 가장 최선이라 생각한 선택을 하는 알고리즘을 `그리디 알고리즘(Greedy Algorithm)`이라고 한다.  
  `그리디 알고리즘`은 그 순간에는 최선의 선택을 하지만, 그렇게 구한 결과가 항상 최적의 해라는 보장이 없다. 그러므로, 구한 해가 최적의 해인지에 대한 검증이 필요하다.  
* 이 문제가 그리디 알고리즘을 이용해 해가 구해진것은 주어진 거스름돈 동전들이 서로 배수를 이루고 있기에 가능하다.  
  만약, k가 10이고, 동전의 종류가 { 6, 5, 2, 1}이 되는 경우 (6, 2, 2,) -> 3개, (5, 5) -> 2개 가 되므로, 가장 큰 가치를 지닌 6을 선택하는것이 최적의해가 될수 없기 때문이다.   
  
  
<b> 코드 </b>  
    
```   
    public int getMinNumOfCoins(int[] coins, int n, int money) {
        int cnt = 0;
        int i = n - 1;
        while (money > 0 && i >= 0) {
            cnt += (money / coins[i]);
            money %= coins[i];
            i--;
        }
        return cnt;
    }
```     
    
       
         
          
          
          
          
