---
layout: post
title:  "leetcode643. Maximum Average Subarray"
date:   2018-07-29
author: EunHye Jung
categories: algorithm
tags:	algorithm leetcode java
cover:  "/assets/instacode.png"
---  
    
   
### 643. Maximum Average Subarray.  
  
[문제출저](https://leetcode.com/problems/maximum-average-subarray-i/description/)  
   
n개의 정수로 구성된 배열이 주어지면, 연속적인 부분배열의 크기가 k이고 k개로 이루어진 값이 최고의 평균값을 가지는 값을 찾아서 출력.   
  
<b> Example 1 </b>  
   
Input: [1,12,-5,-6,50,3], k = 4   
Output: 12.75   
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75   
  
<b> Note </b>  
1 <= k <= n <= 30,000  
배열에서 주어진 값은 -10000부터 10000까지의 범위를 가짐.    
      
      
- - -     
    
    
### Leetcode Artcle    
   
[출저](https://leetcode.com/articles/maximum-average-subarray/)    
    
    
#### 접근법 #1. 누적합 (Cumulative Sum)   
  
길이가 k인 서브배열의 평균을 구하기 위해선, 우선 길이가 k인 부분배열의 합을 먼저 구해야한다.   
이 합을 얻는 방법중 하나는 누적합 배열을 이용하는 것이다.  
`sum[i]`는 주어진 nums 배열의 요소들의 시작부터 인덱스 i까지의 합이 저징된다.   
일단 sum 배열이 채워지면, i부터 i+k까지 원소들의 합은 `sum[i] - sum[i - k]`을 통해 구할 수 있다.   
    
    
```java   
public double findMaxAverage(int[] nums, int k){
        int n = nums.length;
        int[] sum = new int[n];

        // 누적합 구하기
        sum[0] = nums[0];
        for (int i = 1; i < n; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }

        // 최대 평균구하기
        double maxAverage = (sum[k - 1] * 1.0) / k;
        for (int i = k; i < nums.length; i++) {
            maxAverage = Math.max(maxAverage, ((sum[i] - sum[i - k])) * 1.0 / k);
        }

        return maxAverage; 
}
```    
   
      
<b>복잡도 분석(Coplexity Analysis)</b>  
  
* 시간 복잡도(Time Complexity)   
  O(n)  
  우선, 누적합을 구하기 위해서 n길이만큼의 배열을 순회해야 한다.    
  그리고 나서, n-k만큼 반복하여 최대 평균값을 알아낸다.   
* 공간 복잡도(Space Complexity)   
  O(n)  
  배열 원소의 크기(n)만큼의 누적합을 담을 배열이 필요함.   
   
   
_ _ _   
   
    
#### 접근법 #2. 슬라이딩 윈도우 (Sliding Window)   
  
배열 nums에 대해 전체 누적합을 구하지 않아도 원하는 답을 얻으내는 방법이 있다.   
i부터 i+k까지의 원소들의 합을 구한뒤, 이것은 x라고 하자.  
그리고 i+1부터 i+k+1까지의 원소들의 합을 구한다고 하면, x에서 nums[i]를 빼고, nums[i+k+1]만 더하면 된다.  
nums[i+k+1]를 더하고 nums[i]를 빼는것은 결국 (nums[i+k+1] - nums[i])값을 더하는것과 같은 의미이다.  
  
    
```java   
public double findMaxAverage(int[] nums, int k){
        int n = nums.length;

        double sum = 0;

        // nums[0]부터 nums[k-1]까지의 합을 먼저 구함.
        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }
        double maxSum = sum;
        for (int i = k; i < n; i++) {
            sum += (nums[i] - nums[i - k]);
            maxSum = Math.max(maxSum, sum);
        }

        return maxSum / k; 
}
```    
  
  
  
<b>복잡도 분석(Coplexity Analysis)</b>  
  
* 시간 복잡도(Time Complexity)   
  O(n)  
  우리는 단지, 길이가 n인 배열인 nums을 한번만 순회하면 된다.  
* 공간 복잡도(Space Complexity)   
  O(1)  
   
   
