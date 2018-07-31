---
layout: post
title:  "LinkedList(연결리스트)"
date:   2018-06-25
author: EunHye Jung
categories: java
comment : true
tags: LinkedList 연결리스트 Java
cover:  "/assets/instacode.png"
---
	
    
### LinkedList (연결리스트)	
  
  * 원소들이 연속적인 위치에 저장되지 않는 선형 자료구조.	
  * 모든 원소는 분리된 객체이고, 데이터 파트와 주소 파트를 가진다.	
    (원소들이 포인터와 주소들로 연결되있음.)   
  * 각각의 원소는 노드(node)라고도 불린다.   
  * 배열(array)에 비해 동적으로 원소들을 삽입과 삭제하기 편함,   
    하지만 원하는 값을 찾을때는 head부터 시작해서 연결된 노드들을 하나하나씩 찾아가야함.   
      
  * Java에서 연결리스트 클래스는 list 인터페이스를 구현함.   
  * 연결리스트 생성자(LinkedList Constructors)   
     1) **LinkedList()** : 빈(empty) 연결리스트를 생성할때 사용   
     2) **LinkedList(Collection C)** : 순서를 가진 리스트를 생성할 때 사용.	
    
    
- - -
 
     
### Method for Java LinkedList
  *(더 자세한 내용은 참조사이트에서 확인.)*
  * int size() : 리스트에 있는 원소의 수	
  * void clear() : 리스트에 있는 모든 원소 삭제	
  * void addFirst(Object element) : 리스트 가장 앞에 원소 삽입	
  * void addLast(Object element) : 리스트의 끝에 원소 삽입	
  * Object getFirst() : 연결리스트에서 가장 앞에 있는 원소 반환.	
  * Object getLast() : 연결리스트에서 가장 뒤에 있는 원소 반환.	
  * boolean add(Object elemetn) : 리스트에 가장 끝에 원소 추가.	
  * void add(int index, Object element) : 리스트에서 'index'위치에 원소 삽입.	
  * int indexOf(Object element) : 만약 원소를 발견하면, 처음 나왔을때의 index 반환, 없으면 -1 반환.   
  * int lastIndexOf(Object element) : 만약 원소를 발견하면, 가장 마지막으로 나왔을때의 index 반환, 없으면 -1 반환.	
  * Object remove() : 리스트에서 원소를 제거하고 제거된 원소를 반환.	
  * Object remove(int index) : 리스트에서 'index' 위치인 원소를 제거, 만약에 리스트가 비어있다면 'NoSuchElementException' 익셉션 발생.	
  * boolean remove(Object O) : 연결리스트에서 특정한 원소를 제거할 때 사용, boolean값 리턴.	
  * Object removeLast() : 연결리스트에서 가장 마지막 원소 삭제 후 반환.		
	
	
	
- - -
     
     
### 연관문제
*  [조세퍼드문제](https://www.acmicpc.net/problem/1158)
*  [Hacerrank-LinkedList](https://www.hackerrank.com/domains/data-structures?filters%5Bsubdomains%5D%5B%5D=linked-lists)

- - -

	
    
    
[참조](https://www.geeksforgeeks.org/linked-list-in-java/)