---
layout: post
title:  "BOJ-11053, 11054, 11055 증가하는 부분 수열 시리즈 (DP)"
date:   2018-09-16
author: EunHye Jung
categories: algorithm
tags:	algorithm java boj acmicpc
comment : true
cover:  "/assets/instacode.png"
---  
   
  
### <font color = "3B5998"> BOJ 11053 가장 긴 증가하는 부분 수열     </font>
  
   
[문제출저](https://www.acmicpc.net/problem/11053)   
  
     
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.   
    
예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.   
   
        
- - -   
   
   
### 풀이  
   
`dp[i] : i번째 위치까지 탐색했을때 가장 긴 증가하는 부분 수열의 길이.  `   
  
수열 A가 int형 배열 nums에 담겨져있고, i번째 위치에서 가장 긴 증가하는 부분 수열을 구한다고 할때,
우선 dp[i]의 값은 1로 세팅된다. (nums[i]값 자체 1개가 있으므로)  
그 다음 0부터 i-1까지 가장 긴 증가하는 부분 수열의 길이를 확인하는데,   
이때의 인덱스를 j라고 하자. (j는 0~i-1중 가장 긴 증가하는 부분 수열의 길이를 가리키는 인덱스)
이제 dp[i]값이 업데이트 여부를 확인해주면 되는데 nums[i] > nums[j]이고, dp[j] > dp[i] + 1 이면   
dp[i]의 값을 업데이트 해준다.  
2중 for문을 이용하여서 dp값을 n까지 채워나가면 문제를 해결할 수 있다.  
  
   
 - - -  
    
  
#### 소스코드   
  
```java   
int[] dp = new int[n];
int maxLength = 0;
for (int i = 0; i < n; i++) {
	dp[i] = 1;
	for (int j = 0; j < i; j++) {
		if (nums[i] > nums[j] && dp[j] + 1 > dp[i]) {
			dp[i] = dp[j] + 1;
		}
	}
	maxLength = Math.max(maxLength, dp[i]);
}
```   
  
　  
[BOJ 11053 전체소스](https://github.com/EunHyeJung/AlgorithmStudy/blob/master/BOJ/BOJ11053.java)   
   
   　  
      
<hr>   
   
  
### <font color = "3B5998"> BOJ 11055 가장 큰 증가하는 부분 수열     </font>
   
   
[문제출저](https://www.acmicpc.net/problem/11055)   
  
   
수열 A가 주어졌을 때, 그 수열의 증가 부분 수열 중에서 합이 가장 큰 것을 구하는 프로그램을 작성하시오.  
   
예를 들어, 수열 A = {1, 100, 2, 50, 60, 3, 5, 6, 7, 8} 인 경우에 합이 가장 큰 증가 부분 수열은 A = {<b>1</b>, 100, <b>2</b>, <b>50</b>, <b>60</b>, 3, 5, 6, 7, 8} 이고, 합은 113이다.    
   
        
- - -   
   
   
### 풀이  
   
`dp[i] : i번째 위치까지 탐색했을때 증가하는 부분 수열의 가장 큰 합   `   
  
가장 긴 증가하는 부분 수열의 길이와 유사한 문제.  
초기값 dp[i]의 값은 nums[i]값으로 할당해준다. 그리고 현재의 값 num[i]이 nums[j] 보다 크고 (j는 0이상 i 미만의 범위를 가짐)  
현재 값과 dp[j]의 값을 더했을때(nums[i] + dp[j]) dp[i]값보다 크면 그게 최종적으로 가장 큰 합이 되므로   
dp[i]의 값을 업데이트 시켜주면서 n까지 dp배열을 채워나간다.   
  
   
 - - -  
    
  
#### 소스코드   
  
```java   
int[] dp = new int[n];
int maxSum = 0;
for (int i = 0; i < n; i++) {
	dp[i] = nums[i];
	for (int j = 0; j < i; j++) {
		if (nums[i] > nums[j] && nums[i] + dp[j] > dp[i]) {
			dp[i] = nums[i] + dp[j];
		}
	}
	maxSum = Math.max(dp[i], maxSum);
}
```   
  
　  
[BOJ 11055 전체소스](https://github.com/EunHyeJung/AlgorithmStudy/blob/master/BOJ/BOJ11055.java)   
   
   　  
      
<hr>    
   　  
   
  
### <font color = "3B5998"> BOJ 11054 가장 긴 바이토닉 부분 수열     </font>
  
   
[문제출저](https://www.acmicpc.net/problem/11054)   
  
     
수열 S가 어떤 수 Sk를 기준으로 S1 < S2 < ... Sk-1 < Sk > Sk+1 > ... SN-1 > SN을 만족한다면, 그 수열을 바이토닉 수열이라고 한다.    

예를 들어, {10, 20, 30, 25, 20}과 {10, 20, 30, 40}, {50, 40, 25, 10} 은 바이토닉 수열이지만,  {1, 2, 3, 2, 1, 2, 3, 2, 1}과 {10, 20, 30, 40, 20, 30} 은 바이토닉 수열이 아니다.    
  
수열 A가 주어졌을 때, 그 수열의 부분 수열 중 바이토닉 수열이면서 가장 긴 수열의 길이를 구하는 프로그램을 작성하시오.   
   
        
- - -   
   
   
### 풀이  
   
가장 긴 증가하는 부분 수열 길이 + 가장 긴 감소하는 부분 수열 길이 문제의 짬뽕  
위의 2가지 경우의 수를 충족하는 dp값을 각각 구해주면 문제를 해결할 수 있다.  
2차원 배열 dp[i][2]를 이용해서 문제를 풀었다.  
  
`dp[i][0]` : 가장 긴 증가하는 부분 수열의 길이  
`dp[i][1]` : 가장 긴 감소하는 부분 수열의 길이   
    
dp[i][0] + dp[i][1]의 값이 최대가 되는 경우가 가장 긴 바이토닉 부분 수열의 길이가 된다.  
이때, dp[i][0]과 dp[i][1]에는 둘다 nums[i]의 값이 포함되어 계산되었으므로 dp[i][0] + dp[i][1]에서 중복된 nums[i]값을 처리해주기위해 1을 빼준 값을 취한다.  
   
 - - -  
    
  
#### 소스코드   
  
```java   
int[][] dp = new int[n][2];
int maxLength = 0;

// 가장 긴 증가하는 부분 수열의 길이
for (int i = 0; i < n; i++) {
	dp[i][0] = 1;
	for (int j = 0; j < i; j++) {
		if (nums[i] > nums[j] && dp[j][0] + 1 > dp[i][0]) {
			dp[i][0] = dp[j][0] + 1;
		}
	}
}

// 가장 긴 감소하는 부분 수열의 길이
for (int i = n - 1; i >= 0; i--) {
	dp[i][1] = 1;
	for (int j = n - 1; j > i; j--) {
        if (nums[i] > nums[j] && dp[j][1] + 1 > dp[i][1]) {
            dp[i][1] = dp[j][1] + 1;
        }
	}
}

// 가장 긴 바이토닉 부분 수열의 길이 구해주기
for (int i = 0; i < n; i++) {
	maxLength = Math.max(maxLength, dp[i][0] + dp[i][1] - 1);
}
```   
  
　  
[BOJ 11054 전체소스](https://github.com/EunHyeJung/AlgorithmStudy/blob/master/BOJ/BOJ11054.java)   
   
   　  
      
<hr>      
   
   
