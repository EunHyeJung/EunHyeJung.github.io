---
layout: post
title:  "정렬 알고리즘-01"
date:   2018-07-12
author: EunHye Jung
categories: algorithm
comment : true
tags:	알고리즘 정렬알고리즘 Algorithm
cover:  "/assets/instacode.png"
---
   
### 버블 정렬 (Bubble Sorting)
    
* 인접한 두개의 값를 서로 비교하여, 왼쪽에 있는 값이 오른쪽에 있는값보다 크면 서로 위치 변경.  
* 1단계가 완료되면, 가장 큰 값이 가장 오른쪽에 위치!  
* n개의 수가 주어질때, 위의 과정을 n-1번 반복.  
* O(n^2)시간 걸리는 알고리즘.  
* 내림차순으로 이미 정렬되어 있는 경우가 최악, 이때 비교횟수는 n(n-1)/2
  
<b>버블 정렬 소스</b>   
   
```   

public void bubbleSorting(int[] arr) {
	int tmp = 0;
	for (int i = 0, n = arr.length; i < n - 1; i++) {
		for (int j = 0; j < n - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				tmp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = tmp;
			}
		}
	}
}
    
```    
   
[버블정렬 관련문제](https://www.hackerearth.com/practice/algorithms/sorting/bubble-sort/tutorial/)    
   
   
　  
- - -   
   
### 선택 정렬 (Selection Sorting)    
   
* 값들을 탐색하면서 가장 작은값을 찾고, 두번째로 작은 값을 찾고, 세번째로 작은 값을 순서대로 찾으면서  
  각자의 위치에 재배치시키면서 정렬.  
* O(n^2)시간 걸리는 알고리즘.  
   
  
<b>버블 정렬 소스</b>   
   
```   
	public void selectionSrorting(int[] arr) {
		int minIdx = Integer.MAX_VALUE;
		int tmp = 0;
		for (int i = 0, n = arr.length; i < n; i++) {
			minIdx = i;
			for (int j = i + 1; j < n; j++) {
				if (arr[minIdx] > arr[j]) {
					minIdx = j;
				}
			}
			// swap
			tmp = arr[i];
			arr[i] = arr[minIdx];
			arr[minIdx] = tmp;
		}
	}
```   
   
   
- - -
    
   
[선택정렬 관련문제](https://www.hackerearth.com/practice/algorithms/sorting/selection-sort/tutorial/)     
  　   
      　  
         
