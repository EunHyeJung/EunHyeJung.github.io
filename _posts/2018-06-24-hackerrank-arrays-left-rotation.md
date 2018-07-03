---
layout: post
title:  "hackerrank-arrays-Left-Rotation"
date:   2018-06-24
author: EunHye Jung
categories: algorithm
tags:	algorithm array datastructure java hackerrank
comment : true
cover:  "/assets/instacode.png"
---

## Left Rotation

[문제출저][source]

### 문제
   
A left rotation operation on an array of size  shifts each of the array's elements  unit to the left. For example, if  left rotations are performed on array , then the array would become .   
   
Given an array of  integers and a number, , perform  left rotations on the array. Then print the updated array as a single line of space-separated integers.   
   
Input Format   
   
The first line contains two space-separated integers denoting the respective values of  (the number of integers) and  (the number of left rotations you must perform). 
The second line contains  space-separated integers describing the respective elements of the array's initial state.   
   
Constraints   
   
Output Format   
   
Print a single line of  space-separated integers denoting the final state of the array after performing  left rotations.
    
Sample Input
   
5 4  
1 2 3 4 5  
Sample Output   
   
5 1 2 3 4   
Explanation   
   
When we perform  left rotations, the array undergoes the following sequence of changes:   
  
Thus, we print the array's final state as a single line of space-separated values, which is 5 1 2 3 4.  

_ _ _

   

- - -


  
### 풀이코드
  
  * 조회한 배열원소의 개수를 체크하는 cnt변수를 가지고, cnt개수가 n이 될때까지 순회.   
  * d만큼 왼쪽으로 회전시킨다는것은 d만큼 시작위치를 이동시킨 후 순차적으로 배열을 순회하면 된다.   이때 인덱스의 범위가 초과되지않도록 주의해야한다.
    
    ```
     void rotateArray(int[] arr, int n, int d) {
        int cnt = 0, idx = d;
        while(cnt != n) {
            System.out.print(arr[idx % n] + " ");
            idx++;
            cnt++;
        }
    }
```
  
- - -

   

- - -


[source]:   https://www.hackerrank.com/challenges/array-left-rotation/problem

[source]:   https://www.hackerrank.com/challenges/arrays-ds/problem