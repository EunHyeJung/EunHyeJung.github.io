---
layout: post
title:  "hackerrank-array-ds"
date:   2018-06-24
author: EunHye Jung
categories: algorithm
tags:	algorithm array datastructure java hackerrank
comment : true
cover:  "/assets/instacode.png"
---

## Array-DS

[문제출저][source]

### 문제

An array is a type of data structure that stores elements of the same type in a contiguous block of memory. In an array, , of size , each memory location has some unique index,  (where ), that can be referenced as  (you may also see it written as ).

Given an array, , of  integers, print each element in reverse order as a single line of space-separated integers.

Note: If you've already solved our C++ domain's Arrays Introduction challenge, you may want to skip this.

Input Format

The first line contains an integer,  (the number of integers in ). 
The second line contains  space-separated integers describing .

Constraints

Output Format

Print all  integers in  in reverse order as a single line of space-separated integers.

Sample Input 1

CopyDownload
Array: arr
1
4
3
2

 
4
1 4 3 2
Sample Output 1

2 3 4 1

- - -


### 풀이코드
  
  * 배열의 크기 N/2만큼 반복문을 돌면서 현재위치(i)의 값과 뒤에서 i위치(n-(i+1))의 값을을 차례로 swap해줌.  
  * 시간복잡도 O(N/2)   
    
```
	static int[] reverseArray(int[] a) {
		for (int i = 0, n = a.length / 2; i < n; i++) {
			int tmp = a[i];
			a[i] = a[n - (i + 1)];
			a[n - (i + 1)] = tmp;

		}
		return a;
	}
```  

- - -


[source](https://www.hackerrank.com/challenges/arrays-ds/problem)
  
