---
layout: post
title:  "정렬 알고리즘-02 (Counting Sort)"
date:   2018-07-15
author: EunHye Jung
categories: algorithm
comment : true
tags:	알고리즘 정렬알고리즘 Algorithm
cover:  "/assets/instacode.png"
---
   
### 계수 정렬(Counting Sort)
   
* 0부터N까지의 수를 정렬할때, 0부터 N까지의 빈도수의 누적합을 기반으로 정렬하는 방법  
* 선형시간(O(n))에 정렬 수행이 가능하다.  
  
<b>예제</b>   
   
예를 들어 배열 nums[] = { 1, 2, 2, 1, 3, 4, 4, 1 }에 대해 정렬을 수행한다고 하자.  
STEP 1) nums[]에 들어있는 원소들을 하나씩 확인하여 원소들을 카운팅하는 배열 count[0:4]에 저장해둔다.    
   
  ![content01](/assets/contents/counting-sort01.PNG)    
    
STEP2) 카운팅한 값을 기반으로, 누적합을 다음과 같이 구해준다.  
       누적합이 count[1] = 3이 됨으로써, nums[0]~nums[2[ (3개의 인덱스)가 1로 채워짐을 알 수 있다.  
       
  ![content02](/assets/contents/counting-sort02.PNG)    
        
STEP3) 기존의 배열 nums[]에서 뒤에서부터 원소들을 하나씩 가져와서 count[nums[idx]]에 있는 값을 기반으로 해당 원소의 정렬된 위치를 찾는다. 정렬될 배열 sortedNums[count[nums[idx]]에 해당 값을 넣어준 다음, count배열의 값을 하나씩 감소시켜주면서 정렬을 수행한다.   
   
     
     
<b> 계수정렬 소스코드 </b>
     
```   

public void countSort(int[] nums, int n, int maxValue) {
	int[] count = new int[maxValue + 1];

	// 배열의 각 원소 카운팅
	for(int idx = 0; idx N; idx) {
    	count[nums[idx]] += 1;
    }
    
    // 누적합 구하기
    int prev = 0
    for(int idx =0; idx= maxValue; idx++) {
    	if(count[idx] > 0) {
        	count[idx] += prev;
    		prev = count[idx];
        }
   }
   
   // 카운팅 정렬
   int[] sortedNums = new int[N];
   for(int idx = n-1; idx >=0; idx--) {
   	sorted[count[nums[idx]-1] = nums[idx];
        count[nums[idx]] -= 1;
   }
}
    
```    
   
[계수정렬 관련문제1](https://www.acmicpc.net/problem/10989)    
[계수정렬 관련문제2](https://www.hackerearth.com/practice/algorithms/sorting/counting-sort/tutorial/)     
   
　  
- - -   
   
  　   
      　  
         
