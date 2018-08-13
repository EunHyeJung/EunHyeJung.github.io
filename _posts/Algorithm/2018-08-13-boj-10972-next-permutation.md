---
layout: post
title:  "BOJ-10972-다음 순열"
date:   2018-08-13
author: EunHye Jung
categories: algorithm
tags:	algorithm divideandconquer java boj acmicpc
comment : true
cover:  "/assets/instacode.png"
---
   
### BOJ 10972 다음 순열   
  
  
[문제출저](https://www.acmicpc.net/problem/10972)   
   
1부터 N까지의 수로 이루어진 순열이 있을때, 사전순으로 다음에 오는 순열을 구하는 프로그램 작성.  
  
   
- - -   
   
   
### 풀이  
   
[Next lexicographical permutation](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm)  
  
<b> num = { 0 1 2 5 3 0 }</b>   
  
1) 가장 긴 감소하는 접미사(suffix)를 찾는다.  
   (뒤에서 부터 가장 긴 감소하는 부분 순열을 찾음)
   0 1 2 `5 3 0`   
   이 접미사 부분은 이미 최종 다음순열의 형태를 띄고 있다. (5, 3, 3, 0의 다음 순열은 존재하지 않음!)  
2) 가장 긴 감소하는 접미사사의 왼쪽 값이 pivot이 되고, pivot은 접미사의 가장 처음값보다 작을것이다. ( 2 < 5)  
  이제 접미사 부분에서 피봇값보다는 큰 수들중에 가장 작은 값을 찾아서 pivot값과 바꿔준다. (swap)  
  0 1 `3` 5 `2` 0   
3) 마지막으로, 접미사 부분을 증가하는 순서로 바꿔준다. (뒤집어주면됨)  
   0 1 3 `0 2 5`  
   왜냐하면 접두어부분을 초기에 0 1 2 인 상태에서 0 1 3인 상태로 증가시켜주었다.  
   그러므로 0 1 3 다음에 올 수 있는 순열은 0 1 3 으로 시작하는 순열 중 가장 작은 순열(사전상으로 가장 앞에 오는 순열)이 되어야하기 때문이다.  
4) 그래서 0 1 2 5 3 0의 다음 순열은 0 1 3 0 2 5가 된다.  
   
  

  
  
<b> 코드 </b>  
    
```java   
	public  boolean getNextPermutation(int[] nums, int n) {
		int i = n - 1;
		while (i > 0 && (nums[i - 1] > nums[i])) {
			i -= 1;
		}

		int pivotIdx = i - 1;
		if (pivotIdx < 0) {
			return false;
		} else {
			int j = n - 1;
			while (j > i && nums[j] < nums[pivotIdx]) {
				j -= 1;
			}

			// swap
			int tmp = nums[pivotIdx];
			nums[pivotIdx] = nums[j];
			nums[j] = tmp;
			// reverse nums[i] ~ [n-1]
			int l = i;
			int r = n - 1;
			while (l < r) {
				tmp = nums[l];
				nums[l] = nums[r];
				nums[r] = tmp;
				l += 1;
				r -= 1;
			}
		}

		return true;
	}
   
```     
           
- - -   
   
   
* <b> 연관문제  </b>  
  [이전 순열](https://www.acmicpc.net/problem/10973)   
  [모든 순열](https://www.acmicpc.net/problem/10974)   
  [순열의 순서](https://www.acmicpc.net/problem/1722)   
          
          
          
          
