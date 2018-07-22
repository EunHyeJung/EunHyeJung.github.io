---
layout: post
title:  "이진탐색(Binary Search)"
date:   2018-07-22
author: EunHye Jung
categories: algorithm
tags:	algorithm binary search java
comment : true
cover:  "/assets/instacode.png"
---
  
## 탐색(Search)  
   
여러개의 자료 중에서 원하는 자료를 찾는 작업,  
탐색을 효율적으로 수행하는 것이 매우 중요하다.   
   
- - -    
   
    
### 순차 탐색(Sequential Search)    
    
탐색 방법 중 가장 간단하고 직접적인 탐색 기법 
정열되지 않은 배열의 항목들을 처음부터 마지막까지 하나씩 검사하여 원하는 항목을 찾아가는 방법    
   
```   
int seq_serach(int[] list, int key, int left, int right) {
	for(int i = left; i <= right; i++) {
    	if(list[i] == key) {
        	return i;   // 탐색 성공
        }
    }
    
    return -1;    // 탐색 실패
}
```     
    
    
- - -   
   
   
### 이진 탐색(Binary Search)    
    
* 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘. 
* 배열의 중앙값을 기준으로, 찾고자 하는 항목이 왼쪽 또는 오른쪽 부분 배열에 있는지 알아내어 탐색의 범위를 반으로 줄인다.    
  
[참조](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%EA%B2%80%EC%83%89_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)   
    
    
    
```   
// 반복문으로 이진 탐색 구현  
int binary_search(int[] list, int key, int left, int right) {
	while(left <= right) {
    	int middle = (low + high) / 2;
        if(key == list[middle]) {
        	return middle;
        } else if(key > list[middle]) {
        	low = middle + 1;
        }  else {
        	high = middle -1;
        }
    }
}
```   
   
```   
// 재귀문으로 이진 탐색 구현
int binary_search(int[] list, int key, int left, int right) {
	if(left > right) {
    	return false;
    }
    int mid = (left + right) / 2;
    if(list[mid == key]) {
    	return mid;
    } else if(key > list[mid]) {
    	return binary_search(list, key, mid + 1, right);
    } else {
    	return binary_search(list, key, left, mid - 1);
    }
     
}
```   
    
   
- - - 
   
#### 이진탐색 시간복잡도   
     
처음 이진탐색시 주어지는 원소의 개수가 N이라고 할때,
한번 탐색을 수행하면 원소의 절반(중간값보다 큰값 혹은 작은값들) 이 버려지므로 2/N개의 원소에 대해서 탐색하게 된다.   
두번째 탐색후에는 또 남은 원소의 절반이 버려지므로 2/N * 1/N,  
그 다음 차례도 마찬가지로 계속해서 반씩 줄어들게 되므로..   
K번 탐색을 수행하고 나면 (1/2)^k * N 개의 원소가 남개 될것이다.  
마지막까지 탐색을 수행하다 보면 결국 데이터가 1개남을때까지 반복할것이고
(1/2)^k ≒ 1 이 된다. 양면에 2^k를 곱한뒤 로그를 취해주면, K ≒ logN이 된다.  
즉, N개의 원소에서 시행횟수는 logN이 되고, 
이진탐색의 시간복잡도는 `O(logN)`으로 나타낼 수 있다.   
   
   

   
- - -    
   
   
### 이진탐색 관련문제    
    
#### BOJ 1920 수찾기      
   
[문제 출제](https://www.acmicpc.net/problem/1920)    
   
<b> 문제 풀이 </b>  
위에서 정리한 이진탐색 코드를 이용해 해당 숫자가 존재하는지 하나씩 체크해주면 된다.  
이진 탐색의 경우 `리스트가 오름차순 정렬` 되어 있는 상태가 전재조건이니깐 입력으로 주어진 A배열을 사전에 정렬해주어야 한다.  
   
[풀이소스](http://colorscripter.com/s/vBWwPDa)   
   
   








