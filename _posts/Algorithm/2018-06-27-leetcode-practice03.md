---
layout: post
title:  "leetcode-283.Move Zeros"
date:   2018-06-27
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode
comment : true
cover:  "/assets/instacode.png"
---

## Leetcode 283.Move Zeros

### 문제	
	
[문제출저][source]	  
배열 nums가 주어질때, 모든 0을 배열의 끝으로 옮기기.   
0이 아닌 원소들의 순서는 유지할것.   
   
Example 1:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]


Note:
1. 배열 복사본을 만드지 않고 해결할것.    
2. 연산수를 최소화할것.   
	
- - -
	

### 풀이코드	
  		
  * i는 기존 배열의 인덱스를 나타내고 j는 최종 배열의 인덱스값을 가진다.  
  * 0이 아닌 숫자가 나오면 j값에 위치시키고, j값을 증가시켜준다.  
    만약 i의 값과 j값이 일치하지 않는다는 의미는, 원소의 이동이 있음을 의미하게 되고, 원소가 이동되었으므로, 기존의 값(nums[i])을 0으로 만들어준다.   
    	
```
    public void moveZeroes(int[] nums) {
		for (int i = 0, j = 0, n = nums.length; i < n; i++) {
			if (nums[i] != 0) {
				nums[j] = nums[i];
				if (i != j) {
					nums[i] = 0;
				}
				j++;
			}
		}  
    }
```
  	
- - -
    
#### 다른 사람의 코드
* 내가 푼것과 비슷하지만, 최종 배열에서의 인덱스값을 담는 변수가 0이 아닌 원소의 개수를 의미할 것이므로, 그 이후로, 배열의 길이만큼 0으로 채워주는 형태가 더 깔끔한것 같다.   
```
public void moveZeroes(int[] nums){
	int index=0;
    for (int i=0;i<nums.length;i++){
    	if (nums[i]!=0) nums[index++]=nums[i];
   	}
   	while(index<nums.length){
   		nums[index++]=0;
   	}
}
```

- - -
	
    
[source]:   https://leetcode.com/problems/move-zeroes/description/